# 404 Bank

## Enumeration&#x20;



### Port scanning&#x20;

```
PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
80/tcp    open  http          syn-ack ttl 126 Microsoft IIS httpd 10.0
|_http-title: 404 Finance Group
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-10-26 13:51:04Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: 404finance.local, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC-404.404finance.local
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC-404.404finance.local
| Issuer: commonName=404finance-DC-404-CA/domainComponent=404finance
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-26T13:35:05
| Not valid after:  2027-10-26T13:35:05
| MD5:     efe5 0742 6716 90c8 14cf 82af 29ef 63e4
| SHA-1:   6066 3558 3b23 369b d4dc 76a0 2d75 94f0 ef06 93c6
| SHA-256: 517f 9ddf 5da6 4b4d d323 1622 1b87 294f bca1 8bb2 0178 e47b 633b 083b 552a 652f
| -----BEGIN CERTIFICATE-----
| MIIGXTCCBUWgAwIBAgITFAAAAAQFV2HyMEyf5QAAAAAABDANBgkqhkiG9w0BAQsF
| ADBSMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxGjAYBgoJkiaJk/IsZAEZFgo0MDRm
| aW5hbmNlMR0wGwYDVQQDExQ0MDRmaW5hbmNlLURDLTQwNC1DQTAeFw0yNjEwMjYx
| MzM1MDVaFw0yNzEwMjYxMzM1MDVaMCIxIDAeBgNVBAMTF0RDLTQwNC40MDRmaW5h
| bmNlLmxvY2FsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwq8fRJ21
| IM0DlTGkM6x2jnwqzxnrSiYIdSHV+VNarKvTPt3SLI/BxWrJwYdX7zGM0ZnCqlsB
| J3MUI1egGELaXphyIhRJxwwJEdjkI3gTt9bgVjQP52TwwQlAIGH7LlAf1+3FfaDM
| +4UM7ovfBuMoTeaj37L4iHPEqEwfpygXl0lw56mlBzxfPwaXc6v502O8JgbgAkGY
| 1UsqwfAXZzLHuZLgmKZD3ZyaAI2yNx1Ghs7RMxXtZ9Z9h0XUqlcv+ybNX45LMPBQ
| XuFvg5ahVj4KB5UzFoj39WAJX4wg5mIXouGiRsUXZEw7i8EcRS2HhNDBbYsL97+H
| u/r9F9w7Bmo/4QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBh
| AGkAbgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggr
| BgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG
| 9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQME
| AS0wCwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0D
| BzAdBgNVHQ4EFgQUjewvXaKgrd8lGWR2SZ8FOPf6d9wwHwYDVR0jBBgwFoAUYCDD
| p0zNzj1hn627bWVopybiQqQwgdYGA1UdHwSBzjCByzCByKCBxaCBwoaBv2xkYXA6
| Ly8vQ049NDA0ZmluYW5jZS1EQy00MDQtQ0EsQ049REMtNDA0LENOPUNEUCxDTj1Q
| dWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0
| aW9uLERDPTQwNGZpbmFuY2UsREM9bG9jYWw/Y2VydGlmaWNhdGVSZXZvY2F0aW9u
| TGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50MIHLBggr
| BgEFBQcBAQSBvjCBuzCBuAYIKwYBBQUHMAKGgatsZGFwOi8vL0NOPTQwNGZpbmFu
| Y2UtREMtNDA0LUNBLENOPUFJQSxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxD
| Tj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0aW9uLERDPTQwNGZpbmFuY2UsREM9bG9j
| YWw/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25B
| dXRob3JpdHkwQwYDVR0RBDwwOqAfBgkrBgEEAYI3GQGgEgQQrWGYGlXpVEOwHBNc
| wFZNIYIXREMtNDA0LjQwNGZpbmFuY2UubG9jYWwwTgYJKwYBBAGCNxkCBEEwP6A9
| BgorBgEEAYI3GQIBoC8ELVMtMS01LTIxLTI5NTY3MjU0NzMtMzE3NzgyOTE4LTI3
| OTU2MzY0OTYtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEAGD8iKf9U0F1XBIq13A8p
| 2TX7jI/+wl40kxWFP76SyezpIWEQrttWpIv5sYxypmDYpH+DZB3P2anLOpEuzQko
| ka2teP2qoF+JocZqAyP99/gDIipx9vQqB8Xf+sdKj2zoP2ryEGqQhGrj7GgNAmh0
| MLw98pm6MAdJ/EnlmnmHWk1ttAMUghP4dA0Xs8bBHZBHBVrEGqpmAiMbxZnJiCMc
| WZ0/lpYwznJ928YXAkEomPnIoU9J005y0GlfLqIudhMWz1CSzHaNUqKY/CuURkN7
| 6wcdQX/lz5TATsSTNPEwPGLPEqQv+HNckFJwU3lj/8VqrewXiiaSHd+Ys3KZjVvt
| wA==
|_-----END CERTIFICATE-----
|_ssl-date: 2026-10-26T13:52:35+00:00; 0s from scanner time.
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: 404finance.local, Site: Default-First-Site-Name)
|_ssl-date: 2026-10-26T13:52:35+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC-404.404finance.local
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC-404.404finance.local
| Issuer: commonName=404finance-DC-404-CA/domainComponent=404finance
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-26T13:35:05
| Not valid after:  2027-10-26T13:35:05
| MD5:     efe5 0742 6716 90c8 14cf 82af 29ef 63e4
| SHA-1:   6066 3558 3b23 369b d4dc 76a0 2d75 94f0 ef06 93c6
| SHA-256: 517f 9ddf 5da6 4b4d d323 1622 1b87 294f bca1 8bb2 0178 e47b 633b 083b 552a 652f
| -----BEGIN CERTIFICATE-----
| MIIGXTCCBUWgAwIBAgITFAAAAAQFV2HyMEyf5QAAAAAABDANBgkqhkiG9w0BAQsF
| ADBSMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxGjAYBgoJkiaJk/IsZAEZFgo0MDRm
| aW5hbmNlMR0wGwYDVQQDExQ0MDRmaW5hbmNlLURDLTQwNC1DQTAeFw0yNjEwMjYx
| MzM1MDVaFw0yNzEwMjYxMzM1MDVaMCIxIDAeBgNVBAMTF0RDLTQwNC40MDRmaW5h
| bmNlLmxvY2FsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwq8fRJ21
| IM0DlTGkM6x2jnwqzxnrSiYIdSHV+VNarKvTPt3SLI/BxWrJwYdX7zGM0ZnCqlsB
| J3MUI1egGELaXphyIhRJxwwJEdjkI3gTt9bgVjQP52TwwQlAIGH7LlAf1+3FfaDM
| +4UM7ovfBuMoTeaj37L4iHPEqEwfpygXl0lw56mlBzxfPwaXc6v502O8JgbgAkGY
| 1UsqwfAXZzLHuZLgmKZD3ZyaAI2yNx1Ghs7RMxXtZ9Z9h0XUqlcv+ybNX45LMPBQ
| XuFvg5ahVj4KB5UzFoj39WAJX4wg5mIXouGiRsUXZEw7i8EcRS2HhNDBbYsL97+H
| u/r9F9w7Bmo/4QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBh
| AGkAbgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggr
| BgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG
| 9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQME
| AS0wCwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0D
| BzAdBgNVHQ4EFgQUjewvXaKgrd8lGWR2SZ8FOPf6d9wwHwYDVR0jBBgwFoAUYCDD
| p0zNzj1hn627bWVopybiQqQwgdYGA1UdHwSBzjCByzCByKCBxaCBwoaBv2xkYXA6
| Ly8vQ049NDA0ZmluYW5jZS1EQy00MDQtQ0EsQ049REMtNDA0LENOPUNEUCxDTj1Q
| dWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0
| aW9uLERDPTQwNGZpbmFuY2UsREM9bG9jYWw/Y2VydGlmaWNhdGVSZXZvY2F0aW9u
| TGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50MIHLBggr
| BgEFBQcBAQSBvjCBuzCBuAYIKwYBBQUHMAKGgatsZGFwOi8vL0NOPTQwNGZpbmFu
| Y2UtREMtNDA0LUNBLENOPUFJQSxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxD
| Tj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0aW9uLERDPTQwNGZpbmFuY2UsREM9bG9j
| YWw/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25B
| dXRob3JpdHkwQwYDVR0RBDwwOqAfBgkrBgEEAYI3GQGgEgQQrWGYGlXpVEOwHBNc
| wFZNIYIXREMtNDA0LjQwNGZpbmFuY2UubG9jYWwwTgYJKwYBBAGCNxkCBEEwP6A9
| BgorBgEEAYI3GQIBoC8ELVMtMS01LTIxLTI5NTY3MjU0NzMtMzE3NzgyOTE4LTI3
| OTU2MzY0OTYtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEAGD8iKf9U0F1XBIq13A8p
| 2TX7jI/+wl40kxWFP76SyezpIWEQrttWpIv5sYxypmDYpH+DZB3P2anLOpEuzQko
| ka2teP2qoF+JocZqAyP99/gDIipx9vQqB8Xf+sdKj2zoP2ryEGqQhGrj7GgNAmh0
| MLw98pm6MAdJ/EnlmnmHWk1ttAMUghP4dA0Xs8bBHZBHBVrEGqpmAiMbxZnJiCMc
| WZ0/lpYwznJ928YXAkEomPnIoU9J005y0GlfLqIudhMWz1CSzHaNUqKY/CuURkN7
| 6wcdQX/lz5TATsSTNPEwPGLPEqQv+HNckFJwU3lj/8VqrewXiiaSHd+Ys3KZjVvt
| wA==
|_-----END CERTIFICATE-----
3268/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: 404finance.local, Site: Default-First-Site-Name)
|_ssl-date: 2026-10-26T13:52:35+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC-404.404finance.local
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC-404.404finance.local
| Issuer: commonName=404finance-DC-404-CA/domainComponent=404finance
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-26T13:35:05
| Not valid after:  2027-10-26T13:35:05
| MD5:     efe5 0742 6716 90c8 14cf 82af 29ef 63e4
| SHA-1:   6066 3558 3b23 369b d4dc 76a0 2d75 94f0 ef06 93c6
| SHA-256: 517f 9ddf 5da6 4b4d d323 1622 1b87 294f bca1 8bb2 0178 e47b 633b 083b 552a 652f
| -----BEGIN CERTIFICATE-----
| MIIGXTCCBUWgAwIBAgITFAAAAAQFV2HyMEyf5QAAAAAABDANBgkqhkiG9w0BAQsF
| ADBSMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxGjAYBgoJkiaJk/IsZAEZFgo0MDRm
| aW5hbmNlMR0wGwYDVQQDExQ0MDRmaW5hbmNlLURDLTQwNC1DQTAeFw0yNjEwMjYx
| MzM1MDVaFw0yNzEwMjYxMzM1MDVaMCIxIDAeBgNVBAMTF0RDLTQwNC40MDRmaW5h
| bmNlLmxvY2FsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwq8fRJ21
| IM0DlTGkM6x2jnwqzxnrSiYIdSHV+VNarKvTPt3SLI/BxWrJwYdX7zGM0ZnCqlsB
| J3MUI1egGELaXphyIhRJxwwJEdjkI3gTt9bgVjQP52TwwQlAIGH7LlAf1+3FfaDM
| +4UM7ovfBuMoTeaj37L4iHPEqEwfpygXl0lw56mlBzxfPwaXc6v502O8JgbgAkGY
| 1UsqwfAXZzLHuZLgmKZD3ZyaAI2yNx1Ghs7RMxXtZ9Z9h0XUqlcv+ybNX45LMPBQ
| XuFvg5ahVj4KB5UzFoj39WAJX4wg5mIXouGiRsUXZEw7i8EcRS2HhNDBbYsL97+H
| u/r9F9w7Bmo/4QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBh
| AGkAbgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggr
| BgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG
| 9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQME
| AS0wCwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0D
| BzAdBgNVHQ4EFgQUjewvXaKgrd8lGWR2SZ8FOPf6d9wwHwYDVR0jBBgwFoAUYCDD
| p0zNzj1hn627bWVopybiQqQwgdYGA1UdHwSBzjCByzCByKCBxaCBwoaBv2xkYXA6
| Ly8vQ049NDA0ZmluYW5jZS1EQy00MDQtQ0EsQ049REMtNDA0LENOPUNEUCxDTj1Q
| dWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0
| aW9uLERDPTQwNGZpbmFuY2UsREM9bG9jYWw/Y2VydGlmaWNhdGVSZXZvY2F0aW9u
| TGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50MIHLBggr
| BgEFBQcBAQSBvjCBuzCBuAYIKwYBBQUHMAKGgatsZGFwOi8vL0NOPTQwNGZpbmFu
| Y2UtREMtNDA0LUNBLENOPUFJQSxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxD
| Tj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0aW9uLERDPTQwNGZpbmFuY2UsREM9bG9j
| YWw/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25B
| dXRob3JpdHkwQwYDVR0RBDwwOqAfBgkrBgEEAYI3GQGgEgQQrWGYGlXpVEOwHBNc
| wFZNIYIXREMtNDA0LjQwNGZpbmFuY2UubG9jYWwwTgYJKwYBBAGCNxkCBEEwP6A9
| BgorBgEEAYI3GQIBoC8ELVMtMS01LTIxLTI5NTY3MjU0NzMtMzE3NzgyOTE4LTI3
| OTU2MzY0OTYtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEAGD8iKf9U0F1XBIq13A8p
| 2TX7jI/+wl40kxWFP76SyezpIWEQrttWpIv5sYxypmDYpH+DZB3P2anLOpEuzQko
| ka2teP2qoF+JocZqAyP99/gDIipx9vQqB8Xf+sdKj2zoP2ryEGqQhGrj7GgNAmh0
| MLw98pm6MAdJ/EnlmnmHWk1ttAMUghP4dA0Xs8bBHZBHBVrEGqpmAiMbxZnJiCMc
| WZ0/lpYwznJ928YXAkEomPnIoU9J005y0GlfLqIudhMWz1CSzHaNUqKY/CuURkN7
| 6wcdQX/lz5TATsSTNPEwPGLPEqQv+HNckFJwU3lj/8VqrewXiiaSHd+Ys3KZjVvt
| wA==
|_-----END CERTIFICATE-----
3269/tcp  open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: 404finance.local, Site: Default-First-Site-Name)
|_ssl-date: 2026-10-26T13:52:35+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC-404.404finance.local
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC-404.404finance.local
| Issuer: commonName=404finance-DC-404-CA/domainComponent=404finance
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-26T13:35:05
| Not valid after:  2027-10-26T13:35:05
| MD5:     efe5 0742 6716 90c8 14cf 82af 29ef 63e4
| SHA-1:   6066 3558 3b23 369b d4dc 76a0 2d75 94f0 ef06 93c6
| SHA-256: 517f 9ddf 5da6 4b4d d323 1622 1b87 294f bca1 8bb2 0178 e47b 633b 083b 552a 652f
| -----BEGIN CERTIFICATE-----
| MIIGXTCCBUWgAwIBAgITFAAAAAQFV2HyMEyf5QAAAAAABDANBgkqhkiG9w0BAQsF
| ADBSMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxGjAYBgoJkiaJk/IsZAEZFgo0MDRm
| aW5hbmNlMR0wGwYDVQQDExQ0MDRmaW5hbmNlLURDLTQwNC1DQTAeFw0yNjEwMjYx
| MzM1MDVaFw0yNzEwMjYxMzM1MDVaMCIxIDAeBgNVBAMTF0RDLTQwNC40MDRmaW5h
| bmNlLmxvY2FsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwq8fRJ21
| IM0DlTGkM6x2jnwqzxnrSiYIdSHV+VNarKvTPt3SLI/BxWrJwYdX7zGM0ZnCqlsB
| J3MUI1egGELaXphyIhRJxwwJEdjkI3gTt9bgVjQP52TwwQlAIGH7LlAf1+3FfaDM
| +4UM7ovfBuMoTeaj37L4iHPEqEwfpygXl0lw56mlBzxfPwaXc6v502O8JgbgAkGY
| 1UsqwfAXZzLHuZLgmKZD3ZyaAI2yNx1Ghs7RMxXtZ9Z9h0XUqlcv+ybNX45LMPBQ
| XuFvg5ahVj4KB5UzFoj39WAJX4wg5mIXouGiRsUXZEw7i8EcRS2HhNDBbYsL97+H
| u/r9F9w7Bmo/4QIDAQABo4IDWjCCA1YwLwYJKwYBBAGCNxQCBCIeIABEAG8AbQBh
| AGkAbgBDAG8AbgB0AHIAbwBsAGwAZQByMB0GA1UdJQQWMBQGCCsGAQUFBwMCBggr
| BgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAweAYJKoZIhvcNAQkPBGswaTAOBggqhkiG
| 9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCAMAsGCWCGSAFlAwQBKjALBglghkgBZQME
| AS0wCwYJYIZIAWUDBAECMAsGCWCGSAFlAwQBBTAHBgUrDgMCBzAKBggqhkiG9w0D
| BzAdBgNVHQ4EFgQUjewvXaKgrd8lGWR2SZ8FOPf6d9wwHwYDVR0jBBgwFoAUYCDD
| p0zNzj1hn627bWVopybiQqQwgdYGA1UdHwSBzjCByzCByKCBxaCBwoaBv2xkYXA6
| Ly8vQ049NDA0ZmluYW5jZS1EQy00MDQtQ0EsQ049REMtNDA0LENOPUNEUCxDTj1Q
| dWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0
| aW9uLERDPTQwNGZpbmFuY2UsREM9bG9jYWw/Y2VydGlmaWNhdGVSZXZvY2F0aW9u
| TGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50MIHLBggr
| BgEFBQcBAQSBvjCBuzCBuAYIKwYBBQUHMAKGgatsZGFwOi8vL0NOPTQwNGZpbmFu
| Y2UtREMtNDA0LUNBLENOPUFJQSxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxD
| Tj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0aW9uLERDPTQwNGZpbmFuY2UsREM9bG9j
| YWw/Y0FDZXJ0aWZpY2F0ZT9iYXNlP29iamVjdENsYXNzPWNlcnRpZmljYXRpb25B
| dXRob3JpdHkwQwYDVR0RBDwwOqAfBgkrBgEEAYI3GQGgEgQQrWGYGlXpVEOwHBNc
| wFZNIYIXREMtNDA0LjQwNGZpbmFuY2UubG9jYWwwTgYJKwYBBAGCNxkCBEEwP6A9
| BgorBgEEAYI3GQIBoC8ELVMtMS01LTIxLTI5NTY3MjU0NzMtMzE3NzgyOTE4LTI3
| OTU2MzY0OTYtMTAwMDANBgkqhkiG9w0BAQsFAAOCAQEAGD8iKf9U0F1XBIq13A8p
| 2TX7jI/+wl40kxWFP76SyezpIWEQrttWpIv5sYxypmDYpH+DZB3P2anLOpEuzQko
| ka2teP2qoF+JocZqAyP99/gDIipx9vQqB8Xf+sdKj2zoP2ryEGqQhGrj7GgNAmh0
| MLw98pm6MAdJ/EnlmnmHWk1ttAMUghP4dA0Xs8bBHZBHBVrEGqpmAiMbxZnJiCMc
| WZ0/lpYwznJ928YXAkEomPnIoU9J005y0GlfLqIudhMWz1CSzHaNUqKY/CuURkN7
| 6wcdQX/lz5TATsSTNPEwPGLPEqQv+HNckFJwU3lj/8VqrewXiiaSHd+Ys3KZjVvt
| wA==
|_-----END CERTIFICATE-----
3389/tcp  open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
|_ssl-date: 2026-10-26T13:52:35+00:00; 0s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: FINANCE404
|   NetBIOS_Domain_Name: FINANCE404
|   NetBIOS_Computer_Name: DC-404
|   DNS_Domain_Name: 404finance.local
|   DNS_Computer_Name: DC-404.404finance.local
|   DNS_Tree_Name: 404finance.local
|   Product_Version: 10.0.17763
|_  System_Time: 2026-10-26T13:51:55+00:00
| ssl-cert: Subject: commonName=DC-404.404finance.local
| Issuer: commonName=DC-404.404finance.local
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-10-25T13:44:16
| Not valid after:  2027-04-26T13:44:16
| MD5:     728e 4956 a5f6 00f9 85d2 b8d2 c5d5 6a33
| SHA-1:   61b4 0459 9e43 a258 9db0 11cc 04f1 675f 108c b7c8
| SHA-256: 6ea2 3639 25c6 4819 6511 ec46 de8d 6efa 693a 418f f68e 36fd bb02 8521 fe33 ad3d
| -----BEGIN CERTIFICATE-----
| MIIC8jCCAdqgAwIBAgIQEvK29BYMYbhD5VnxEEao3TANBgkqhkiG9w0BAQsFADAi
| MSAwHgYDVQQDExdEQy00MDQuNDA0ZmluYW5jZS5sb2NhbDAeFw0yNjEwMjUxMzQ0
| MTZaFw0yNzA0MjYxMzQ0MTZaMCIxIDAeBgNVBAMTF0RDLTQwNC40MDRmaW5hbmNl
| LmxvY2FsMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtcPZmc7BglBu
| z+PH8hc5O5uWrusgiddoybj65gh6QJbfEgdxo3valNFyL4ChmxSflH2Iu9lzBVAK
| Xh8eZ6UP8BH6rBcqmXUEME8rvJJQErFhhN4gWBTMPsSJG1fExdO78h2CN4g0pffs
| KC4l/twOIWnR0o4JrrIcBRKCFPXHZdOe6d0i28AkqduqNB1Dp+QZv8cp+7FX2UXh
| Ek149VnbhMoNouVvrPUUygOLMuYk0A68dKuT2Cghswmc5+EawCGGAZ75HUGqbKcV
| JBk2HaokWPigU3QN0fWyrmsNGg+AZ/rU1dT0Ud2PhHoUZdQIQ3/iQK60rKSNcGbD
| XZIt5P50vQIDAQABoyQwIjATBgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMC
| BDAwDQYJKoZIhvcNAQELBQADggEBAE+/Fj4CcZjs4eDRxgEYSa7L6K9UmxiGOZhL
| EGxZaRQBtAnyNlnlDpxreEGKdLWjinzcKPl1E7VBDgtOAGxvUpzq2mo9E4vzLJXZ
| 2CWuktcmf30QseDAQIXAQaPHV3HQNk57pK7gS6qUnE9enVF9RW2JBjOIucJz1W3g
| hGdmNJJrTt6LgNIlD/IEtSHU1mYjStpwmdBmICwo8PwnPJ1uEiDGazN0UfslgbYs
| yat922dtuSHEkhZN51Ec5V464J2XiYUmVGbKr5PazxwX6Tb4WDTGqEKfa2Ufiwgg
| RYL9cxFZDgsF8I9l9DSkmEVYQHdPMzMpV+sKUlsjL2MREAMwUFM=
|_-----END CERTIFICATE-----
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        syn-ack ttl 126 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49670/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
49671/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49679/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49700/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49718/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49734/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49829/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose

```



### Port 80 - HTTP&#x20;

Found team members names on the main webpage

<figure><img src="../.gitbook/assets/image (226).png" alt=""><figcaption></figcaption></figure>

With the help of kerbrute, able to determine whether the users are valid or not, by testing firstname.lastname format and it worked&#x20;

<figure><img src="../.gitbook/assets/image (227).png" alt=""><figcaption></figcaption></figure>

Upon enumerating more, found a .exe file in services, downloaded it and found a hash in the file&#x20;

<figure><img src="../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (230).png" alt=""><figcaption></figcaption></figure>

able to crack the password with john by decoding it with base64&#x20;

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

Did a password spray and found that user karl uses this password

<figure><img src="../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure>

### Bloodhound data collection&#x20;

I exploited a multi-step Active Directory ACL chain starting with the user karl, who held GenericWrite permissions over tom.reboot. Using this control, I forced a password reset on tom.reboot, logged in, and abused Tom's ForceChangePassword rights to take over the account of robert. Because robert possessed both password reset rights and the ability to add members to the Remote Desktop Users group, I added Robert to the group and successfully established an RDP session.

```
karl.hackermann--> tom.reboot-->robert.graef-->add robert to remote desktop users group
```



<figure><img src="../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (234).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (237).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

[https://www.revshells.com/](https://www.revshells.com/)   &#x20;

<figure><img src="../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure>

Leveraging the reverse shell payload, I gained full terminal access and located the profile for jan.tresor under C:\Users. Since the previous step granted me control over robert , who held ForceChangePassword rights over Jan, I reset Jan's password to pivot to their account. Inside Jan's Recycle Bin, I discovered deleted email files (.eml) containing the cleartext password for daniel.hoffmann

<figure><img src="../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (243).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - Winrm access as daniel.hoffmann

<figure><img src="../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (245).png" alt=""><figcaption></figcaption></figure>

After pivoting to Daniel's account, I utilized his ForceChangePassword privileges to take over the webadmin user, who belonged to the Web Admins group. Because the target web application was running locally on port 5000, I set up a port forwarding tunnel to access the webpage from my attack machine. This allowed me to leverage the compromised webadmin credentials against the newly exposed internal webpage.



<figure><img src="../.gitbook/assets/image (246).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (247).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (248).png" alt=""><figcaption></figcaption></figure>

### Local Port 5000 - HTTP

did a port forward to gain access to the port&#x20;

<figure><img src="../.gitbook/assets/image (251).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

Found a config zip, file which is password protected, used zip2john to crack it, and read the cleartext password for the user svc.services

<figure><img src="../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (255).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (257).png" alt=""><figcaption></figcaption></figure>

Found that svc.services is a member of certificate services&#x20;

<figure><img src="../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>



Found from earlier enumeration that robert.graef has permission on svc.services, since this account is disabled, with robert privilges can enable the svc.services account again&#x20;

<figure><img src="../.gitbook/assets/image (259).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (260).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (261).png" alt=""><figcaption></figcaption></figure>



Using Certipy-AD, I identified the vulnerable template vuln-esc4 by leveraging the svc.services user’s membership in the Certificate Services group. Because this group had write permissions, I altered the template configuration to allow a custom Subject Alternative Name. This allowed me to request a certificate as the Domain Administrator and successfully extracted admin NTLM hash



<figure><img src="../.gitbook/assets/image (262).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (263).png" alt=""><figcaption></figcaption></figure>



### Root.txt

<figure><img src="../.gitbook/assets/image (264).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (265).png" alt=""><figcaption></figcaption></figure>



