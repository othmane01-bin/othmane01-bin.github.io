---
layout: post
title:  "Hidden Deep Into my Heart"
date:   2026-03-9 20:05:27 -0500
categories: writeups
level: easy
points: 100
author: "othmane01"
tags: "tryhackme writeup"
---
![Image]({{ site.baseurl }}/images/startup/1.png)

**Hidden Deep Into my Heart** is a tryhackme easy challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [Startup](https://tryhackme.com/room/lafb2026e9)

# websiteo overview :

![Image]({{ site.baseurl }}/images/startup/2.png)

# RECON 

**cheking the robots.txt :**

![Image]({{ site.baseurl }}/images/startup/3.png)

hmmmm interesting! , ```` cupid_arrow_2026!!! ```` might be a potential cred.  let's save it for later.
 
![Image]({{ site.baseurl }}/images/startup/4.png)

**Gobuster:**

````
gobuster dir -u http://10.49.128.59:5000/cupids_secret_vault/ -w /usr/share/wordlists/dirb/common.txt -x txt,html,php --no-error -s "200,301" -b "" -t 64
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:            http://10.49.128.59:5000/cupids_secret_vault/
[+] Method:         GET
[+] Threads:        64
[+] Wordlist:       /usr/share/wordlists/dirb/common.txt
[+] Status codes:   200,301
[+] User Agent:     gobuster/3.8.2
[+] Extensions:     html,php,txt
[+] Timeout:        10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
administrator        (Status: 200) [Size: 2381]

````

**its looks like a login page :**

![Image]({{ site.baseurl }}/images/startup/5.png)

**try admin:admin to see how the application works:**

![Image]({{ site.baseurl }}/images/startup/6.png)

**The response:

![Image]({{ site.baseurl }}/images/startup/7.png)

lets' try the cred we've found earlier. 

![Image]({{ site.baseurl }}/images/startup/9.png)

**Et Voila ** 

>**flag** ''' THM{l0v3_is_in_th3_r0b0ts_txt}'''

**Special thanks to [Tryhackme](https://tryhackme.com)**

**that's it . see you next time**	

![Image]({{ site.baseurl }}/images/cat.jpeg)
