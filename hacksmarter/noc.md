# NOC

## Enumeration&#x20;

### Nmap scan&#x20;

```
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 10.2p1 Ubuntu 2ubuntu3.6 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.66 ((Ubuntu))
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-server-header: Apache/2.4.66 (Ubuntu)
|_http-title: Yoshiwara Data Centers | NOC Services
```

The Nmap scan revealed two open ports 22/TCP running OpenSSH 10.2p1 and 80/TCP running an Apache 2.4.66 web server titled Yoshiwara Data Centers.



### Port 80 - HTTP

Found login.php page through directory fuzzing, and tried default credentials, but those credentials did not work.

<figure><img src="../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>



### UDP scan&#x20;

UDP scan revealed that port 161 is open, which is snmp protocol&#x20;

<figure><img src="../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

Identified community monitor, and found a username called david. At the end, found another user credentials called john with cleartext password

<figure><img src="../.gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

### IDOR vulnerability to sql injection&#x20;

We see that parameter user=2 , seems like a IDOR(Insecure direct object reference) vulnerability.

<figure><img src="../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

Why make the user ID negative (-2)?If you leave the ID as 2, the database will successfully find the real user for ID 2, which is john and display it on the page, often hiding your injected numbers. By changing it to an ID that doesn't exist (like -2), you force the database query to return no results for the first part. This forces the application to display UNION SELECT placeholders and it was successful

<figure><img src="../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

Found the table name called employees&#x20;

<figure><img src="../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

Column names for table employees

<figure><img src="../.gitbook/assets/image (208).png" alt=""><figcaption></figcaption></figure>

Got the hash for user admin and john , and able to crack admin hash with hashcat&#x20;

<figure><img src="../.gitbook/assets/image (209).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

Authenticated as admin on port 80 and have an option to check systems which are running,  and it  vulnerable to command injection, can abuse this to get full terminal shell access

<figure><img src="../.gitbook/assets/image (212).png" alt=""><figcaption></figcaption></figure>



Command injection was successful and able to read /etc/passwd file&#x20;

<figure><img src="../.gitbook/assets/image (213).png" alt=""><figcaption></figcaption></figure>

earlier during enumeration phase, found that a config.php file located on the web, but was not accessible due to permissions. Abused command injection vulnerability and found cleartext password in the config.php file, and got ssh access as user david&#x20;

<figure><img src="../.gitbook/assets/image (214).png" alt=""><figcaption></figcaption></figure>

&#x20;

### SSH access as David&#x20;

```
Command:- ssh david@10.1.245.183
```

<figure><img src="../.gitbook/assets/image (215).png" alt=""><figcaption></figcaption></figure>

system has a hidden port running on port 8080 from localhost, which did not show up in the earlier nmap scan.&#x20;

<figure><img src="../.gitbook/assets/image (216).png" alt=""><figcaption></figcaption></figure>

Did a port forwarding with ssh-tunneling and got access to port 8080, which was running librenms&#x20;

```
Command:- ssh -L 3333:127.0.0.1:8080 david@10.1.245.183
```

<figure><img src="../.gitbook/assets/image (217).png" alt=""><figcaption></figcaption></figure>



### Librenms

<figure><img src="../.gitbook/assets/image (218).png" alt=""><figcaption></figcaption></figure>

Authenticated as user david

<figure><img src="../.gitbook/assets/image (219).png" alt=""><figcaption></figcaption></figure>

Found the version number in about&#x20;

<figure><img src="../.gitbook/assets/image (220).png" alt=""><figcaption></figcaption></figure>

Upon researching more found that this particular version is vulnerable to remote code execution&#x20;

[https://www.cve.org/CVERecord?id=CVE-2026-6204 ](https://www.cve.org/CVERecord?id=CVE-2026-6204)&#x20;



#### Exploit for remote code execution&#x20;

[https://projectblack.io/blog/librenms-authenticated-rce-and-xss/#binary-path-rce-poc <br>](https://projectblack.io/blog/librenms-authenticated-rce-and-xss/#binary-path-rce-poc) &#x20;

In global settings-> external-> modify the binary location of whois path to wget

<figure><img src="../.gitbook/assets/image (221).png" alt=""><figcaption></figcaption></figure>

created a small bash shell named rev.sh which has reverse shell payload and start a http.server with python in order for website to download , after that change whois path to /bin/bash to get a reverse shell access as root

<figure><img src="../.gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>



### Root.txt

<figure><img src="../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>





























