# Kitsune

## Enumeration&#x20;

### Port scanning (rustscan)

```
Command:- rustscan -a 10.1.42.221 -- -A 
```

```
Open 10.1.42.221:53
Open 10.1.42.221:88
Open 10.1.42.221:135
Open 10.1.42.221:139
Open 10.1.42.221:389
Open 10.1.42.221:445
Open 10.1.42.221:464
Open 10.1.42.221:593
Open 10.1.42.221:636
Open 10.1.42.221:3269
Open 10.1.42.221:3268
Open 10.1.42.221:3389
Open 10.1.42.221:5985
Open 10.1.42.221:9389
Open 10.1.42.221:49664
Open 10.1.42.221:49667
Open 10.1.42.221:49671
Open 10.1.42.221:49673
Open 10.1.42.221:49674
Open 10.1.42.221:49694
Open 10.1.42.221:49721
Open 10.1.42.221:49733
Open 10.1.42.221:49761

```



### Port 445 - SMB&#x20;

Copy the users list with rid-brute module from nxc&#x20;

<figure><img src="../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

Anonymous guest access is allowed and have read access on share named Files. Share contains psafe2 file , which stores passwords. Download all the file with command mget

<figure><img src="../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>



psafe3 file seems to be password protected, so need to use pwsafe2john and crack it&#x20;

<figure><img src="../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>

Cracked the file password with john, which led to obtaining credentials for the user ranch

<figure><img src="../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>



### Pass the ticket attack

During the enumeration phase, NetExec (-M adcs) and Certipy identified an Active Directory Certificate Services (ADCS) server on DC01.kitsune.local running a template vulnerable to ESC13. By exploiting this misconfiguration and authenticating with the generated PFX file (-pfx), I successfully retrieved a ccache file to perform pass-the-ticket attack.

<figure><img src="../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

export the ccache file for kerberos authentication, this helps us to change the password for the user schlop, and got winrm access on port 5985

```
Command:- export KRB5CCNAME=ranch.ccache
```

<figure><img src="../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - winrm ( Initial access - user.txt)

<figure><img src="../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

Found an interesting file in documents called networkAuth.cred file and it contained user pebble hash

<figure><img src="../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

Upon researching on .cred files, found that we can decrypt the file and read cleartextpassword with command import-clixml, and retrieved password for user pebble.

<figure><img src="../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

Enumerated more with bloodhound data and found that user pebble hash reasgmsapassword permission on svc\_gmsa$, can abuse this privileges to get the NTLM hash for user svc\_gmsa$

<figure><img src="../.gitbook/assets/image (161).png" alt=""><figcaption></figcaption></figure>

Used nxc module gmsa to read the password&#x20;

<figure><img src="../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

User svc\_gmsa$ is a member of backup operators, but do not have any shell access on any port, so used windows registry script reg.py to download registry files like SAM and SYSTEM

<figure><img src="../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

Start a smbserver to download the registry files&#x20;

<figure><img src="../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

Now can do secretsdump and get the hash of the administrator&#x20;

<figure><img src="../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

### Root.txt

<figure><img src="../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

