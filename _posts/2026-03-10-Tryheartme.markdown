---
layout: post
title:  "Tryheartme"
date:   2026-03-10 00:05:27 -0500
categories: writeups
level: easy
points: 100
author: "othmane01"
tags: "tryhackme writeup Tryheartme walkthrough ctf "
---

![Image]({{ site.baseurl }}/images/tryheartme/1.png)

**Tryheartme** is a tryhackme easy challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [Tryheartme](https://tryhackme.com/room/lafb2026e5)

## website overview :

![Image]({{ site.baseurl }}/images/tryheartme/2.png)

# RECON 



**Gobuster:**

````
gobuster dir -u http://10.49.134.49:5000 -x php,txt,zip,html  -w /usr/share/wordlists/dirb/common.txt -s "200,301" -b "" -t 64 --no-error
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:            http://10.49.134.49:5000
[+] Method:         GET
[+] Threads:        64
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,301
[+] User Agent:     gobuster/3.8.2
[+] Extensions:     php,txt,zip,html
[+] Timeout:        10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
login                (Status: 200) [Size: 1461]
register             (Status: 200) [Size: 1517]

````

**let's try to login using a random creds**

![Image]({{ site.baseurl }}/images/tryheartme/3.png)

**The response:**

![Image]({{ site.baseurl }}/images/tryheartme/4.png)

**lets' try the creating a new account.** 

![Image]({{ site.baseurl }}/images/tryheartme/5.png)

**Nice looks like the webapp use JWT cookie to verify our session**

>**JWT cookie** is simply a cookie that stores a JSON Web Token (JWT). It is often used by web applications for authentication and session management

**lets use cyberchef to decode it** 

![Image]({{ site.baseurl }}/images/tryheartme/6.png)

**we can use cyberchef again to sign a JWT , with the claims(data) we want.**

![Image]({{ site.baseurl }}/images/tryheartme/7.png)

**press F12>Storage , update the cookie and then refrech the page .**

![Image]({{ site.baseurl }}/images/tryheartme/8.png)

![Image]({{ site.baseurl }}/images/tryheartme/9.png)

**we can press buy on the ValenFlag product to revile te flag.**

![Image]({{ site.baseurl }}/images/tryheartme/10.png)

**Et Voila ** 

# FLAG :

```` THM{v4l3nt1n3_jwt_c00k13_t4mp3r_4dm1n_sh0p} ````

**Special thanks to [Tryhackme](https://tryhackme.com)**

**that's it . see you next time**	

![Image]({{ site.baseurl }}/images/cat.jpeg)
