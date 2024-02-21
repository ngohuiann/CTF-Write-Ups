---
description: Wizlynx PwnTillDawn Stuntman Mike
---

# Stuntman Mike (10.150.150.166)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Sun Apr  4 10:07:29 2021 as: nmap -sS -A -p- -T4 -oN /root/machines/pwntilldawn/10.150.150.166/nmap.txt 10.150.150.166
Nmap scan report for 10.150.150.166
Host is up (0.17s latency).
Not shown: 65533 closed ports
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 7.6p1 (protocol 2.0)
| ssh-hostkey: 
|   2048 b7:9e:99:ed:7e:e0:d5:83:ad:c9:ba:7c:f1:bc:44:06 (RSA)
|   256 7e:53:59:7b:2d:6c:3b:d7:21:28:cb:cb:78:af:99:78 (ECDSA)
|_  256 c5:d2:2d:04:f9:69:40:4c:15:34:36:fe:83:1f:f3:44 (ED25519)
8089/tcp open  ssl/http Splunkd httpd
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Splunkd
|_http-title: splunkd
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Not valid before: 2019-10-25T09:15:13
|_Not valid after:  2022-10-24T09:15:13

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Apr  4 10:18:03 2021 -- 1 IP address (1 host up) scanned in 634.73 seconds
```
{% endcode %}
