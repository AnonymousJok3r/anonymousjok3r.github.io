# Lumon

## Enumeration&#x20;

### Nmap scan&#x20;

```
Domain scan-
Open 10.1.17.185:53
Open 10.1.17.185:88
Open 10.1.17.185:135
Open 10.1.17.185:139
Open 10.1.17.185:389
Open 10.1.17.185:445
Open 10.1.17.185:464
Open 10.1.17.185:593
Open 10.1.17.185:636
Open 10.1.17.185:3268
Open 10.1.17.185:3269
Open 10.1.17.185:3389
Open 10.1.17.185:5985
Open 10.1.17.185:9389
Open 10.1.17.185:49664
Open 10.1.17.185:49668
Open 10.1.17.185:49667
Open 10.1.17.185:49669
Open 10.1.17.185:49673
Open 10.1.17.185:49671
Open 10.1.17.185:49692
Open 10.1.17.185:49706
Open 10.1.17.185:49716
Open 10.1.17.185:49751
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -A" on ip 10.1.17.185

 
 
 
 
Intranet scan 
nmap 10.1.85.113                                       
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-21 11:38 -0400
Nmap scan report for 10.1.85.113
Host is up (0.029s latency).
Not shown: 993 filtered tcp ports (no-response)
PORT     STATE SERVICE
80/tcp   open  http
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
5985/tcp open  wsman




```

### Assumed breached credentials&#x20;

```
hellyr:H3lenaR!2025
```

### Port 445 - SMB&#x20;

Copying users list with rid-brute from nxc to a users.txt file

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

hellyr has read and write option on share MDRepo&#x20;

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

MDRepo share contains 2 files, download both of them.

```
Command:- mget *
```

<figure><img src="../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

Both files mentioned about another web service running, and how to interact with it&#x20;

<figure><img src="../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

In order to access the webpage, need to add in the hosts file

<figure><img src="../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

Since we have write permissions on the share, we can capture the hash, with the help of ntlm\_theft.py generated files, before uploading them start responder to caputre the hash

<figure><img src="../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

Got hash for user harmonyc

<figure><img src="../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

hash cracking with john the ripper on NTLMv2 hash

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>



### Port 443 - HTTPS&#x20;

Authenticated as harmonyc, and found admin panel

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

There is a browse file share option, tried to capture the hash by providing it with my ip address, and got intranetsvc user hash on smbserver.py&#x20;

<figure><img src="../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

Cracked the NTLMv2 hash of intranetsvc with john the ripper&#x20;

<figure><img src="../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

### Bloodhound-python

Bloodhound data enumeration revealed that user intranetsvc has forcechange password on 6 users and user marks and peterk are members of laps admin, Can abuse this privileges because laps admin group memebers can read passwords of local administrators

<figure><img src="../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

Changing password for user marks and peterk with rpcclient, and this lead to initial access on port 5985

<figure><img src="../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - Winrm (Initial Access - user.txt)

<figure><img src="../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

Since marks is a member of laps admin, we can then try to read the LAPS password of the computer account i.e. the password of the computer's local administrator.

<figure><img src="../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

### Port 389 - RDP

local admin credentials are valid on port 389&#x20;

<figure><img src="../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

In order to get better shell access and run any commands, open the command prompt and run it as administrator, so that we add user marks to administrators group.&#x20;

<figure><img src="../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>

Since marks is member of administrators, do a secretsdump to get the hash of domain admin users like hellye&#x20;

<figure><img src="../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

Cracked the hash with hashcat and got cleartext password for user hellye&#x20;

<figure><img src="../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>



### Root.txt

<figure><img src="../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>





