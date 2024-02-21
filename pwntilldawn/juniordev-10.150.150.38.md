---
description: Wizlynx PwnTillDawn Online JuniorDev
---

# JuniorDev (10.150.150.38)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Sat Apr  3 21:09:56 2021 as: nmap -sS -A -p- -T4 -v -oN machines/pwntilldawn/10.150.150.38/nmap.txt 10.150.150.38
Increasing send delay for 10.150.150.38 from 0 to 5 due to 1297 out of 3242 dropped probes since last increase.
Nmap scan report for 10.150.150.38
Host is up (0.16s latency).
Not shown: 65533 closed ports
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 64:63:02:cb:00:44:4a:0f:95:1a:34:8d:4e:60:38:1c (RSA)
|   256 0a:6e:10:95:de:3d:6d:4b:98:5f:f0:cf:cb:f5:79:9e (ECDSA)
|_  256 08:04:04:08:51:d2:b4:a4:03:bb:02:71:2f:66:09:69 (ED25519)
30609/tcp open  http    Jetty 9.4.27.v20200227
|_http-favicon: Unknown favicon MD5: 23E8C7BD78E8CD826C5A6073B15068B1
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Jetty(9.4.27.v20200227)
|_http-title: Site doesn't have a title (text/html;charset=utf-8).

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Apr  3 21:20:28 2021 -- 1 IP address (1 host up) scanned in 632.88 seconds
```
{% endcode %}
