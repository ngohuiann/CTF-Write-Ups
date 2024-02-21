---
description: Wizlynx PwnTillDawn Online Juno
---

# Juno (10.150.150.224)

## Nmap

{% code overflow="wrap" %}
```bash
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Apache2 Debian Default Page: It works
```
{% endcode %}

[http://10.150.150.224/login.php](http://10.150.150.224/login.php)

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Download JunoClient.apk and decompile it with jadx.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Password is stored in string variable "YouKnoWhat". Strings values can be found under Resources -> resources.arsc -> res -> values -> strings.xml.

### FLAG43

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### FLAG44

Login to http://10.150.150.224/login.php with the string.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### FLAG45

Identify the possible cipher [https://www.dcode.fr/cipher-identifier](https://www.dcode.fr/cipher-identifier)

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Try the one with the most possible result.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

