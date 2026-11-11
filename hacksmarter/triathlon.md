# Triathlon

## Enumeration&#x20;

### Nmap scan&#x20;

```
nmap 10.1.82.202 10.1.252.183 10.1.27.247                                
Starting Nmap 7.99 ( https://nmap.org ) at 2026-11-10 15:59 -0500
Nmap scan report for 10.1.82.202
Host is up (0.058s latency).
Not shown: 995 filtered tcp ports (no-response)
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

Nmap scan report for 10.1.252.183
Host is up (0.047s latency).
Not shown: 987 filtered tcp ports (no-response)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

 nmap 10.1.27.247 -Pn 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-11-10 16:01 -0500
Nmap scan report for 10.1.27.247
Host is up (0.058s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE
135/tcp  open  msrpc
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

```

Based on the lab description, I searched public records for the 2025 USA Triathlon Team roster. I located the official announcement, which narrowed down the targets to 9 specific athletes.

#### OSNIT - [https://www.usatriathlon.org/articles/news/usa-triathlon-announces-2025-u-s-elite-triathlon-national-team<br>](https://www.usatriathlon.org/articles/news/usa-triathlon-announces-2025-u-s-elite-triathlon-national-team)

Using Kerbrute to enumerate valid domain accounts with various naming conventions, I identified the f.last format as active and extracted the full user list

<figure><img src="../.gitbook/assets/image (492).png" alt=""><figcaption></figcaption></figure>

I performed AS-REP Roasting (GetNPUsers.py) using the discovered usernames and successfully retrieved an AS-REP hash for the user t.spivey, but unforntunately the hash was not crackable

<figure><img src="../.gitbook/assets/image (493).png" alt=""><figcaption></figcaption></figure>

Leveraged GetUserSPNs.py -no-preauth to enumerate SPNs without providing valid credentials.

<figure><img src="../.gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure>

I cracked the extracted hash using Hashcat with the **`rockyou.txt`** wordlist and the **`best66`** rule.

<figure><img src="../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure>

### Port 445 - SMB&#x20;

User **`j.reed`** had read/write access to the **`transitionzone$`** share on **`swim-srv`**. Leveraged these permissions by uploading a crafted LNK file to capture the NTLM hash of user **`e.ackerlund`**

<figure><img src="../.gitbook/assets/image (496).png" alt=""><figcaption></figcaption></figure>

#### Hashgrab.py repo - [https://github.com/xct/hashgrab](https://github.com/xct/hashgrab)

<figure><img src="../.gitbook/assets/image (497).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (498).png" alt=""><figcaption></figcaption></figure>

Since I was unable to crack the NTLM hash for **`e.ackerlund`**, I switched to an NTLM relay attack using **`ntlmrelayx.py`**. The target server allowed NTLM authentication relay because signing was not enforced, enabling me to relay the captured authentication and dump the domain hashes. Among the dumped hashes, I identified the NTLM hash belonging to **`m.pearson`**.

<figure><img src="../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (500).png" alt=""><figcaption></figcaption></figure>



Did a secretsdump with administrator hash and found m.pearson hash which I was able to crack with hashcat&#x20;

<figure><img src="../.gitbook/assets/image (501).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (502).png" alt=""><figcaption></figcaption></figure>

I looked through the usual privilege escalation paths but couldn't find anything useful. So I decided to check ADCS using nxc with the `-M adcs` option, which revealed the Certificate Authority information and gave me another possible attack path to investigate.

<figure><img src="../.gitbook/assets/image (503).png" alt=""><figcaption></figcaption></figure>

With local admin rights on **`SWIM-SRV.tri.lab`** via **`m.pearson`**, I used **`certipy ca -backup`** to remotely extract the **`tri-CA`**&#x63;ertificate and private key **(`tri-CA.pfx`)**. Because the domain implicitly trusts anything signed by this private key, stealing it allows me to forge valid authentication certificates for any Domain Admin offline.

#### More about Stolen CA attack - [https://www.thehacker.recipes/ad/persistence/adcs/certificate-authority#stolen-ca](https://www.thehacker.recipes/ad/persistence/adcs/certificate-authority#stolen-ca)

<figure><img src="../.gitbook/assets/image (504).png" alt=""><figcaption></figcaption></figure>

BloodHound data confirmed that j.reed\_adm is a member of the Domain Admins group. Using the stolen tri-CA.pfx private key, I forged a client authentication certificate for j.reed\_adm@tri.lab via certipy forge to impersonate the account.

<figure><img src="../.gitbook/assets/image (505).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (506).png" alt=""><figcaption></figcaption></figure>

Forging the certificate without a Certificate Revocation List (CRL) triggered a KDC\_ERROR\_CLIENT\_NOT\_TRUSTED error because the Domain Controller could not complete its PKINIT revocation check. Re-forging the certificate with the -crl flag embedded the valid domain CRL distribution point, allowing certipy auth to successfully retrieve the TGT and NT hash for j.reed\_adm.

<figure><img src="../.gitbook/assets/image (507).png" alt=""><figcaption></figcaption></figure>

With the compromised j.reed\_adm hash, I ran impacket-secretsdump against the Domain Controller to dump the NTDS database and extract the krbtgt hash.

<figure><img src="../.gitbook/assets/image (508).png" alt=""><figcaption></figcaption></figure>

