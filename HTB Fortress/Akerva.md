# Nmap
```bash
TCP
Nmap scan report for 10.13.37.11
Host is up, received user-set (0.20s latency).
Scanned at 2024-02-08 08:51:35 +08 for 1110s
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 0d:e4:41:fd:9f:a9:07:4d:25:b4:bd:5d:26:cc:4f:da (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCYsb2eP012xQGyABOzy+gWdxyHIa7xFBkwpLlFOBlYVsJp87Vtve02GudeSUjrz59c7y5nJkLxJAKQRXIObz/jzvCUkTMjH56Mc/3hzdkAzlWg/Gq3vNTyOLODkPPInJGGk1WgovnLcAJtNgdXaO7nYrDqyC8eCjBt7ppsONrz9FmEbiqLQl1m/LYb7Em6X1ZviytlJeH7eEk3UcKX45sNpzaUINdf1PJnXK3CLTB+vEAaieWz1GzCMsuRMphsmnW/d2ObpfZfCMa/NKYpAi0Z6yxUlI/HPEOWNnWO45OZ+7+M8NTxklZCHUbeCDhK8YSnpXtaEFPZvKajqZB+F2tR
|   256 f7:65:51:e0:39:37:2c:81:7f:b5:55:bd:63:9c:82:b5 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBEKLumcSSQuW4qihcz0zZyca/KvBaXlysVAvY/DqLV0vo4bPoz+PH0qP7vuSlgCIqdiyJKq5JFfJz58e4kujk90=
|   256 28:61:d3:5a:b9:39:f2:5b:d7:10:5a:67:ee:81:a8:5e (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINAqCT5KghTKGzjImXygZG4vYKvk0akCYJaonX3hXvkE
80/tcp   open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Root of the Universe &#8211; by @lydericlefebvre &amp; @akerva_fr
|_http-generator: WordPress 5.4-alpha-47225
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 6A6F2809F13E037DDC8D625B58FDA218
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
5000/tcp open  http    syn-ack ttl 63 Werkzeug httpd 0.16.0 (Python 2.7.15+)
| http-auth: 
| HTTP/1.0 401 UNAUTHORIZED\x0D
|_  Basic realm=Authentication Required
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
| http-methods: 
|_  Supported Methods: HEAD OPTIONS GET

UDP
Nmap scan report for 10.13.37.11
Host is up, received user-set (0.19s latency).
Scanned at 2024-02-08 08:51:36 +08 for 849s
Not shown: 91 closed udp ports (port-unreach)
PORT     STATE         SERVICE       REASON              VERSION
49/udp   open|filtered tacacs        no-response
161/udp  open          snmp          udp-response ttl 63 SNMPv1 server; net-snmp SNMPv3 server (public)
| snmp-info: 
|   enterprise: net-snmp
|   engineIDFormat: unknown
|   engineIDData: 423f5e76cd7abe5e00000000
|   snmpEngineBoots: 6
|_  snmpEngineTime: 3d03h15m38s
```

## Flag 1 Plain Sight
View source in the web application.

## Flag 2 Take a Look Around
```bash
snmpwalk -v 2c 10.13.37.11 -c public

[...SNIP...]
so.3.6.1.2.1.25.4.2.1.5.1230 = STRING: "-c /opt/check_devSite.sh"
iso.3.6.1.2.1.25.4.2.1.5.1231 = STRING: "/opt/check_backup.sh"
iso.3.6.1.2.1.25.4.2.1.5.1232 = STRING: "/opt/check_devSite.sh"
iso.3.6.1.2.1.25.4.2.1.5.1235 = STRING: "/var/www/html/scripts/backup_every_17minutes.sh AKERVA{IkN0w_SnMP@@@MIsconfigur@T!onS}"
iso.3.6.1.2.1.25.4.2.1.5.1236 = STRING: "/var/www/html/dev/space_dev.py"
iso.3.6.1.2.1.25.4.2.1.5.1241 = STRING: "/var/www/html/dev/space_dev.py"
iso.3.6.1.2.1.25.4.2.1.5.1243 = STRING: "--socket-activation"
[...SNIP...]
```
