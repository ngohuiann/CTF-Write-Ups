---
description: Wizlynx PwnTillDawn Online ElMariachi-PC
---

# ElMariachi-PC (10.150.150.69)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Sun Apr  4 00:36:21 2021 as: nmap -sC -sV -A -T4 -p- -v -oN /root/machines/pwntilldawn/10.150.150.69/nmap.txt 10.150.150.69
Increasing send delay for 10.150.150.69 from 0 to 5 due to 51 out of 127 dropped probes since last increase.
Nmap scan report for 10.150.150.69
Host is up (0.17s latency).
Not shown: 65521 closed ports
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: ELMARIACHI-PC
|   NetBIOS_Domain_Name: ELMARIACHI-PC
|   NetBIOS_Computer_Name: ELMARIACHI-PC
|   DNS_Domain_Name: ElMariachi-PC
|   DNS_Computer_Name: ElMariachi-PC
|   Product_Version: 10.0.17763
|_  System_Time: 2021-04-03T17:52:02+00:00
| ssl-cert: Subject: commonName=ElMariachi-PC
| Issuer: commonName=ElMariachi-PC
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-04-02T15:41:36
| Not valid after:  2021-10-02T15:41:36
| MD5:   cab3 384e d469 d7fb 1611 bcac 2afb fc9b
|_SHA-1: 3e8f b423 16b3 a37a 19f6 9563 d9d8 44c3 2661 2137
|_ssl-date: 2021-04-03T17:52:32+00:00; +52m47s from scanner time.
5040/tcp  open  unknown
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
50417/tcp open  msrpc         Microsoft Windows RPC
60000/tcp open  unknown
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 401 Access Denied
|     Content-Type: text/html
|     Content-Length: 144
|     Connection: Keep-Alive
|     WWW-Authenticate: Digest realm="ThinVNC", qop="auth", nonce="gBcZbi6g5UDI4UcCLqDlQA==", opaque="m2yqFi2usv3AY2yatYSTRmyNPAplB8C1oC"
|_    <HTML><HEAD><TITLE>401 Access Denied</TITLE></HEAD><BODY><H1>401 Access Denied</H1>The requested URL requires authorization.<P></BODY></HTML>

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Apr  4 00:59:46 2021 -- 1 IP address (1 host up) scanned in 1406.22 seconds
```
{% endcode %}
