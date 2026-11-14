# BBSCute

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 22:21:9c:39:c8:9d:9c:f5:62:05:2e:b1:62:3e:78:9d (RSA)
|   256 d9:09:1d:e1:5d:97:1a:83:fc:ed:e6:41:df:8b:a5:8a (ECDSA)
|_  256 ab:90:2f:4f:13:0d:f9:da:dd:da:67:6c:21:4e:44:9d (ED25519)
80/tcp  open  http     Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Apache2 Debian Default Page: It works
88/tcp  open  http     nginx 1.14.2
|_http-server-header: nginx/1.14.2
|_http-title: 404 Not Found
110/tcp open  pop3     Courier pop3d
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: UTF8(USER) IMPLEMENTATION(Courier Mail Server) PIPELINING USER STLS TOP UIDL LOGIN-DELAY(10)
| ssl-cert: Subject: commonName=localhost/organizationName=Courier Mail Server/stateOrProvinceName=NY/countryName=US
| Subject Alternative Name: email:postmaster@example.com
| Not valid before: 2020-09-17T16:28:06
|_Not valid after:  2021-09-17T16:28:06
995/tcp open  ssl/pop3 Courier pop3d
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: UTF8(USER) IMPLEMENTATION(Courier Mail Server) USER LOGIN-DELAY(10) TOP UIDL PIPELINING
| ssl-cert: Subject: commonName=localhost/organizationName=Courier Mail Server/stateOrProvinceName=NY/countryName=US
| Subject Alternative Name: email:postmaster@example.com
| Not valid before: 2020-09-17T16:28:06
|_Not valid after:  2021-09-17T16:28:06
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```



### Port 80 - HTTP

During initial web enumeration, directory brute-forcing uncovered a `/migration` and also `index.php` endpoint on the target server

<figure><img src="../.gitbook/assets/image (542).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (543).png" alt=""><figcaption></figcaption></figure>

Inspecting the `/migration` directory revealed a PHP file. Accessing this endpoint in the browser confirmed the target was running an instance of CuteNews

<figure><img src="../.gitbook/assets/image (544).png" alt=""><figcaption></figcaption></figure>

Reveals information about cutenews 2.0.3 to 2.0.4

<figure><img src="../.gitbook/assets/image (545).png" alt=""><figcaption></figcaption></figure>

Inspecting `index.php` revealed that the application was running **CuteNews version 2.1.2**. With the exact software version identified, I began searching for known public vulnerabilities affecting this release

<figure><img src="../.gitbook/assets/image (546).png" alt=""><figcaption></figcaption></figure>

Found exploits on searchsploit&#x20;

<figure><img src="../.gitbook/assets/image (547).png" alt=""><figcaption></figcaption></figure>

#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2019-11447](https://nvd.nist.gov/vuln/detail/cve-2019-11447)

While attempting to register a new account, the CAPTCHA image failed to render properly on the page. Inspecting the page source revealed the direct endpoint generating the CAPTCHA, allowing me to visit the URL directly, read the code, and complete the registration.

<figure><img src="../.gitbook/assets/image (548).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (549).png" alt=""><figcaption></figcaption></figure>



With a registered account, I exploited the arbitrary file upload vulnerability in CuteNews 2.1.2 by uploading a malicious PHP payload disguised as an avatar image. Triggering the uploaded file executed my reverse shell, granting initial access to the target machine

<figure><img src="../.gitbook/assets/image (551).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (552).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (553).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (554).png" alt=""><figcaption></figcaption></figure>

In order to get full terminal shell access used nc&#x20;

<figure><img src="../.gitbook/assets/image (555).png" alt=""><figcaption></figcaption></figure>

### Initial Access

Found local.txt in /var/www

<figure><img src="../.gitbook/assets/image (556).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation

Enumerating SUID binaries on the system revealed that `hping3` had the SUID bit set. By abusing its interactive shell feature via GTFOBins (`hping3` followed by `/bin/sh -p`), I spawned a root shell.

```
Command:- hping3 
          /bin/sh -p 
```

<figure><img src="../.gitbook/assets/image (557).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (558).png" alt=""><figcaption></figcaption></figure>

