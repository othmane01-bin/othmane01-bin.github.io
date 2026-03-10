---
layout: post
title:  "Love Letter Locker"
date:   2026-03-10 01:05:27 -0500
categories: writeups
level: easy
points: 100
author: "othmane01"
tags: "tryhackme writeup Tryheartme walkthrough ctf "
---

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/0.png)

**Love Letter Locker** is a tryhackme easy challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [Tryheartme](https://tryhackme.com/room/lafb2026e2)

## website overview :

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/1.png)

# RECON 


**Gobuster:**

````
gobuster dir -u http://10.49.182.19:5000/   -w /usr/share/wordlists/dirb/common.txt -s "200,301" -b "" -t 64 --no-error   
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:            http://10.49.182.19:5000/
[+] Method:         GET
[+] Threads:        64
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   301,200
[+] User Agent:     gobuster/3.8.2
[+] Timeout:        10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
login                (Status: 200) [Size: 1017]
register             (Status: 200) [Size: 1048]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================

````

**let's try to login using a admin:admin creds**

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/2.png)


**The response:**

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/3.png)


**lets' try to register a new account. and then Login** 

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/4.png)

**After creating a new letter and opening it, we can see the path where it is stored. By modifying the identifier in the request, it may be possible to access other users’ letters. This suggests the presence of an IDOR (Insecure Direct Object Reference) vulnerability, where the application fails to enforce proper access control on object references.**

### - creating a new Letter:

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/5.png)

### - Opening the letter we've created :

![Image]({{ site.baseurl }}/images/Love_Letter_Locker/6.png)

## THE FLAG 
![Image]({{ site.baseurl }}/images/Love_Letter_Locker/7.png)


```` THM{1_c4n_r3ad_4ll_l3tters_w1th_th1s_1d0r}````

**Special thanks to [Tryhackme](https://tryhackme.com)**

**that's it . see you next time**	

![Image]({{ site.baseurl }}/images/cat.jpeg)
