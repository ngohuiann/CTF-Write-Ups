# Vega (10.150.150.222)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Tue Apr  6 10:59:11 2021 as: nmap -sS -A -p- -T4 -v -oN machines/pwntilldawn/10.150.150.222/nmap.txt 10.150.150.222
Increasing send delay for 10.150.150.222 from 0 to 5 due to 1481 out of 3702 dropped probes since last increase.
Nmap scan report for 10.150.150.222
Host is up (0.30s latency).
Not shown: 65531 closed ports
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 af:56:59:c5:9a:de:f4:a9:b7:8f:34:4b:a2:21:24:71 (RSA)
|   256 1b:e8:16:d4:dc:a6:7a:3e:5d:6f:f2:95:5a:59:08:9a (ECDSA)
|_  256 9c:35:dd:da:ee:a9:b4:0b:55:68:45:fd:8f:85:35:30 (ED25519)
80/tcp    open  http     Apache httpd 2.4.29 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 643D3106699AA425269DBE0BB7768440
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Home Page
8089/tcp  open  ssl/http Splunkd httpd
| http-methods: 
|_  Supported Methods: GET HEAD OPTIONS
|_http-title: splunkd
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Issuer: commonName=SplunkCommonCA/organizationName=Splunk/stateOrProvinceName=CA/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2019-10-25T09:19:54
| Not valid after:  2022-10-24T09:19:54
| MD5:   536b fb1f 1fc1 e54d 822f b12d 650d 734a
|_SHA-1: e879 2227 39ad 966f aa5b 26a1 4701 cef0 06b5 2a5c
10000/tcp open  http     MiniServ 1.941 (Webmin httpd)
|_http-favicon: Unknown favicon MD5: 7EFDCFA0F0F7B6D238CC297C038144D4
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Apr  6 11:22:26 2021 -- 1 IP address (1 host up) scanned in 1395.67 second
```
{% endcode %}
