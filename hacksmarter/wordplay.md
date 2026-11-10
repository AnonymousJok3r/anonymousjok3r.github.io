# Wordplay

## Enumeration

### Nmap scan&#x20;

```
22/tcp    open  ssh      syn-ack ttl 62 OpenSSH 10.2p1 Ubuntu 2ubuntu3.2 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http     syn-ack ttl 62 Apache httpd 2.4.66 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: The Wired
|_http-generator: WordPress 6.9.4
|_http-server-header: Apache/2.4.66 (Ubuntu)
111/tcp   open  rpcbind  syn-ack ttl 62 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      34404/udp   mountd
|   100005  1,2,3      34505/tcp6  mountd
|   100005  1,2,3      38817/tcp   mountd
|   100005  1,2,3      56107/udp6  mountd
|   100021  1,3,4      36413/tcp   nlockmgr
|   100021  1,3,4      42143/tcp6  nlockmgr
|   100021  1,3,4      47252/udp   nlockmgr
|   100021  1,3,4      55221/udp6  nlockmgr
|   100024  1          33523/tcp6  status
|   100024  1          36250/udp6  status
|   100024  1          45397/tcp   status
|   100024  1          59820/udp   status
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/tcp6  nfs_acl
2049/tcp  open  nfs_acl  syn-ack ttl 62 3 (RPC #100227)
36413/tcp open  nlockmgr syn-ack ttl 62 1-4 (RPC #100021)
38817/tcp open  mountd   syn-ack ttl 62 1-3 (RPC #100005)
42869/tcp open  mountd   syn-ack ttl 62 1-3 (RPC #100005)
45397/tcp open  status   syn-ack ttl 62 1 (RPC #100024)
60831/tcp open  mountd   syn-ack ttl 62 1-3 (RPC #100005)

```

### Port 2049 -NFS&#x20;

Using showmount -e, I identified a publicly accessible NFS share (/var/nfs/documents), which I mounted locally to discover two leaked documents, but nothing was interesting in those documents.

<figure><img src="../.gitbook/assets/image (470).png" alt=""><figcaption></figcaption></figure>

### Port 80 - HTTP

Web application is running on wordpress v6.9.4

<figure><img src="../.gitbook/assets/image (471).png" alt=""><figcaption></figcaption></figure>

wpscan revealed that the site is using the post-slides plugin version 1.0.1. This specific version contains a known Local File Inclusion (LFI) vulnerability (CVE-2025-15491)

<figure><img src="../.gitbook/assets/image (472).png" alt=""><figcaption></figcaption></figure>

#### CVE- [https://nvd.nist.gov/vuln/detail/cve-2025-15491](https://nvd.nist.gov/vuln/detail/cve-2025-15491)



Looking back at the web application, able to enumerate users list with regular author checks, and found 2 users john and admin.

<figure><img src="../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure>

#### Wordpress Users Enumeration -[https://hackertarget.com/attacking-wordpress/](https://hackertarget.com/attacking-wordpress/)

When accessing, wp-admin it is redirecting me to a domain name called lklinux1.local, so added the domain the to hosts file and was able to access the admin page&#x20;

<figure><img src="../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure>

Trying username as password worked for user john&#x20;

<figure><img src="../.gitbook/assets/image (477).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (478).png" alt=""><figcaption></figcaption></figure>

On the dashboard, by navigating to "Posts" > "Add New" and inserting a "Shortcode" block to execute malicious code via the vulnerable plugin

<figure><img src="../.gitbook/assets/image (479).png" alt=""><figcaption></figcaption></figure>

**`Note:- Had issues with the lab, so did a reset and the ip of the target will be different, but the steps and methodology are same`**

Mounted it to different directory because of the lab reset

<figure><img src="../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>

I placed a reverse shell script **`bash.sh`** into the mounted NFS directory and created a PHP file **`shell.php`** that triggers it via the system() function.

<figure><img src="../.gitbook/assets/image (481).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure>

#### PoC for vulnerable plugin post-slides 1.0.1 - [https://wpscan.com/vulnerability/eb0424cc-e60c-44a5-aa24-cd1fe042b27a/](https://wpscan.com/vulnerability/eb0424cc-e60c-44a5-aa24-cd1fe042b27a/)



<figure><img src="../.gitbook/assets/image (484).png" alt=""><figcaption></figcaption></figure>

I then leveraged the WordPress shortcode feature to execute shell.php, which triggered my bash payload and successfully granted me a remote reverse shell

<figure><img src="../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (486).png" alt=""><figcaption></figcaption></figure>

I ran **`getcap -r /`** to look for Linux capabilities and discovered **`/usr/bin/gawk`** had **`cap_dac_read_search=ep`** enabled, allowing me to bypass file read restrictions and steal the **`id_rsa`** private key for the user **`martin`**

<figure><img src="../.gitbook/assets/image (488).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH

Using the extracted private key, I successfully authenticated via SSH on port 22 as the user martin to establish a more stable, higher-privileged session.

<figure><img src="../.gitbook/assets/image (490).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation

Running **sudo -l** revealed that martin could execute **/usr/bin/ansible-playbook** as root without a password. I exploited this by running a custom playbook that appended a new root user **(toor)** directly to **/etc/passwd**, allowing me to log in via **su toor** and obtain full root privileges.

<figure><img src="../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>







