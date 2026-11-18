# DC-1

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT      STATE SERVICE REASON         VERSION
22/tcp    open  ssh     syn-ack ttl 61 OpenSSH 6.0p1 Debian 4+deb7u7 (protocol 2.0)
| ssh-hostkey: 
|   1024 c4:d6:59:e6:77:4c:22:7a:96:16:60:67:8b:42:48:8f (DSA)
| ssh-dss AAAAB3NzaC1kc3MAAACBAI1NiSeZ5dkSttUT5BvkRgdQ0Ll7uF//UJCPnySOrC1vg62DWq/Dn1ktunFd09FT5Nm/ZP9BHlaW5hftzUdtYUQRKfazWfs6g5glPJQSVUqnlNwVUBA46qS65p4hXHkkl5QO0OHzs8dovwe3e+doYiHTRZ9nnlNGbkrg7yRFQLKPAAAAFQC5qj0MICUmhO3Gj+VCqf3aHsiRdQAAAIAoVp13EkVwBtQQJnS5mY4vPR5A9kK3DqAQmj4XP1GAn16r9rSLUFffz/ONrDWflFrmoPbxzRhpgNpHx9hZpyobSyOkEU3b/hnE/hdq3dygHLZ3adaFIdNVG4U8P9ZHuVUk0vHvsu2qYt5MJs0k1A+pXKFc9n06/DEU0rnNo+mMKwAAAIA/Y//BwzC2IlByd7g7eQiXgZC2pGE4RgO1pQCNo9IM4ZkV1MxH3/WVCdi27fjAbLQ+32cGIzjsgFhzFoJ+vfSYZTI+avqU0N86qT+mDCGCSeyAbOoNq52WtzWId1mqDoOzu7qG52HarRmxQlvbmtifYYTZCJWJcYla2GAsqUGFHw==
|   2048 11:82:fe:53:4e:dc:5b:32:7f:44:64:82:75:7d:d0:a0 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCbDC/6BDEUIa7NP87jp5dQh/rJpDQz5JBGpFRHXa+jb5aEd/SgvWKIlMjUDoeIMjdzmsNhwCRYAoY7Qq2OrrRh2kIvQipyohWB8nImetQe52QG6+LHDKXiiEFJRHg9AtsgE2Mt9RAg2RvSlXfGbWXgobiKw3RqpFtk/gK66C0SJE4MkKZcQNNQeC5dzYtVQqfNh9uUb1FjQpvpEkOnCmiTqFxlqzHp/T1AKZ4RKED/ShumJcQknNe/WOD1ypeDeR+BUixiIoq+fR+grQB9GC3TcpWYI0IrC5ESe3mSyeHmR8yYTVIgbIN5RgEiOggWpeIPXgajILPkHThWdXf70fiv
|   256 3d:aa:98:5c:87:af:ea:84:b8:23:68:8d:b9:05:5f:d8 (ECDSA)
|_ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBKUNN60T4EOFHGiGdFU1ljvBlREaVWgZvgWlkhSKutr8l75VBlGbgTaFBcTzWrPdRItKooYsejeC80l5nEnKkNU=
80/tcp    open  http    syn-ack ttl 61 Apache httpd 2.2.22 ((Debian))
|_http-favicon: Unknown favicon MD5: B6341DFC213100C61DB4FB8775878CEC
| http-robots.txt: 36 disallowed entries 
| /includes/ /misc/ /modules/ /profiles/ /scripts/ 
| /themes/ /CHANGELOG.txt /cron.php /INSTALL.mysql.txt 
| /INSTALL.pgsql.txt /INSTALL.sqlite.txt /install.php /INSTALL.txt 
| /LICENSE.txt /MAINTAINERS.txt /update.php /UPGRADE.txt /xmlrpc.php 
| /admin/ /comment/reply/ /filter/tips/ /node/add/ /search/ 
| /user/register/ /user/password/ /user/login/ /user/logout/ /?q=admin/ 
| /?q=comment/reply/ /?q=filter/tips/ /?q=node/add/ /?q=search/ 
|_/?q=user/password/ /?q=user/register/ /?q=user/login/ /?q=user/logout/
|_http-title: Welcome to Drupal Site | Drupal Site
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.2.22 (Debian)
|_http-generator: Drupal 7 (http://drupal.org)
111/tcp   open  rpcbind syn-ack ttl 61 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          41274/tcp6  status
|   100024  1          41720/tcp   status
|   100024  1          49941/udp6  status
|_  100024  1          54030/udp   status
41720/tcp open  status  syn-ack ttl 61 1 (RPC #100024)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (98%), Linux 2.6.32 - 3.10 (98%), Linux 3.10 - 4.11 (96%), Linux 3.2 - 4.14 (96%), Linux 3.2 (95%), Linux 3.2 - 3.10 (95%), Linux 3.2 - 3.16 (95%), Linux 3.2 - 3.8 (95%), XBMCbuntu Frodo v12.2 (Linux 3.X) (95%), Olivetti 65C-9 printer (95%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/17%OT=22%CT=%CU=34622%PV=Y%DS=4%DC=T%G=N%TM=6AFC9F3D%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=10C%TI=Z%CI=I%II=I%TS=8)
SEQ(SP=FB%GCD=1%ISR=105%TI=Z%CI=I%II=I%TS=8)
OPS(O1=M578ST11NW4%O2=M578ST11NW4%O3=M578NNT11NW4%O4=M578ST11NW4%O5=M578ST11NW4%O6=M578ST11)
WIN(W1=3890%W2=3890%W3=3890%W4=3890%W5=3890%W6=3890)
ECN(R=Y%DF=Y%T=40%W=3908%O=M578NNSNW4%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 198.048 days (since Sun May  3 13:29:15 2026)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=251 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 111/tcp)
HOP RTT      ADDRESS
1   14.54 ms 192.168.45.1
2   14.51 ms 192.168.45.254
3   14.58 ms 192.168.251.1
4   14.67 ms 192.168.106.193
```

### Port 80 - HTTP

Enumeration revealed the target was running an outdated instance of **Drupal 7**, which is vulnerable to remote code execution. Leveraging a public exploit script against the web application allowed me to execute arbitrary commands and gain an initial shell on the server.

#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2018-7600](https://nvd.nist.gov/vuln/detail/cve-2018-7600)

<figure><img src="../.gitbook/assets/image (617).png" alt=""><figcaption></figcaption></figure>

#### PoC rce for drupal 7 - [https://www.exploit-db.com/exploits/44449](https://www.exploit-db.com/exploits/44449)

<figure><img src="../.gitbook/assets/image (618).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (619).png" alt=""><figcaption></figcaption></figure>

did a nc command for a stable full terminal shell access&#x20;

<figure><img src="../.gitbook/assets/image (620).png" alt=""><figcaption></figcaption></figure>

Found local.txt in /home directory

<figure><img src="../.gitbook/assets/image (621).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation&#x20;

I searched for SUID binaries and discovered that /usr/bin/find had the SUID bit set. Leveraging its -exec flag allowed me to execute commands as root and obtain a root shell.

<figure><img src="../.gitbook/assets/image (622).png" alt=""><figcaption></figcaption></figure>

#### PoC for find - [https://gtfobins.org/gtfobins/find/](https://gtfobins.org/gtfobins/find/)&#x20;

<figure><img src="../.gitbook/assets/image (623).png" alt=""><figcaption></figcaption></figure>

