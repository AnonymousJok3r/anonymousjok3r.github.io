# Induction

## Enumeration

### Nmap scan

```
PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 126 Werkzeug httpd 3.1.9 (Python 3.14.8)
| http-methods: 
|_  Supported Methods: GET OPTIONS HEAD
|_http-server-header: Werkzeug/3.1.9 Python/3.14.8
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 126
3389/tcp  open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| ssl-cert: Subject: commonName=WIN-0MTGMLVOBBO
| Issuer: commonName=WIN-0MTGMLVOBBO
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-11T18:31:30
| Not valid after:  2027-04-12T18:31:30
| MD5:     aeac 10ed 6e2a 5176 02e8 64dd 9f14 5a99
| SHA-1:   f325 73e4 a23f 341a 2d3f b8ad 9d06 45e9 23ac 157c
| SHA-256: 330f 1d38 5b67 79ee e2ea 11b2 7634 eeb5 fb59 0e49 6e2c f91b 9be0 a13e d63b dbac
| -----BEGIN CERTIFICATE-----
| MIIC4jCCAcqgAwIBAgIQT1c8wB8U54VIjH3r410kTjANBgkqhkiG9w0BAQsFADAa
| MRgwFgYDVQQDEw9XSU4tME1UR01MVk9CQk8wHhcNMjYxMDExMTgzMTMwWhcNMjcw
| NDEyMTgzMTMwWjAaMRgwFgYDVQQDEw9XSU4tME1UR01MVk9CQk8wggEiMA0GCSqG
| SIb3DQEBAQUAA4IBDwAwggEKAoIBAQCk8O75sF5wybGOGWDt9RCc1XI95FnezEDj
| DbMweGp8BVCi7nW5LGbEKqaoI/OBVtgjbtHttnS7XxwZsgqJDSQegokTTuSeY8yu
| fn8UQZj7iCqc++Y2eOGFvmucM6KkxKg77kb9dCVebe33wrQJsYsx8T3saIZZkn1M
| WBnjjL6RS9kdOy5wkSXeFcDFj8hhnzrgtmXHR/wiMsGamPW//C9mpnsJEuNtFB8W
| /E5b9kcVcdhJf6rybpmu/jzX2imMYmCpza+Oeh4EdoIpufDZZeIDL3T8NJjhzIv/
| jjRUO83IDrquY1WG8/QUfOOxxtMcgwpyrIXMbRqpG/Vhc4e6pmA1AgMBAAGjJDAi
| MBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQsF
| AAOCAQEATJerAF56XTZdYXd943MjbAS14CmubcePucg73fyUDPXkOnJH0U83bZtZ
| p7rLYHwBMJqwHpqP0ATJzg2j78MZbFmTU1zzKFmL5kNDGse3XPpR1WCOq103RZA7
| RPV7eXn4G14dydIdo1/0T18n6E9BRRT4gWAKHCsZE1YPfoPfx6mhatq3uiqtCNxe
| aJq30LhjoUzVsF25hnrGIMqhin8OsHSGezZQWHiIxVjo0eWiz6jV27K4Z/9oUVev
| OJhfgvN8EKcAnbAQAUtYc7dRSRs+3HuaI4Ng2ncgQfuDW24ek/ggkLUiNvOR8P/W
| jOTCrPVla/oOvoZLCLrP729TG/V/ng==
|_-----END CERTIFICATE-----
|_ssl-date: 2026-10-26T19:00:43+00:00; 0s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: WIN-0MTGMLVOBBO
|   NetBIOS_Domain_Name: WIN-0MTGMLVOBBO
|   NetBIOS_Computer_Name: WIN-0MTGMLVOBBO
|   DNS_Domain_Name: WIN-0MTGMLVOBBO
|   DNS_Computer_Name: WIN-0MTGMLVOBBO
|   Product_Version: 10.0.20348
|_  System_Time: 2026-10-26T19:00:04+00:00
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=10/26%OT=80%CT=%CU=%PV=Y%DS=3%DC=T%G=N%TM=6ADFA35C%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=10C%TI=I%TS=A)
SEQ(SP=FF%GCD=1%ISR=107%TI=I%TS=A)
OPS(O1=M510NW8ST11%O2=M510NW8ST11%O3=M510NW8NNT11%O4=M510NW8ST11%O5=M510NW8ST11%O6=M510ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFDC)
ECN(R=Y%DF=Y%TG=80%W=FFFF%O=M510NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=N)

Uptime guess: 0.005 days (since Mon Oct 26 14:53:56 2026)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2026-10-26T19:00:06
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 62090/tcp): CLEAN (Timeout)
|   Check 2 (port 63404/tcp): CLEAN (Timeout)
|   Check 3 (port 12751/udp): CLEAN (Timeout)
|   Check 4 (port 63391/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: 0s, deviation: 0s, median: 0s

TRACEROUTE (using port 139/tcp)
HOP RTT       ADDRESS
1   145.47 ms 10.200.0.1
2   ...
3   145.82 ms 10.1.163.19

```



### Port 445 - SMB&#x20;

Discovered that anonymous guest login was enabled on the SMB server, granting read access to the fyodor\_documents\_backup share. Inside, identified two files: a PowerShell backup script and a Python script used for the web application.

<figure><img src="../.gitbook/assets/image (266).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (268).png" alt=""><figcaption></figcaption></figure>



backup.ps1 has a cleartext password, but it did not work, because the user updated it with new password.

<figure><img src="../.gitbook/assets/image (270).png" alt=""><figcaption></figcaption></figure>



### Port 80 - HTTP&#x20;

Discovered a /log directory that accepted a file path parameter, strongly indicating a Local File Inclusion (LFI) vulnerability. Exploiting this parameter allowed for arbitrary local file read across the system.

<figure><img src="../.gitbook/assets/image (271).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>

Captured the user's NTLM hash using Responder, but the hash could not be cracked via wordlist attacks.

<figure><img src="../.gitbook/assets/image (273).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (274).png" alt=""><figcaption></figcaption></figure>

Identified the path for backup.ps1 script by guessing the fodoyor\_dpcuments\_backup share name, which was accessible via anonymous guest access. Reviewing the script revealed a cleartext password. Able to authenticate the webpage via admin crednetials that are found, gained access to /run which runs powershell scripts.

<figure><img src="../.gitbook/assets/image (275).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (276).png" alt=""><figcaption></figcaption></figure>

Hosted a malicious payload.ps1 script on a local SMB share and executed it remotely via the web application. This triggered the payload to connect back, establishing a successful reverse shell.

#### Payload generated from the below website.

[https://www.revshells.com/](https://www.revshells.com/)&#x20;



<figure><img src="../.gitbook/assets/image (277).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (278).png" alt=""><figcaption></figcaption></figure>

Full terminal shell access as user fyodor on our listener

<figure><img src="../.gitbook/assets/image (279).png" alt=""><figcaption></figcaption></figure>

Ran the PrivescCheck.ps1 script and discovered a misconfigured service (tapisrv) with modifiable permissions. This allows for a privilege escalation attack by overwriting the service binary path.

<figure><img src="../.gitbook/assets/image (280).png" alt=""><figcaption></figcaption></figure>

modified binpath with powershell reverse shell payload, so that when it starts, we get escalated privilege access&#x20;

<figure><img src="../.gitbook/assets/image (281).png" alt=""><figcaption></figcaption></figure>

### Access as network service

<figure><img src="../.gitbook/assets/image (282).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

SeImpersonate is enabled and we can abuse it with tool like printspoofer to escalate our privileges to NT Authority SYSTEM&#x20;

<figure><img src="../.gitbook/assets/image (283).png" alt=""><figcaption></figcaption></figure>

Upload nc.exe and printspoofer.exe&#x20;

<figure><img src="../.gitbook/assets/image (284).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (285).png" alt=""><figcaption></figcaption></figure>

### Root.txt

<figure><img src="../.gitbook/assets/image (286).png" alt=""><figcaption></figcaption></figure>





