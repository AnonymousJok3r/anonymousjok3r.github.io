# Blogger

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 c0:9f:a9:dc:52:46:7a:6e:bc:d9:58:df:eb:3e:74:59 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDASN6kt2row9ZdMLC0OPykNKLf7EJ/2AV3P9pm2svG7kRpYX8gO5k+0Wh/aTZoAh5DJqnLovTCiu/IteA3fe9dLGdifM8klW+btGvG7g+1f5g8MDdO+So+3XsEj8BZbOKe9aqwBaLwYMJjL/z0LDfT+WPUfazyMKPu+tNabNdGAzbYEcX2QAdRrWs72R5Y5fzc/EBmSbZFmtytCQHIk49Fw2rG6RsUDptQaEN9MrhwE6fY6gp4SU+YNY2evXj+RFCXKgZ9E8cPLZLn7vUut543r8PlBCRnZxXSxuY7vd0yOSuhcCOUMVQQdqSufMsep6iQFQYgiHveiPZRS3J2Zh1b
|   256 36:4a:44:a8:82:85:a6:33:87:0b:76:e5:5c:f5:d5:01 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLpP/bP6xlHl37glIaLNCz1BiNa3d+D5Zfbl5NeufdvIZgbHcx1hsq59Ck640C85jtANEwT7oHk7EOwVAMKKDb0=
|   256 b5:64:00:93:8a:e3:73:78:84:6d:42:2f:e1:e2:8c:b7 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJRtEBHTrQbJVrJq8NNXpTwaxcdCkcy65DfErLUpHSZ9
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Blogger | Home
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-methods: 
|_  Supported Methods: POST OPTIONS GET HEAD
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 3.10 - 4.11 (96%), Linux 3.13 - 4.4 (96%), Linux 3.8 - 3.16 (96%), Linux 4.4 (96%), Linux 3.2 - 4.14 (96%), Linux 2.6.32 - 3.13 (95%), Linux 2.6.32 - 3.10 (94%), Linux 3.16 (92%), Amazon Fire TV (92%), Sony Android TV (Android 5.0) (92%)
No exact OS matches for host (test conditions non-ideal).
```

### Port 80 - HTTP

I found the `register` functionality, but further investigation revealed that it does not lead anywhere useful or allow me to create a new user. It appears to be a dead end, so I decided not to investigate it further

<figure><img src="../.gitbook/assets/image (559).png" alt=""><figcaption></figcaption></figure>

Using `feroxbuster`, I discovered that a WordPress application is running on the target.

<figure><img src="../.gitbook/assets/image (560).png" alt=""><figcaption></figcaption></figure>

After adding the domain name to the `/etc/hosts` file, I was able to successfully access the WordPress application. The issue was caused by the domain name not being properly resolved.

<figure><img src="../.gitbook/assets/image (561).png" alt=""><figcaption></figcaption></figure>

Found username j@m3s

<figure><img src="../.gitbook/assets/image (562).png" alt=""><figcaption></figcaption></figure>

verified user j@m3s as valid user&#x20;

<figure><img src="../.gitbook/assets/image (563).png" alt=""><figcaption></figcaption></figure>

Using `WPScan`, I identified that the WordPress installation is running the `wpDiscuz` plugin, version `7.0.4`

<figure><img src="../.gitbook/assets/image (564).png" alt=""><figcaption></figcaption></figure>

#### CVE - [https://nvd.nist.gov/vuln/detail/cve-2020-24186](https://nvd.nist.gov/vuln/detail/cve-2020-24186)



#### PoC exploit for wpDiscuz v7.0.4 unauthenticated rce - [http://github.com/hev0x/CVE-2020-24186-wpDiscuz-7.0.4-RCE/tree/main](http://github.com/hev0x/CVE-2020-24186-wpDiscuz-7.0.4-RCE/tree/main)

### Initial access as user www-data&#x20;

<figure><img src="../.gitbook/assets/image (565).png" alt=""><figcaption></figcaption></figure>

I uploaded a small Bash reverse shell to get a more stable connection.

<figure><img src="../.gitbook/assets/image (567).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (568).png" alt=""><figcaption></figcaption></figure>

Found database credentials in wp-config.php file&#x20;

<figure><img src="../.gitbook/assets/image (569).png" alt=""><figcaption></figcaption></figure>

Found local.txt in james home directory

<figure><img src="../.gitbook/assets/image (570).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

After exploring several potential privilege escalation paths without success, I discovered that using `vagrant` as both the username and password allowed me to gain access to the system as the `vagrant` user.

<figure><img src="../.gitbook/assets/image (571).png" alt=""><figcaption></figcaption></figure>

Running `sudo -l` revealed that `vagrant` could execute any command as root without a password. I leveraged this misconfiguration to obtain a root shell and retrieve `proof.txt`.

<figure><img src="../.gitbook/assets/image (572).png" alt=""><figcaption></figcaption></figure>
