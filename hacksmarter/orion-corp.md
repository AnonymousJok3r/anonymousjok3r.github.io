# Orion Corp

## Enumeration&#x20;

### Nmap scan&#x20;

```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-23 13:38 -0400
Nmap scan report for 10.0.0.6
Host is up (0.027s latency).
Not shown: 995 filtered tcp ports (no-response)
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 5.30 seconds
                                                                                                                                                             
┌──(💀root@kali)-[/home/kali/Downloads/prac/hacksmarter/orion]
└─# nmap 10.0.0.5
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-23 13:38 -0400
Nmap scan report for 10.0.0.5
Host is up (0.028s latency).
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

```



### Port 445 - SMB&#x20;

Anonymous guest access is allowed and have read and write access on share Uploads

<figure><img src="../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

Found a README.txt file, since we have write permission, can upload hash grab files and see if we can capture any users hash

<figure><img src="../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

Used hashgrab.py, which generates lnk payload that captures hash, start the responder and upload the generated lnk file in Uploads share &#x20;

[https://github.com/xct/hashgrab ](https://github.com/xct/hashgrab)&#x20;

<figure><img src="../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

Start the responder before uploading the files to the share

```
Command:- responder -I tun0 -v 
```

<figure><img src="../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

and got hash for user b.williams, and cracked the password with john&#x20;

<figure><img src="../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

Since we obtained credentials, can get users list from ldap with module --users-export&#x20;

<figure><img src="../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>

User williams has access to share called company, but did not find anything in the share.

<figure><img src="../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

Using the credentials of b.williams, a Kerberoasting attack was executed to retrieve the password hash for the svc-onboarding service account, and hash was cracked via hashcat.

<figure><img src="../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

```
Command:- hashcat -m 13100 hashfile rockyou.txt
```

<figure><img src="../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

### Bloodhound data

BloodHound analysis revealed a critical path where svc-onboarding can force a password change on s.mitchell, who holds generic write privileges over two other user accounts. Additionally, s.mitchell can target m.white, an account that grants direct remote access to network systems.

<figure><img src="../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (184).png" alt=""><figcaption></figcaption></figure>

Changing password for user s.mitchell and abusing generic write privileges on user m.white

<figure><img src="../.gitbook/assets/image (185).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - winrm ( Initial access and user.txt)

<figure><img src="../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

Found user.txt on user m.white desktop, and in powerhshell history found cleartext password for user m.reeves, which helped to access IT shares, because m.reeves is a member of IT group

<figure><img src="../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>



### Access as m.reeves&#x20;

In folder scripts found a publish script, which contained credentials for user svc-pki

<figure><img src="../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

BloodHound data revealed that the svc-pki service account is a member of the Certificate Enrollers group, which grants it permissions to enroll in a misconfigured ESC1 certificate template. We can exploit this vulnerable template to request a certificate as any domain user, leading to immediate domain takeover.

<figure><img src="../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

Using certipy-ad, a misconfigured template vulnerable to an ESC1 attack was identified, on which the svc-pki account holds enrollment rights.&#x20;

<figure><img src="../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

### Root.txt

<figure><img src="../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>



