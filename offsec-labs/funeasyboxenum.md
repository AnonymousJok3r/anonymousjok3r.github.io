# FunEasyBoxEnum

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 de:ae:45:ec:96:56:1e:77:f0:cc:4b:98:45:9a:02:14 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCi+9RO4xYnkRYRaUHO97Z1M93h6H0glzp39lhmsOYjgtKV30yfdOBsaCpfkivvlMxwE4KQU5DcE5LFx/4pAoTm+RAUhDJQ0Z3kAjbf97w/pVOJe7KWdhaJABiAhC2vkGxhYeVJnyh82bp5bmhfS15izUKAtDjmBfGitM02PwkEKhFkQi3Phe6how643osxgCk7C9EexXnOcPeijv1jrg71oA8OgoG3/F8hm3USgr3kPMLQp1eCfNYL0Qg9JFJwG+XCkVJhNxKDurKrh+xM2U/xsC936SRcTisNnbgLRznMDHdgytUlBgo0Uy/P8KASDF8t26EJ/dNXRVZYM/cJdZ6b
|   256 a0:54:e7:18:0b:d6:b6:81:b2:96:b3:af:01:9d:db:1d (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOs2JZSmcGOjkNrb/d3ob8waEIm4ODJtqsFgLh5BKE7hs40D3MrpGdqpC8yqbjnfM9yUUuTaMlrYkx4goTW7Nso=
|   256 94:9d:69:a9:57:5a:e0:86:f0:e7:88:98:92:07:f2:f7 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIB3VH+qvW5B5l84QY/XnKUVYdg62a+SZKcM8HmxU++FG
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.29 (Ubuntu)
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (96%), Linux 4.15 (96%), Linux 5.0 - 5.14 (96%), Linux 5.14 - 6.8 (96%), Linux 3.2 - 4.14 (96%), Linux 4.15 - 5.19 (96%), Linux 2.6.32 - 3.10 (96%), Linux 3.10 - 4.11 (95%), Linux 2.6.32 - 3.5 (93%), HP P2000 G3 NAS device (93%)
No exact OS matches for host (test conditions non-ideal).

```

### Port 80 - HTTP

While performing directory enumeration, I identified an accessible PHP endpoint named `mini.php`

<figure><img src="../.gitbook/assets/image (573).png" alt=""><figcaption></figcaption></figure>

After discovering `mini.php` during directory enumeration, I navigated to the endpoint and identified a file upload functionality, and I uploaded a php reverse shell

<figure><img src="../.gitbook/assets/image (574).png" alt=""><figcaption></figcaption></figure>

After successfully uploading the payload, I navigated to `/shell.php`, which triggered the reverse shell connection. This provided me with shell access to the target system as the `www-data` user.

<figure><img src="../.gitbook/assets/image (575).png" alt=""><figcaption></figcaption></figure>

Found local.txt file in /var/www

<figure><img src="../.gitbook/assets/image (576).png" alt=""><figcaption></figcaption></figure>

After enumerating the available user accounts, I attempted to authenticate using the username as the password. This weak credential configuration allowed me to successfully log in as `goat`

<figure><img src="../.gitbook/assets/image (577).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (578).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

<figure><img src="../.gitbook/assets/image (579).png" alt=""><figcaption></figcaption></figure>

I identified a sudo misconfiguration involving `/usr/bin/mysql`. By exploiting this misconfiguration, I was able to escalate privileges from `goat` to `root`

#### PoC - [https://gtfobins.org/gtfobins/mysql/](https://gtfobins.org/gtfobins/mysql/)



<figure><img src="../.gitbook/assets/image (580).png" alt=""><figcaption></figcaption></figure>
