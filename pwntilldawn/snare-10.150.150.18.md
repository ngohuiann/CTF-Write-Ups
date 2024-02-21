---
description: Wizlynx PwnTillDawn Online Snare
---

# Snare (10.150.150.18)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Sat Apr  3 17:09:09 2021 as: nmap -sS -A -p- -T4 -oN machines/pwntilldawn/10.150.150.18/nmap.txt 10.150.150.18
Nmap scan report for 10.150.150.18
Host is up (0.16s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 2f:0e:73:d4:ae:73:14:7e:c5:1c:15:84:ef:45:a4:d1 (RSA)
|   256 39:0b:0b:c9:86:c9:8e:b5:2b:0c:39:c7:63:ec:e2:10 (ECDSA)
|_  256 f6:bf:c5:03:5b:df:e5:e1:f4:da:ac:1e:b2:07:88:2f (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-title: Welcome to my homepage!
|_Requested resource was /index.php?page=home
# Nmap done at Sat Apr  3 17:17:47 2021 -- 1 IP address (1 host up) scanned in 518.08 seconds
```
{% endcode %}

