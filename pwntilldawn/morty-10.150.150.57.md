---
description: Wizlynx PwnTillDawn Online Morty
---

# Morty (10.150.150.57)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Mon Apr  5 16:32:05 2021 as: nmap -sS -A -p- -T4 -v -oN machines/pwntilldawn/10.150.150.57/nmap.txt 10.150.150.57
Nmap scan report for 10.150.150.57
Host is up (0.27s latency).
Not shown: 65532 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e8:60:09:66:aa:1f:e8:76:d8:84:16:18:1c:e4:ee:32 (RSA)
|   256 92:09:d3:0e:f9:47:48:03:9f:32:9f:0f:17:87:c2:a4 (ECDSA)
|_  256 1d:d1:b3:2b:24:dc:c2:8a:d7:ca:44:39:24:c3:af:3d (ED25519)
53/tcp open  domain  ISC BIND 9.16.1 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.16.1-Ubuntu
80/tcp open  http    Apache httpd 2.4.41
| http-ls: Volume /
| SIZE  TIME              FILENAME
| 147   2020-06-10 11:25  note.html
|_
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Index of /

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Apr  5 16:41:19 2021 -- 1 IP address (1 host up) scanned in 554.79 seconds
```
{% endcode %}
