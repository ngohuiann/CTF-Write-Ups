# HackTheBox Pov Writeup
## Nmap
```
Nmap scan report for 10.10.11.251
Host is up, received user-set (0.014s latency).
Scanned at 2024-02-20 13:49:57 +08 for 155s
Not shown: 65534 filtered tcp ports (no-response)
PORT   STATE SERVICE REASON          VERSION
80/tcp open  http    syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-favicon: Unknown favicon MD5: E9B5E66DEBD9405ED864CAC17E2A888E
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-title: pov.htb
|_http-server-header: Microsoft-IIS/10.0
```

### LFI
![pov1](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/pov1.png)

dev.pov.htb download CV button generate this request:
```
POST /portfolio/default.aspx HTTP/1.1
Host: dev.pov.htb
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 373
Origin: http://dev.pov.htb
Connection: close
Referer: http://dev.pov.htb/portfolio/default.aspx
Upgrade-Insecure-Requests: 1

__EVENTTARGET=download&__EVENTARGUMENT=&__VIEWSTATE=DAsrQy2PiX5KXtsNF4kDsu5N%2BdzCpkMawb5RGKK2jE9Ib1cqLXmSkDJFVuSLpnFGy42fvDQIQ%2BM4UNG84A9ADXmHZV8%3D&__VIEWSTATEGENERATOR=8E0F0FA3&__EVENTVALIDATION=GU%2F9W%2BTIKmqI67CcoIuM9cVEupmKIkWHSIH7STIYe2%2F98bqu8u2yf9qPKhgQ2okH9EAcOgB243e%2BaS4XYn3bwjWrnH4g3ByuUxIOSQER88Q%2F4FAoE9FtdJH0jmKFG1ipF84l2g%3D%3D&file=index.aspx.cs
```
![pov2](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/pov2.png)

The file parameter is vulnerable to LFI, read source code by inserting default.aspx. It is shown that "../" is being sanitized. But we can bypass this with "....//" or just specified the full path (eg. C:\windows\win.ini)


