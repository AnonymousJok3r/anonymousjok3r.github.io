# New Hire

## Enumeration&#x20;

### Nmap scan&#x20;

```

PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 126
3389/tcp  open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| ssl-cert: Subject: commonName=WIN-0MTGMLVOBBO
| Issuer: commonName=WIN-0MTGMLVOBBO
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-08-29T19:25:58
| Not valid after:  2027-02-28T19:25:58
| MD5:     c39e d38e 37eb 4466 089b 4795 fc90 dabc
| SHA-1:   f207 146c 2797 cc64 6189 fc58 07ff 3823 bea7 06db
| SHA-256: ed2f d5f1 fb1b 1193 7e3c 008f b5b4 2c2f f69d 2f7c 0e52 31d3 c135 7415 d799 3806
| -----BEGIN CERTIFICATE-----
| MIIC4jCCAcqgAwIBAgIQM2WaS7IG0JRNzqygLJly1zANBgkqhkiG9w0BAQsFADAa
| MRgwFgYDVQQDEw9XSU4tME1UR01MVk9CQk8wHhcNMjYwODI5MTkyNTU4WhcNMjcw
| MjI4MTkyNTU4WjAaMRgwFgYDVQQDEw9XSU4tME1UR01MVk9CQk8wggEiMA0GCSqG
| SIb3DQEBAQUAA4IBDwAwggEKAoIBAQDHvX2Pg0upmN5uiRYQyHfuTPPWPxt6yK2d
| f2Z+ClYMm/vZ+rgKrLOcfFl5L6hRZmhULfo/haWGZZ9mFdQCdLfEOW9S6lQ+hODu
| VOkDVXYclVF8SJQzQybrRocWDb8CTI1oJOMSo5870XItvaAKSCHtbFnOWBI9nivr
| wSDrcFFu/DR97QbUPBdjQp84CWmV7cmCX5dTubvFxRN2fur4gE0zH37qEgOlYtTU
| czLhtFesvsRa5mJsVeXT8yUf/uA98iKNH1geFo9GxBXUVxuHH9br/aJmkk0K1dcP
| M9EVU3SUQoF7p/TnbBV/DyFERycjK9vOKbWLV2C2w/DNunYsqYGtAgMBAAGjJDAi
| MBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQsF
| AAOCAQEAQAlzR737ucY37+9owMbk/CBCyre6OcW/3vKL8O8vQccr2I5ONZqr9grJ
| tDU45PxkztLJ4Qpc/T8Kxu6isono5gPVIJo8g1rGmwQ+RBTeVEejoPcBMxoff9Yl
| B3zOOVRXp9Tz4aiBAVNor6Rv07KAzb51TbYu+XZxlue/meBv2ZBP3q/HbQYMu9Ou
| gC26QHQrOfy/u2NenqQr2EtPLASqVlKmiIQTUvSKpXzn6GampLCFO+mmDRWITj6m
| YDa3c90zDNw5lLhClnyFf4eRcXNfjxI/hkyZ0Kl8xwxtix9RGXU+1dGLFYVxmv29
| T/5fe5K1nkZ+XQynyDEsUe2X+UH33g==
|_-----END CERTIFICATE-----
|_ssl-date: 2026-11-06T19:41:40+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: WIN-0MTGMLVOBBO
|   NetBIOS_Domain_Name: WIN-0MTGMLVOBBO
|   NetBIOS_Computer_Name: WIN-0MTGMLVOBBO
|   DNS_Domain_Name: WIN-0MTGMLVOBBO
|   DNS_Computer_Name: WIN-0MTGMLVOBBO
|   Product_Version: 10.0.20348
|_  System_Time: 2026-11-06T19:41:00+00:00
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49669/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/6%OT=135%CT=%CU=%PV=Y%DS=3%DC=T%G=N%TM=6AEE2D76%P=x86_64-pc-linux-gnu)
SEQ(SP=107%GCD=1%ISR=109%TI=I%TS=A)
SEQ(SP=108%GCD=1%ISR=10C%TI=I%TS=A)
OPS(O1=M510NW8ST11%O2=M510NW8ST11%O3=M510NW8NNT11%O4=M510NW8ST11%O5=M510NW8ST11%O6=M510ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFDC)
ECN(R=Y%DF=Y%TG=80%W=FFFF%O=M510NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%TG=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=N)
U1(R=N)
IE(R=N)

Uptime guess: 0.007 days (since Fri Nov  6 14:31:21 2026)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=263 (Good luck!)
IP ID Sequence Generation: Incremental
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2026-11-06T19:41:03
|_  start_date: N/A
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 43297/tcp): CLEAN (Timeout)
|   Check 2 (port 51520/tcp): CLEAN (Timeout)
|   Check 3 (port 63345/udp): CLEAN (Timeout)
|   Check 4 (port 63461/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: mean: -1s, deviation: 0s, median: -2s
```

### Port 445 - SMB&#x20;

An anonymous SMB login allowed unauthenticated read access to the HR network share. This misconfiguration made it possible to list and download sensitive files directly from the server without credentials.

<figure><img src="../.gitbook/assets/image (390).png" alt=""><figcaption></figcaption></figure>

Found temporary password employees.eml file

<figure><img src="../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure>

I ran a rid-brute scan against the target and managed to dump a clean list of valid usernames.

<figure><img src="../.gitbook/assets/image (392).png" alt=""><figcaption></figcaption></figure>

I took that user list and ran a quick password spray for standard temporary passwords. Turns out, two accounts were still using their defaults, which let me right into the system

<figure><img src="../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure>

User tim.torner has read access to an IT share containing a database.kdb file. I downloaded it, ran keepass2john to get the hash, cracked the master password, and found fred.green's cleartext password sitting right inside.&#x20;

<figure><img src="../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (395).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (396).png" alt=""><figcaption></figcaption></figure>



cracking the password with john&#x20;

<figure><img src="../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>



Imported the kdb file using the import feature which was located in Database

<figure><img src="../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>



Fred.green credentials are valid and able to authenticate as him on port 5985

<figure><img src="../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - Winrm (user.txt)

<figure><img src="../.gitbook/assets/image (400).png" alt=""><figcaption></figcaption></figure>

During internal enumeration, I discovered an MSSQL service listening locally on port 1433. Since this wasn't exposed externally during the initial Nmap scan, I used Chisel to set up a port forward, allowing me to access the database from my local machine.

<figure><img src="../.gitbook/assets/image (401).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (403).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (404).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

Using fred.green's credentials to authenticate to the MSSQL instance, I checked for impersonation privileges using enum\_impersonate. The output showed that the account had permission to impersonate the sysadmin (sa) user. I executed exec\_as\_login sa, and verifying with SELECT USER\_NAME(); confirmed that I successfully escalated my privileges to database owner (dbo).

<figure><img src="../.gitbook/assets/image (405).png" alt=""><figcaption></figcaption></figure>

```
Command: enable_xp_cmdshell
```

With sa privileges, I used xp\_cmdshell to execute a PowerShell reverse shell one-liner back to my attack machine

<figure><img src="../.gitbook/assets/image (406).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (407).png" alt=""><figcaption></figcaption></figure>

I found an ssh.lnk file, copied it to C:\ProgramData, and downloaded it to my local machine using fred.green's WinRM access

<figure><img src="../.gitbook/assets/image (408).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (409).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (410).png" alt=""><figcaption></figcaption></figure>

Inspecting the .lnk file revealed a cleartext password for the administrator user. Running a quick password spray with it showed that the same password was reused for the sysadmin account.

<figure><img src="../.gitbook/assets/image (411).png" alt=""><figcaption></figcaption></figure>

### sysadmin password

<figure><img src="../.gitbook/assets/image (412).png" alt=""><figcaption></figcaption></figure>





