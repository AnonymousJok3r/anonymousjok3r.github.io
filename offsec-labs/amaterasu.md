# Amaterasu

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT      STATE SERVICE REASON         VERSION
21/tcp    open  ftp     syn-ack ttl 61 vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.45.169
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
25022/tcp open  ssh     syn-ack ttl 61 OpenSSH 8.6 (protocol 2.0)
| ssh-hostkey: 
|   256 68:c6:05:e8:dc:f2:9a:2a:78:9b:ee:a1:ae:f6:38:1a (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBD6xv/PZkusP5TZdYJWDT8TTNY2xojo5b2DU/zrXm1tP4kkjNCGmwq8UwFrjo5EbEbk3wMmgHBnE73XwgnqaPd4=
|   256 e9:89:cc:c2:17:14:f3:bc:62:21:06:4a:5e:71:80:ce (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHRX3RvvSVPY3FJV9u7N2xIQbLJgQoEMkmRMey39/Jxz
33414/tcp open  http    syn-ack ttl 61 Werkzeug httpd 2.2.3 (Python 3.9.13)
|_http-title: 404 Not Found
|_http-server-header: Werkzeug/2.2.3 Python/3.9.13
40080/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.53 ((Fedora))
| http-methods: 
|   Supported Methods: GET POST OPTIONS HEAD TRACE
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.53 (Fedora)
|_http-title: My test page
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|router
Running (JUST GUESSING): Linux 4.X|5.X|2.6.X|3.X (97%), MikroTik RouterOS 7.X (95%)
```

### Port 40080, 33414 - HTTP&#x20;

**Port 40080:** Hosted what appeared to be a standard webpage. No particularly interesting functionality or potential attack surface was identified during the initial inspection.

**Port 33414:** Appeared more promising. After performing directory fuzzing, I discovered several accessible endpoints



<figure><img src="../.gitbook/assets/image (509).png" alt=""><figcaption></figcaption></figure>

Using the **`/api/file-list`** endpoint, I identified the username **`alfredo`** and discovered that his **`.ssh`** directory was accessible, although no private key could be retrieved. Since the **`/api/file-upload`** endpoint allowed successful file uploads, I generated an SSH key pair using **`ssh-keygen`** and uploaded the public key, which allowed me to authenticate to the SSH service as **`alfredo`**

<figure><img src="../.gitbook/assets/image (510).png" alt=""><figcaption></figcaption></figure>

The `curl -F` option allows us to send data using `multipart/form-data`, which is commonly used for file uploads. The `file=@example.txt` parameter attaches the actual contents of `example.txt` to the request, whereas `filename=example.txt` sends the filename as a separate form field. This distinction is important because the application may require both the file content and its intended filename to process the upload correctly.

```
Command:- Command:- curl -I -X POST 'http://ip:33414/file-upload' -F 'file=@file.txt' -F 'filename=file.txt'
```

<figure><img src="../.gitbook/assets/image (511).png" alt=""><figcaption></figcaption></figure>



Only few file types are allowed, so php will not work, tried by injecting php shell code inside the a picture but that attack was not successful

<figure><img src="../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure>

Generating a private key with ssh-keygen

<figure><img src="../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

change the file name to accepted file types&#x20;

<figure><img src="../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure>



### Port 25022 -SSH

Authenticated as user alfredo and able to access local.txt file&#x20;

<figure><img src="../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

While enumerating privilege escalation opportunities, I discovered a cron job in **`/etc/crontab`** that executes **`/usr/local/bin/backup-flask.sh`** every minute as root. Upon inspecting the script, I noticed that it uses **`tar`** with a wildcard **(`*`**) to archive files from **`/home/alfredo/restapi`**. This introduced a Tar Wildcard Injection vulnerability.

<figure><img src="../.gitbook/assets/image (516).png" alt=""><figcaption></figcaption></figure>

After identifying the vulnerable backup script, I created a malicious **`tar`** executable and crafted filenames to exploit tar's checkpoint functionality. Since the cron job runs as root, my payload was executed with root privileges, allowing me to add a new user named **`toor`** with root access. I then switched to the newly created account and verified successful privilege escalation using the **`id`** command

<figure><img src="../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>



