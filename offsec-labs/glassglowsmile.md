# GlassGlowSmile

## Enumeration&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 9c:f2:68:fd:80:8e:8a:27:9d:6b:16:4e:d2:89:9b:c0 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDoB9oGHsIoZUHlPJEiHlbo5ug9Yq3l6OKPqfiy/gx0Nyr5P3T2o2+rNhz9At07JANRRI5SDiMnP/lVgRHze4CfpTEleweWVGgyg8/eYWH1UTqx269nALiSWW4ZKp2KlxYPiqy3kx8lxGzHcaHJ3b9dpd9lFHsKusXxG8gWoUtjHUU9EwmlkPDBmoy6AqYzeu8w28ZnanWdjxzMXEtPMfkIiHb8GK16XIdzVbMUCxo166uRUf2NUqkdMJPQt7oIZr5vhnaFwVJ5PTdKqQ0CZ4yf0/QPhE05Nja9oT/Cb7GhdynqO8NvxQGxpMgcBDKQHHGtqRo0WHDknJFsjtZJjVQP
|   256 b3:6d:01:6a:df:32:b5:52:b6:9c:45:05:0b:f9:5d:d9 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBhobHHQIHEpI8VxCnL+DUvRGFlBolH1lCJTda3v5snNL2pCalX9EqQy+JUlkPiLdYZZnI+fJ3khT8RMvRYjBFY=
|   256 40:36:8b:f5:a7:45:ca:b5:31:92:d7:89:6e:6c:fc:3a (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO/pEcm1NeuX0Gcr0bu22MFuc3qJixWjcjHETqpAZFZq
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.38 ((Debian))
|_http-title: Site doesn't have a title (text/html).
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-server-header: Apache/2.4.38 (Debian)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 2.6.32 - 3.13 (96%), Linux 4.15 (96%), Linux 5.0 - 5.14 (96%), Linux 5.14 - 6.8 (96%), Linux 3.2 - 4.14 (96%), Linux 4.15 - 5.19 (96%), Linux 2.6.32 - 3.10 (96%), Linux 3.10 - 4.11 (95%), Linux 2.6.32 - 3.5 (93%), HP P2000 G3 NAS device (93%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/16%OT=22%CT=%CU=42356%PV=Y%DS=4%DC=T%G=N%TM=6AFB3DF0%P=x86_64-pc-linux-gnu)
SEQ(SP=102%GCD=1%ISR=10A%TI=Z%CI=Z%II=I%TS=B)
SEQ(SP=104%GCD=1%ISR=107%TI=Z%CI=Z%II=I%TS=A)
OPS(O1=M540ST11NW7%O2=M540ST11NW7%O3=M540NNT11NW7%O4=M540ST11NW7%O5=M540ST11NW7%O6=M540ST11)

```

### Port 80 - HTTP

I performed directory brute-forcing to identify hidden directories and web applications hosted on the target. During this process, I discovered a Joomla installation, which became the next point of investigation.

<figure><img src="../.gitbook/assets/image (581).png" alt=""><figcaption></figcaption></figure>

#### Joomla Version detection

```
Command:- curl -s http://IP/administrator/manifests/files/joomla.xml | grep -i version 
```



I used CeWL to extract keywords from the target website and generate a custom wordlist for password-related testing

<figure><img src="../.gitbook/assets/image (582).png" alt=""><figcaption></figcaption></figure>

I intercepted the authentication request and used the custom wordlist generated with CeWL to perform a password brute-force attack. This allowed me to identify a valid password for the `joomla` user.

<figure><img src="../.gitbook/assets/image (583).png" alt=""><figcaption></figcaption></figure>

After successfully authenticating to the Joomla administrator panel, I navigated to Extensions → Templates. I then modified the `error.php` template file by adding a simple PHP command shell, which allowed me to execute system commands through the web application.

<figure><img src="../.gitbook/assets/image (584).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (585).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (586).png" alt=""><figcaption></figcaption></figure>

I started a Netcat listener on my attacking machine and triggered the reverse shell from the target server. Once the connection was established, I successfully obtained an interactive shell, allowing me to execute commands on the target system

<figure><img src="../.gitbook/assets/image (587).png" alt=""><figcaption></figcaption></figure>

Found local.txt file in rob home directory&#x20;

<figure><img src="../.gitbook/assets/image (589).png" alt=""><figcaption></figcaption></figure>

Found database credentials in configuration.php file in /var/www/html/joomla

<figure><img src="../.gitbook/assets/image (590).png" alt=""><figcaption></figcaption></figure>

During further enumeration of the database, I discovered another database named `mybatjoke`. After inspecting its tables, I found a table named `taskforce`, which contained a password hash belonging to the user `rob`.

<figure><img src="../.gitbook/assets/image (591).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (593).png" alt=""><figcaption></figcaption></figure>



The hash was decoded with base64&#x20;

<figure><img src="../.gitbook/assets/image (592).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH&#x20;

Authenticated as rob&#x20;

<figure><img src="../.gitbook/assets/image (594).png" alt=""><figcaption></figcaption></figure>

While enumerating `rob`'s home directory, I discovered a file containing encrypted text. I used an online cipher identification tool to determine that the text was encrypted using the Vigenère cipher. After decrypting the content, I found a hash associated with the user `abner`. The hash was decoded with base64&#x20;

<figure><img src="../.gitbook/assets/image (595).png" alt=""><figcaption></figcaption></figure>

#### Identifying cipher - [https://www.boxentriq.com/analysis/cipher-identifier](https://www.boxentriq.com/analysis/cipher-identifier)

#### Vigenère Cipher Decryption - [https://www.dcode.fr/vigenere-cipher](https://www.dcode.fr/vigenere-cipher)



<figure><img src="../.gitbook/assets/image (596).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (597).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (598).png" alt=""><figcaption></figcaption></figure>

I used the `find` command to search the filesystem for files and directories owned by the user `abner`. This helped me identify a hidden zip file that conatined penguin user credentials&#x20;

```
Command:- find / -user abner 2>/dev/null
```

<figure><img src="../.gitbook/assets/image (599).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (601).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation

I used `pspy64` to monitor running processes and identify scheduled tasks on the target system. During this process, I noticed that a process named `.trash_old`, located in the `penguin` user's home directory, was being executed with root privileges. I modified the file to include a Netcat reverse shell command. After waiting for the scheduled task to execute again, I received a reverse shell connection with root privileges, successfully escalating my access to `root`

<figure><img src="../.gitbook/assets/image (602).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (603).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (604).png" alt=""><figcaption></figcaption></figure>





