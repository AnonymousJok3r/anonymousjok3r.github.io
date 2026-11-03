# Samurai

## Enumeration&#x20;

### Nmap scan&#x20;

```
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 c3:5a:83:50:80:9a:61:37:05:b7:45:96:cb:ab:1d:1e (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDnWIbBLcbSbZZmw8nDh5DOA9ecneGMU8Ff1Rm8Frp71DcloANVhYkmErZ3+o839XNGO+k2tmXeNcwJ8jICj06M=
|   256 6b:15:12:60:1b:21:d1:bf:7e:b8:c0:e8:d7:7e:7b:6b (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIP9JIv57fNRXYSBb4BDtI+WNZG/hfJuGHaaMLL7Iu9PG
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
|_http-server-header: Apache/2.4.52 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-favicon: Unknown favicon MD5: 3E18B73692FF5A74F54EFFB2E047C8CB
|_http-title: Samurai
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=11/2%OT=22%CT=%CU=36322%PV=Y%DS=3%DC=T%G=N%TM=6AE8F50F
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=M510ST11NW7%O2=M510ST11NW7%O3=M510NNT11NW7%O4=M510ST11NW7%O5=M510ST11
OS:NW7%O6=M510ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(
OS:R=Y%DF=Y%T=40%W=F507%O=M510NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%R
OS:UD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 7.190 days (since Mon Oct 26 12:05:41 2026)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=261 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
```



### Port 80 - HTTP

I fuzzed the directories and stumbled upon /administrator, which brought up a Joomla login page. After poking around the manifest files, I managed to fingerprint the exact version: Joomla 4.2.5. This particular version is vulnerable to unauthenticated information disclosure.

<figure><img src="../.gitbook/assets/image (364).png" alt=""><figcaption></figcaption></figure>

#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2023-23752](https://nvd.nist.gov/vuln/detail/cve-2023-23752)&#x20;

Because the application doesn't properly check access rights, anyone can hit the backend web service endpoints.

```
Command:- curl -s "http://<TARGET-IP>/api/index.php/v1/config/application?public=true"

```

<figure><img src="../.gitbook/assets/image (365).png" alt=""><figcaption></figcaption></figure>

#### PoC Exploit:- [https://www.exploit-db.com/exploits/51334](https://www.exploit-db.com/exploits/51334)

After downloading the exploit via Searchsploit, I renamed it from .py to .rb since the original file was mistakenly mislabeled as Python code

<figure><img src="../.gitbook/assets/image (366).png" alt=""><figcaption></figcaption></figure>

Executing the exploit successfully leaked the database credentials and the superuser account details. Using this info, I logged right into the /administrator page with full superuser privileges.

<figure><img src="../.gitbook/assets/image (371).png" alt=""><figcaption></figcaption></figure>

Using my superuser access, I navigated to the templates area and injected a PHP reverse shell into the error.php file. After browsing to the modified page, my listener caught a reverse shell connection as www-data.

<figure><img src="../.gitbook/assets/image (372).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (373).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (374).png" alt=""><figcaption></figcaption></figure>



### User.txt

user.txt was found in /var/www/ path

<figure><img src="../.gitbook/assets/image (375).png" alt=""><figcaption></figcaption></figure>

### Privilege escalation&#x20;

Checking my sudo privileges with sudo -l revealed that www-data could execute a backup script at /opt/backup/DbMaria as root without a password. I exploited this by injecting a command to append a new root user entry (toor) directly into /etc/passwd

<figure><img src="../.gitbook/assets/image (376).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (377).png" alt=""><figcaption></figcaption></figure>



### Root.txt

<figure><img src="../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>





<br>





&#x20;&#x20;



