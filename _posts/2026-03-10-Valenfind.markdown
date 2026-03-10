---
layout: post
title:  "Valenfind"
date:   2026-03-10 01:05:27 -0500
categories: writeups
level: Medium
points: 200
author: "othmane01"
tags: "tryhackme writeup Valenfind walkthrough ctf "
---

![Image]({{ site.baseurl }}/images/Valenfind/1.png)

**Valenfind** is a tryhackme easy challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [Valenfind](https://tryhackme.com/room/lafb2026e10)


![Image]({{ site.baseurl }}/images/Valenfind/0.png)

## website overview :

![Image]({{ site.baseurl }}/images/Valenfind/2.png)

# RECON  :

**Gobuster :**

````
 gobuster dir -u http://10.49.141.114:5000  -w /usr/share/wordlists/dirb/common.txt -s "200,301" -b "" -t 64 --no-error
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:            http://10.49.141.114:5000
[+] Method:         GET
[+] Threads:        64
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,301
[+] User Agent:     gobuster/3.8.2
[+] Timeout:        10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
login                (Status: 200) [Size: 2682]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================


````

**lets' register a new account.** 

![Image]({{ site.baseurl }}/images/Valenfind/3.png)


**Dashboard overview :**

![Image]({{ site.baseurl }}/images/Valenfind/4.png)


**let's try to view some random profile to see what happend when we like it.**

![Image]({{ site.baseurl }}/images/Valenfind/5.png)

**let's press send valentine and intercept the request using a proxy (caido/burp/zap).**

![Image]({{ site.baseurl }}/images/Valenfind/5-1.png)

**The API calls an HTML theme file. Based on the hint suggesting the developer might be a vibe coder, there is a possibility that this feature is misconfigured. If proper validation is missing, it could lead to a path traversal vulnerability.**

>**Path Traversal** (also called Directory Traversal) is a web vulnerability that allows an attacker to access files outside the intended directory of a web application.

![Image]({{ site.baseurl }}/images/Valenfind/6.png)

**The error message reveals valuable information, including the root directory of the application. Knowing that the application is built with Python3, we can attempt to locate the app.py file to review the source code and better understand the application's behavior.**

![Image]({{ site.baseurl }}/images/Valenfind/7.png)

## .env file :

![Image]({{ site.baseurl }}/images/Valenfind/8.png)

## app.py file:

![Image]({{ site.baseurl }}/images/Valenfind/9.png)

**The app.py reveals :**

![Image]({{ site.baseurl }}/images/Valenfind/10.png)

![Image]({{ site.baseurl }}/images/Valenfind/11.png)


**we can dowload the db using :**

```
curl -H "ADMIN_API_KEY = "CUPID_MASTER_KEY_2024_XOXO" \ http://10.49.141.114:5000/api/admin/export_db -o cupid.db
```

 
**next is to see what we got on the db we've downloaded.**

![Image]({{ site.baseurl }}/images/Valenfind/12.png)

## THE FLAG :

````
THM{v1be_c0ding_1s_n0t_my_cup_0f_t3a}````

**Special thanks to [Tryhackme](https://tryhackme.com)**

**that's it . see you next time**	

![Image]({{ site.baseurl }}/images/cat.jpeg)
