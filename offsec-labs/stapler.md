# Stapler

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT      STATE SERVICE     REASON         VERSION
21/tcp    open  ftp         syn-ack ttl 61 vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 550 Permission denied.
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.45.169
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp    open  ssh         syn-ack ttl 61 OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4c:0d:74:66:95:2b:59:ce:14:91:a3:2b:35:2f:01:6a (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5cWUdrQWkc6jCBD6B+B84kq6RPLXBjvGmtUW+NXet639MMwaSpWoYqlpfzxQApKibolx3/ZU1ShNEuYlY2Bo0wms962C+qMn5nu1c9JSxmUE4a8KEOAX3JNYFYB/TtopqHKNKENNvOrTAgtIx+CitDyUtv6RgQNhrsNjUrxqxjh758zoS2qBX9+63IFfyOj/B07HCOW0b0Mv9L3m+iJUHJI3xf1F4l2Ewv+oC04SR6BzNQ/NLjSGDQNtNyc3zf1dEkHpEq003xlYSkb0etz6fAxAHk3/DFQ2yDr7efEhBnbmFBxbqzgwbcUE532Ip91jAGo3gF/3T0OJcLiLSRW+r
|   256 0d:5d:38:6f:82:fb:bd:7b:03:d9:b6:d5:b0:80:e5:85 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAAF3/+7soHTVHlXnJiGtIf6D2JW8x8Vr7D/yqcrMZdM6jqgc4fotkCOIMByxQ1rsfci37Z4yndLdcn/SesnnhM=
|   256 8e:59:e3:3d:16:74:66:f3:a2:61:61:f1:bb:0a:e6:90 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMnkhanxt5rW0dX/qX6ZyrN61Z7E+M2Hrqsv0WE56Otw
53/tcp    open  tcpwrapped  syn-ack ttl 61
80/tcp    open  http        syn-ack ttl 61 PHP cli server 5.5 or later
|_http-title: 404 Not Found
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
139/tcp   open  netbios-ssn syn-ack ttl 61 Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
666/tcp   open  pkzip-file  syn-ack ttl 61 .ZIP file
| fingerprint-strings: 
|   NULL: 
|     message2.jpgUT 
|     QWux
|     "DL[E
|     #;3[
|     \xf6
|     u([r
|     qYQq
|     Y_?n2
|     3&M~{
|     9-a)T
|     L}AJ
|_    .npy.9
3306/tcp  open  mysql       syn-ack ttl 61 MySQL 5.7.33-0ubuntu0.16.04.1
| ssl-cert: Subject: commonName=MySQL_Server_5.7.33_Auto_Generated_Server_Certificate
| Issuer: commonName=MySQL_Server_5.7.33_Auto_Generated_CA_Certificate
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-11-17T16:15:04
| Not valid after:  2036-11-14T16:15:04
| MD5:     3e7e 3356 d1ea d705 3919 f204 0391 70b5
| SHA-1:   6e60 9657 49a4 dc72 4024 d2cf cb1c 2c95 e3b9 aa78
| SHA-256: 1199 6586 afd1 e21e 2602 616c c8af 1bf3 fd73 cde7 1dcd 4d90 37ec 874c 7547 6566
| -----BEGIN CERTIFICATE-----
| MIIDBzCCAe+gAwIBAgIBAjANBgkqhkiG9w0BAQsFADA8MTowOAYDVQQDDDFNeVNR
| TF9TZXJ2ZXJfNS43LjMzX0F1dG9fR2VuZXJhdGVkX0NBX0NlcnRpZmljYXRlMB4X
| DTI2MTExNzE2MTUwNFoXDTM2MTExNDE2MTUwNFowQDE+MDwGA1UEAww1TXlTUUxf
| U2VydmVyXzUuNy4zM19BdXRvX0dlbmVyYXRlZF9TZXJ2ZXJfQ2VydGlmaWNhdGUw
| ggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC36jCdp4FjherO7zuwRIgV
| RNf/DNQk0gBVWqur2eVHhX5NW8Ct01E5XQnkMbXGakcTQMEVWzTTlv9alvEztJiZ
| Lz+j50KyVE8m0jZ8lfBhUURJoQQXsNlq/6wGXNkuAklZDz1IvFzZDBzTMq8K0itG
| AOwVsEg9PbxBnQRcMKHpGVB+9zcEzz1aS7ChWKQfSTs7ToMfk6NrOe7IMqejFqjY
| cRUhHnuYpX/cvOGhZ6PWVhh81eI68wB98y/Fb7+svufLOrB2E1fiaoXIvhsIjmR0
| eQ9K7pbtB4Hm7dinnuCicQDCLraR/JnJb7DWdJURFW5zanU/beGzQLc+rRcqzXAN
| AgMBAAGjEDAOMAwGA1UdEwEB/wQCMAAwDQYJKoZIhvcNAQELBQADggEBALgHaWap
| tPSpivL2GxEVhRupC+5u7hjwLaPV8FCJnLHHBbWHFjf3kPmU3p6m9xVPyUn+BiLp
| S0xdkgh6EejD7OPV6tep5Zi4GcIzcJOcEawhYqsPmS21Nini8UJCMuDxttVOXYCK
| SOho5UBgQMIKxcO025+UwjnzQEHBsPY+5LF6s/u4/ecVyc9OBwUEh5rVg9GUGIl+
| yCuwpscZiStZXpURd6aGKXZIy1X1Z3QmfgQBQQsPWSGdwCt6ztw1uEP+2VtItjGj
| iYIQz/u1ZXJPXNW4vUIJ774i0q3Pu+NqzxrIln0o235CZLbXFuVaiyoy0EhZR9vj
| uzHcowpwEWJYiQc=
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
| mysql-info: 
|   Protocol: 10
|   Version: 5.7.33-0ubuntu0.16.04.1
|   Thread ID: 6
|   Capabilities flags: 65535
|   Some Capabilities: FoundRows, Support41Auth, ODBCClient, InteractiveClient, Speaks41ProtocolNew, Speaks41ProtocolOld, SupportsCompression, LongColumnFlag, IgnoreSigpipes, SupportsTransactions, LongPassword, ConnectWithDatabase, SwitchToSSLAfterHandshake, IgnoreSpaceBeforeParenthesis, SupportsLoadDataLocal, DontAllowDatabaseTableColumn, SupportsMultipleStatments, SupportsAuthPlugins, SupportsMultipleResults
|   Status: Autocommit
|   Salt: wc\x05p+ 2D\x11\x03 >>/&W]7.	
|_  Auth Plugin Name: mysql_native_password
12380/tcp open  http        syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: POST OPTIONS GET HEAD
|_http-title: Tim, we need to-do better next year for Initech
|_http-server-header: Apache/2.4.18 (Ubuntu)
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port666-TCP:V=7.99%I=7%D=11/17%Time=6AFC7EEA%P=x86_64-pc-linux-gnu%r(NU
SF:LL,179C,"PK\x03\x04\x14\0\x02\0\x08\0d\x80\xc3Hp\xdf\x15\x81\xaa,\0\0\x
SF:152\0\0\x0c\0\x1c\0message2\.jpgUT\t\0\x03\+\x9cQWJ\x9cQWux\x0b\0\x01\x
SF:04\xf5\x01\0\0\x04\x14\0\0\0\xadz\x0bT\x13\xe7\xbe\xefP\x94\x88\x88A@\x
SF:a2\x20\x19\xabUT\xc4T\x11\xa9\x102>\x8a\xd4RDK\x15\x85Jj\xa9\"DL\[E\xa2
SF:\x0c\x19\x140<\xc4\xb4\xb5\xca\xaen\x89\x8a\x8aV\x11\x91W\xc5H\x20\x0f\
SF:xb2\xf7\xb6\x88\n\x82@%\x99d\xb7\xc8#;3\[\r_\xcddr\x87\xbd\xcf9\xf7\xae
SF:u\xeeY\xeb\xdc\xb3oX\xacY\xf92\xf3e\xfe\xdf\xff\xff\xff=2\x9f\xf3\x99\x
SF:d3\x08y}\xb8a\xe3\x06\xc8\xc5\x05\x82>`\xfe\x20\xa7\x05:\xb4y\xaf\xf8\x
SF:a0\xf8\xc0\^\xf1\x97sC\x97\xbd\x0b\xbd\xb7nc\xdc\xa4I\xd0\xc4\+j\xce\[\
SF:x87\xa0\xe5\x1b\xf7\xcc=,\xce\x9a\xbb\xeb\xeb\xdds\xbf\xde\xbd\xeb\x8b\
SF:xf4\xfdis\x0f\xeeM\?\xb0\xf4\x1f\xa3\xcceY\xfb\xbe\x98\x9b\xb6\xfb\xe0\
SF:xdc\]sS\xc5bQ\xfa\xee\xb7\xe7\xbc\x05AoA\x93\xfe9\xd3\x82\x7f\xcc\xe4\x
SF:d5\x1dx\xa2O\x0e\xdd\x994\x9c\xe7\xfe\x871\xb0N\xea\x1c\x80\xd63w\xf1\x
SF:af\xbd&&q\xf9\x97'i\x85fL\x81\xe2\\\xf6\xb9\xba\xcc\x80\xde\x9a\xe1\xe2
SF::\xc3\xc5\xa9\x85`\x08r\x99\xfc\xcf\x13\xa0\x7f{\xb9\xbc\xe5:i\xb2\x1bk
SF:\x8a\xfbT\x0f\xe6\x84\x06/\xe8-\x17W\xd7\xb7&\xb9N\x9e<\xb1\\\.\xb9\xcc
SF:\xe7\xd0\xa4\x19\x93\xbd\xdf\^\xbe\xd6\xcdg\xcb\.\xd6\xbc\xaf\|W\x1c\xf
SF:d\xf6\xe2\x94\xf9\xebj\xdbf~\xfc\x98x'\xf4\xf3\xaf\x8f\xb9O\xf5\xe3\xcc
SF:\x9a\xed\xbf`a\xd0\xa2\xc5KV\x86\xad\n\x7fou\xc4\xfa\xf7\xa37\xc4\|\xb0
SF:\xf1\xc3\x84O\xb6nK\xdc\xbe#\)\xf5\x8b\xdd{\xd2\xf6\xa6g\x1c8\x98u\(\[r
SF:\xf8H~A\xe1qYQq\xc9w\xa7\xbe\?}\xa6\xfc\x0f\?\x9c\xbdTy\xf9\xca\xd5\xaa
SF:k\xd7\x7f\xbcSW\xdf\xd0\xd8\xf4\xd3\xddf\xb5F\xabk\xd7\xff\xe9\xcf\x7fy
SF:\xd2\xd5\xfd\xb4\xa7\xf7Y_\?n2\xff\xf5\xd7\xdf\x86\^\x0c\x8f\x90\x7f\x7
SF:f\xf9\xea\xb5m\x1c\xfc\xfef\"\.\x17\xc8\xf5\?B\xff\xbf\xc6\xc5,\x82\xcb
SF:\[\x93&\xb9NbM\xc4\xe5\xf2V\xf6\xc4\t3&M~{\xb9\x9b\xf7\xda-\xac\]_\xf9\
SF:xcc\[qt\x8a\xef\xbao/\xd6\xb6\xb9\xcf\x0f\xfd\x98\x98\xf9\xf9\xd7\x8f\x
SF:a7\xfa\xbd\xb3\x12_@N\x84\xf6\x8f\xc8\xfe{\x81\x1d\xfb\x1fE\xf6\x1f\x81
SF:\xfd\xef\xb8\xfa\xa1i\xae\.L\xf2\\g@\x08D\xbb\xbfp\xb5\xd4\xf4Ym\x0bI\x
SF:96\x1e\xcb\x879-a\)T\x02\xc8\$\x14k\x08\xae\xfcZ\x90\xe6E\xcb<C\xcap\x8
SF:f\xd0\x8f\x9fu\x01\x8dvT\xf0'\x9b\xe4ST%\x9f5\x95\xab\rSWb\xecN\xfb&\xf
SF:4\xed\xe3v\x13O\xb73A#\xf0,\xd5\xc2\^\xe8\xfc\xc0\xa7\xaf\xab4\xcfC\xcd
SF:\x88\x8e}\xac\x15\xf6~\xc4R\x8e`wT\x96\xa8KT\x1cam\xdb\x99f\xfb\n\xbc\x
SF:bcL}AJ\xe5H\x912\x88\(O\0k\xc9\xa9\x1a\x93\xb8\x84\x8fdN\xbf\x17\xf5\xf
SF:0\.npy\.9\x04\xcf\x14\x1d\x89Rr9\xe4\xd2\xae\x91#\xfbOg\xed\xf6\x15\x04
SF:\xf6~\xf1\]V\xdcBGu\xeb\xaa=\x8e\xef\xa4HU\x1e\x8f\x9f\x9bI\xf4\xb6GTQ\
SF:xf3\xe9\xe5\x8e\x0b\x14L\xb2\xda\x92\x12\xf3\x95\xa2\x1c\xb3\x13\*P\x11
SF:\?\xfb\xf3\xda\xcaDfv\x89`\xa9\xe4k\xc4S\x0e\xd6P0");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (93%), Linux 3.10 - 4.11 (93%), Linux 3.13 - 4.4 (93%), Linux 3.8 - 3.16 (93%), Linux 3.2 - 4.14 (93%), Linux 2.6.32 - 3.10 (92%), Linux 4.4 (92%), Linux 2.6.32 (89%), Linux 3.18 (89%), Linux 2.6.32 - 3.5 (89%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/17%OT=21%CT=%CU=33673%PV=Y%DS=4%DC=T%G=N%TM=6AFC7F19%P=x86_64-pc-linux-gnu)
SEQ(SP=103%GCD=1%ISR=106%TI=Z%TS=8)
SEQ(SP=FE%GCD=1%ISR=10D%TI=Z%TS=8)
OPS(O1=M540ST11NW7%O2=M540ST11NW7%O3=M540NNT11NW7%O4=M540ST11NW7%O5=M540ST11NW7%O6=M540ST11)
WIN(W1=6810%W2=6810%W3=6810%W4=6810%W5=6810%W6=6810)
ECN(R=Y%DF=Y%T=40%W=6900%O=M540NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=N)

Uptime guess: 0.009 days (since Tue Nov 17 11:08:16 2026)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=259 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Host: LAB-PG-UBUNTU16-STAPLER-245-173; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: \x00
|   NetBIOS computer name: LAB-PG-UBUNTU16-STAPLER-245-173\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2026-11-17T16:21:15+00:00
|_clock-skew: mean: 0s, deviation: 1s, median: -1s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2026-11-17T16:21:19
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 23233/tcp): CLEAN (Timeout)
|   Check 2 (port 23733/tcp): CLEAN (Timeout)
|   Check 3 (port 23464/udp): CLEAN (Failed to receive data)
|   Check 4 (port 50248/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   19.21 ms 192.168.45.1
2   19.04 ms 192.168.45.254
3   19.19 ms 192.168.251.1
4   19.42 ms 192.168.223.148
```

### Port 21 - FTP&#x20;

Anonymous login is allowed and found a file named note&#x20;

<figure><img src="../.gitbook/assets/image (605).png" alt=""><figcaption></figcaption></figure>

Found a couple valid user names called elly, john and harry

<figure><img src="../.gitbook/assets/image (606).png" alt=""><figcaption></figcaption></figure>

Using the enumerated `users` list, I ran Hydra against the FTP service with the `-e nsr` flag  to test for null, matching, or reversed username passwords. This successfully uncovered valid FTP credentials for the user **`elly`**&#x20;

```
Command:- hydra -L users -e nsr ftp://IP
```

<figure><img src="../.gitbook/assets/image (608).png" alt=""><figcaption></figcaption></figure>

Logging into the FTP server with `elly`'s credentials gave me access to the `passwd` file, where I extracted an expanded list of system usernames. Running Hydra again with the `-e nsr` flag against the SSH service uncovered valid credentials for **`SHayslett`**, granting me initial shell access.

<figure><img src="../.gitbook/assets/image (609).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (610).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (613).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH

<figure><img src="../.gitbook/assets/image (614).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation&#x20;

Checking the `.bash_history` files across all user directories revealed plaintext credentials for two additional users, including **`peter`**. Upon switching to `peter`, I discovered a `sudo` misconfiguration allowing him to run any command as `root`, which gave me full root access to the machine.

```
Command:- cat */.bash_history
```

<figure><img src="../.gitbook/assets/image (615).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (616).png" alt=""><figcaption></figcaption></figure>

