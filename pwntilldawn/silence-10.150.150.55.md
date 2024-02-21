---
description: Wizlynx PwnTillDawn Online Silence
---

# Silence (10.150.150.55)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Mon Apr  5 17:06:04 2021 as: nmap -sS -A -p- -T4 -v -oN machines/pwntilldawn/10.150.150.55/nmap.txt 10.150.150.55
Increasing send delay for 10.150.150.55 from 0 to 5 due to 1705 out of 4261 dropped probes since last increase.
Nmap scan report for 10.150.150.55
Host is up (0.29s latency).
Not shown: 65530 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd
80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
139/tcp  open  netbios-ssn Samba smbd 4.6.2
445/tcp  open  netbios-ssn Samba smbd 4.6.2
1055/tcp open  ssh         OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Apr  5 17:31:11 2021 -- 1 IP address (1 host up) scanned in 1507.98 seconds
```
{% endcode %}
