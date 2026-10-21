# Haystack

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT    STATE SERVICE  REASON         VERSION
21/tcp  open  ftp      syn-ack ttl 62 vsftpd 3.0.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.0.0.247
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-rw-r--    1 1000     1000        73761 May 24 04:40 app.zip
| -rw-r--r--    1 0        0           15562 May 24 05:19 backup.sh
| -rwxrw-r--    1 1000     1000       489837 May 24 05:09 blog.zip
| -rw-r--r--    1 1000     1000        99219 May 24 05:10 joomla.sql
|_-rwxrw-r--    1 1000     1000        12444 May 24 05:09 terraform.zip
22/tcp  open  ssh      syn-ack ttl 62 OpenSSH 10.2p1 Ubuntu 2ubuntu3.2 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http     syn-ack ttl 62 Apache httpd 2.4.66 ((Ubuntu))
|_http-title: In The Haystack 
| http-methods: 
|_  Supported Methods: OPTIONS HEAD GET POST
|_http-server-header: Apache/2.4.66 (Ubuntu)
110/tcp open  pop3     syn-ack ttl 62 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=lk-linux2
| Subject Alternative Name: DNS:lk-linux2
| Issuer: commonName=lk-linux2
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-05-24T03:57:58
| Not valid after:  2036-05-21T03:57:58
| MD5:     a641 c928 229f 0a5e 7250 e811 bb3e 884e
| SHA-1:   6b1a 6337 dc42 037c 48b5 1cae 7732 c2d6 3980 e890
| SHA-256: 26de b25e 5462 0a81 bbdb 5625 8765 8ff9 3200 6fd7 1bb4 476e 5035 3460 2d42 8352
| -----BEGIN CERTIFICATE-----
| MIIC+DCCAeCgAwIBAgIUcNcCiiGh9IQIdGEPpEcxn3uiCKcwDQYJKoZIhvcNAQEL
| BQAwFDESMBAGA1UEAwwJbGstbGludXgyMB4XDTI2MDUyNDAzNTc1OFoXDTM2MDUy
| MTAzNTc1OFowFDESMBAGA1UEAwwJbGstbGludXgyMIIBIjANBgkqhkiG9w0BAQEF
| AAOCAQ8AMIIBCgKCAQEA/OFm3KYHQmc6VxorTVWzgA7ed1ZFUtLlQGeeAb2eLQty
| zd6bR3SQ3OyVJ3u+FXfNuFrUvMLTIJQitfnZSOx63Ldx9MHC8hjZx6MkQa+yYsKJ
| 5BzUpuZ6UYwLhx0/ZWs6lD61i/zyHk+RF7+qcCqb3g+ZPU+bBTJ3s4jUgQLY0DFe
| 44jwktw/F2HDK5/iiKVknzVmAWMBWPgUQDsbVdrGqeAa/t+Rgdk3DA5dYdAykSRp
| /3pBYyOzoemkNYhu+CBUDIzAukiD1RkAcJwQM37bFBdW1xWTHp4LLYB1xTrlKcPX
| IjALMSGnO5TgHYJ4lCWpoUsbpl+PbYwZOI/uSzINfQIDAQABo0IwQDAJBgNVHRME
| AjAAMBQGA1UdEQQNMAuCCWxrLWxpbnV4MjAdBgNVHQ4EFgQUsySrB1NVV6twazMG
| xuogd05PvxcwDQYJKoZIhvcNAQELBQADggEBAO7v4DNWiZynWdh84Upobr9+hFH/
| Pcwc0bmMsG8WAW16vVeFPJLmWe7PTdaP4OJ7ylJyLQz61JHwsVlXi9hsa0j1gX+E
| RObeE5ajuYypv4F7mcF21Zi+0XE5cKoF8ZvmBHXtPzWpwLOPSOKCq7rF5fjCPpNp
| QXpLOCXLlZ8jnpY0c8SpYY8k8gCinUgRvbtCRZ9RuYcNd7e17+mnimYYbf3aJ6fZ
| G5JPKoN/XiKe0PN3AIdgpaDEHouyWVt5jNHg3QszSTseEyBiMA1CFcbSTiMPj0j+
| JWk8+1SAWZXFL/lMhKdEcIVa85MFpP5DdTDcY+SGawZMO8YddWIleoYHQ0c=
|_-----END CERTIFICATE-----
|_pop3-capabilities: RESP-CODES SASL STLS CAPA TOP AUTH-RESP-CODE PIPELINING UIDL
143/tcp open  imap     syn-ack ttl 62 Dovecot imapd
|_imap-capabilities: more SASL-IR have LITERAL+ OK IMAP4rev1 IDLE post-login STARTTLS LOGIN-REFERRALS listed ID Pre-login capabilities LOGINDISABLEDA0001 ENABLE
| ssl-cert: Subject: commonName=lk-linux2
| Subject Alternative Name: DNS:lk-linux2
| Issuer: commonName=lk-linux2
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-05-24T03:57:58
| Not valid after:  2036-05-21T03:57:58
| MD5:     a641 c928 229f 0a5e 7250 e811 bb3e 884e
| SHA-1:   6b1a 6337 dc42 037c 48b5 1cae 7732 c2d6 3980 e890
| SHA-256: 26de b25e 5462 0a81 bbdb 5625 8765 8ff9 3200 6fd7 1bb4 476e 5035 3460 2d42 8352
| -----BEGIN CERTIFICATE-----
| MIIC+DCCAeCgAwIBAgIUcNcCiiGh9IQIdGEPpEcxn3uiCKcwDQYJKoZIhvcNAQEL
| BQAwFDESMBAGA1UEAwwJbGstbGludXgyMB4XDTI2MDUyNDAzNTc1OFoXDTM2MDUy
| MTAzNTc1OFowFDESMBAGA1UEAwwJbGstbGludXgyMIIBIjANBgkqhkiG9w0BAQEF
| AAOCAQ8AMIIBCgKCAQEA/OFm3KYHQmc6VxorTVWzgA7ed1ZFUtLlQGeeAb2eLQty
| zd6bR3SQ3OyVJ3u+FXfNuFrUvMLTIJQitfnZSOx63Ldx9MHC8hjZx6MkQa+yYsKJ
| 5BzUpuZ6UYwLhx0/ZWs6lD61i/zyHk+RF7+qcCqb3g+ZPU+bBTJ3s4jUgQLY0DFe
| 44jwktw/F2HDK5/iiKVknzVmAWMBWPgUQDsbVdrGqeAa/t+Rgdk3DA5dYdAykSRp
| /3pBYyOzoemkNYhu+CBUDIzAukiD1RkAcJwQM37bFBdW1xWTHp4LLYB1xTrlKcPX
| IjALMSGnO5TgHYJ4lCWpoUsbpl+PbYwZOI/uSzINfQIDAQABo0IwQDAJBgNVHRME
| AjAAMBQGA1UdEQQNMAuCCWxrLWxpbnV4MjAdBgNVHQ4EFgQUsySrB1NVV6twazMG
| xuogd05PvxcwDQYJKoZIhvcNAQELBQADggEBAO7v4DNWiZynWdh84Upobr9+hFH/
| Pcwc0bmMsG8WAW16vVeFPJLmWe7PTdaP4OJ7ylJyLQz61JHwsVlXi9hsa0j1gX+E
| RObeE5ajuYypv4F7mcF21Zi+0XE5cKoF8ZvmBHXtPzWpwLOPSOKCq7rF5fjCPpNp
| QXpLOCXLlZ8jnpY0c8SpYY8k8gCinUgRvbtCRZ9RuYcNd7e17+mnimYYbf3aJ6fZ
| G5JPKoN/XiKe0PN3AIdgpaDEHouyWVt5jNHg3QszSTseEyBiMA1CFcbSTiMPj0j+
| JWk8+1SAWZXFL/lMhKdEcIVa85MFpP5DdTDcY+SGawZMO8YddWIleoYHQ0c=
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
993/tcp open  ssl/imap syn-ack ttl 62 Dovecot imapd
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: more SASL-IR LITERAL+ OK IMAP4rev1 IDLE have post-login LOGIN-REFERRALS listed ID Pre-login capabilities ENABLE AUTH=PLAINA0001
| ssl-cert: Subject: commonName=lk-linux2
| Subject Alternative Name: DNS:lk-linux2
| Issuer: commonName=lk-linux2
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-05-24T03:57:58
| Not valid after:  2036-05-21T03:57:58
| MD5:     a641 c928 229f 0a5e 7250 e811 bb3e 884e
| SHA-1:   6b1a 6337 dc42 037c 48b5 1cae 7732 c2d6 3980 e890
| SHA-256: 26de b25e 5462 0a81 bbdb 5625 8765 8ff9 3200 6fd7 1bb4 476e 5035 3460 2d42 8352
| -----BEGIN CERTIFICATE-----
| MIIC+DCCAeCgAwIBAgIUcNcCiiGh9IQIdGEPpEcxn3uiCKcwDQYJKoZIhvcNAQEL
| BQAwFDESMBAGA1UEAwwJbGstbGludXgyMB4XDTI2MDUyNDAzNTc1OFoXDTM2MDUy
| MTAzNTc1OFowFDESMBAGA1UEAwwJbGstbGludXgyMIIBIjANBgkqhkiG9w0BAQEF
| AAOCAQ8AMIIBCgKCAQEA/OFm3KYHQmc6VxorTVWzgA7ed1ZFUtLlQGeeAb2eLQty
| zd6bR3SQ3OyVJ3u+FXfNuFrUvMLTIJQitfnZSOx63Ldx9MHC8hjZx6MkQa+yYsKJ
| 5BzUpuZ6UYwLhx0/ZWs6lD61i/zyHk+RF7+qcCqb3g+ZPU+bBTJ3s4jUgQLY0DFe
| 44jwktw/F2HDK5/iiKVknzVmAWMBWPgUQDsbVdrGqeAa/t+Rgdk3DA5dYdAykSRp
| /3pBYyOzoemkNYhu+CBUDIzAukiD1RkAcJwQM37bFBdW1xWTHp4LLYB1xTrlKcPX
| IjALMSGnO5TgHYJ4lCWpoUsbpl+PbYwZOI/uSzINfQIDAQABo0IwQDAJBgNVHRME
| AjAAMBQGA1UdEQQNMAuCCWxrLWxpbnV4MjAdBgNVHQ4EFgQUsySrB1NVV6twazMG
| xuogd05PvxcwDQYJKoZIhvcNAQELBQADggEBAO7v4DNWiZynWdh84Upobr9+hFH/
| Pcwc0bmMsG8WAW16vVeFPJLmWe7PTdaP4OJ7ylJyLQz61JHwsVlXi9hsa0j1gX+E
| RObeE5ajuYypv4F7mcF21Zi+0XE5cKoF8ZvmBHXtPzWpwLOPSOKCq7rF5fjCPpNp
| QXpLOCXLlZ8jnpY0c8SpYY8k8gCinUgRvbtCRZ9RuYcNd7e17+mnimYYbf3aJ6fZ
| G5JPKoN/XiKe0PN3AIdgpaDEHouyWVt5jNHg3QszSTseEyBiMA1CFcbSTiMPj0j+
| JWk8+1SAWZXFL/lMhKdEcIVa85MFpP5DdTDcY+SGawZMO8YddWIleoYHQ0c=
|_-----END CERTIFICATE-----
995/tcp open  ssl/pop3 syn-ack ttl 62 Dovecot pop3d
|_pop3-capabilities: RESP-CODES SASL(PLAIN) USER CAPA TOP AUTH-RESP-CODE PIPELINING UIDL
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=lk-linux2
| Subject Alternative Name: DNS:lk-linux2
| Issuer: commonName=lk-linux2
| Public Key type: rsa

```



### Port 21 - FTP

Anonymous login is allowed, and able to download the files.

```
Command:- mget *
```

<figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

file app.zip is password protected, so used zip2john to crack the password&#x20;

```
Command:- zip2john app.zip > hash
```

<figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

Unzipped the contents. While the active codebase yielded no credentials, checking the Git version history exposed a plaintext password for the user justin in an older commit.

```
7z x app.zip 
```

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>



### Port 80 - HTTP

Directory fuzzing revealed that there was /roundcube webmail instance was running on port 80&#x20;

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>



### Roundcube webmail&#x20;

Authenticated successfully with justin credentials

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

Identified the version number in about, and this particular version is vulnerable to remote code execution

[https://nvd.nist.gov/vuln/detail/cve-2025-49113](https://nvd.nist.gov/vuln/detail/cve-2025-49113)&#x20;

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

### Exploit repo

[https://github.com/fearsoff-org/CVE-2025-49113](https://github.com/fearsoff-org/CVE-2025-49113)

Clone the repo, and run php script for remote code execution and full terminal shell access as user www-data. craft a bash reverse shell payload and start netcat listener&#x20;

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

### Initial access

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

Able to escalate privileges to justin from www-data with earlier found credentials, and justin is part of adm group. adm group users can read /var/log files, which often store sensitive information like passwords.

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

Found gilbert password in /var/log

```
Command:- grep -Rni 'password' .
```

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation

Gilbert credentials are valid and gained ssh access on port 22. User has sudo misconfiguration /usr/bin/git diff, Since git diff natively uses a terminal pager (typically less) to display content, it can be forced into an interactive prompt where an arbitrary shell execution escape sequence can be entered to gain root access.

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

```
Command:- sudo /usr/bin/git diff /dev/null /etc/shadow
!/bin/sh
id 
cat /root/root.txt
```

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>





