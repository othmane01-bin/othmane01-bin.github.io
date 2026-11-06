---
layout: post
title:  "year-of-the-fox"
alias: "yotf"
date:   2026-11-05 21:05:27 -0500
categories: writeups
level: Hard
points: 90
author: "othmane01"
tags: "tryhackme writeup"
---

![Image]({{ site.baseurl }}/images/year-of-the-fox/1.png)

**year-of-the-fox** is a tryhackme Hard challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [year-of-the-fox](https://tryhackme.com/room/yotf)

# RECON :
As always i start enumarating the box with nmap to see the open ports , including the version of the services 

**Nmap output:**

````text
nmap -sCV -vv --top-ports 10000  10.128.161.230 -oN scan.nmap --reason 

Scanning 10.128.161.230 [8387 ports]
Discovered open port 139/tcp on 10.128.161.230
Discovered open port 80/tcp on 10.128.161.230
Discovered open port 445/tcp on 10.128.161.230

PORT    STATE SERVICE     REASON         VERSION
80/tcp  open  http        syn-ack ttl 62 Apache httpd 2.4.29
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=You want in? Gotta guess the password!
|_http-title: 401 Unauthorized
|_http-server-header: Apache/2.4.29 (Ubuntu)
139/tcp open  netbios-ssn syn-ack ttl 62 Samba smbd 3.X - 4.X (workgroup: YEAROFTHEFOX)
445/tcp open  netbios-ssn syn-ack ttl 62 Samba smbd 4.7.6-Ubuntu (workgroup: YEAROFTHEFOX)
Service Info: Hosts: year-of-the-fox.lan, YEAR-OF-THE-FOX

Host script results:
| smb2-time: 
|   date: 2026-11-05T19:36:55
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: year-of-the-fox
|   NetBIOS computer name: YEAR-OF-THE-FOX\x00
|   Domain name: lan
|   FQDN: year-of-the-fox.lan
|_  System time: 2026-11-05T19:36:55+00:00
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 0s, deviation: 1s, median: -1s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 62914/tcp): CLEAN (Couldn't establish connection (ERROR))
|   Check 2 (port 51472/tcp): CLEAN (Couldn't establish connection (ERROR))
|   Check 3 (port 60512/udp): CLEAN (Couldn't receive bytes: ERROR)
|   Check 4 (port 48273/udp): CLEAN (Couldn't receive bytes: ERROR)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| nbstat: NetBIOS name: YEAR-OF-THE-FOX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   YEAR-OF-THE-FOX<00>  Flags: <unique><active>
|   YEAR-OF-THE-FOX<03>  Flags: <unique><active>
|   YEAR-OF-THE-FOX<20>  Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   YEAROFTHEFOX<00>     Flags: <group><active>
|   YEAROFTHEFOX<1d>     Flags: <unique><active>
|   YEAROFTHEFOX<1e>     Flags: <group><active>
| Statistics:
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|_  00 00 00 00 00 00 00 00 00 00 00 00 00 00

````

what we get until now : 
- we might need a password in the web app in the port 80 since the hint says : **| HTTP/1.1 401 Unauthorized\x0D, Basic realm=You want in? Gotta guess the password!** .
- the os is ubuntu .
- the name of the box is : **year-of-the-fox**.
- the domain name is : **year-of-the-fox.lan**.
- login to smb anonymosly (guest) is enable . 
 
add the domain name to the /etc/hosts in your machine :
````bash
echo "ip year-of-the-fox.lan" |tee /etc/hosts
````
## SMB :
lets start by enum the smb :
````bash
smbclient -L //IP  -U ''
````
![Image]({{ site.baseurl }}/images/year-of-the-fox/2.png)

enum the shares using nxc : 
````bash
nxc smb IP -u "" -p ""  --shares
````
![Image]({{ site.baseurl }}/images/year-of-the-fox/3.png)

enum the users , found a valid user **fox**: 
````bash
nxc smb IP -u "" -p ""  --users
````
![Image]({{ site.baseurl }}/images/year-of-the-fox/4.png)

enum the password policy ,since i've a valid user i might brute force my way in if this is no other way.
keep in mind the : **Password Complexity Flags: 000000** means there is no enforce dor the standard password complexity rules , the password can be like :
- password
- password123
- Pa$$word123
anything biger than 5 char.

![Image]({{ site.baseurl }}/images/year-of-the-fox/5.png)

## WEB :
in order to get access the main page we do need to authenticate :

![Image]({{ site.baseurl }}/images/year-of-the-fox/6.png)

the request/responce in burp:

![Image]({{ site.baseurl }}/images/year-of-the-fox/7.png)

let's try to log in using admin:admin to see how the webapp handle the request : 

![Image]({{ site.baseurl }}/images/year-of-the-fox/8.png)

here is how the request looks like in Burp:

![Image]({{ site.baseurl }}/images/year-of-the-fox/9.png)

**the YWRtaW46YWRtaW4=** is base64 encode admin:admin

![Image]({{ site.baseurl }}/images/year-of-the-fox/10.png)

i did try to brute force the user fox but it was a dead end both smmb and http :
````bash
hydra  -l "fox" -P /usr/share/wordlists/rockyou.txt  smb://10.128.161.230
 hydra -l fox \     
-P /usr/share/wordlists/rockyou.txt \
10.128.161.230 \
http-get /
````
howerver i went back to that smb users enum this time i  use **enum4linux**

## SMB-v2.0

````bash
enum4linux 10.128.161.230 
````
**list of users:**
````text
fox
rascal
none
nobody
````

![Image]({{ site.baseurl }}/images/year-of-the-fox/11.png)
![Image]({{ site.baseurl }}/images/year-of-the-fox/12.png)

Let's try brute-forcing using those usernames :
````bash
 hydra -L users_list.txt \     
-P /usr/share/wordlists/rockyou.txt \
10.128.161.230 \
http-get /
````
that shit take a lot of time , go grap for yourself a cup of Coffee.
![Image]({{ site.baseurl }}/images/meme/coffee.png)

i had to reboot the box . the ip changes from **10.128.161.230** to **10.129.149.39**

here we go, i found a valid cred : 
````text
rascal:waterpolo
````
![Image]({{ site.baseurl }}/images/year-of-the-fox/13.png)

time for some injection!! 
![Image]({{ site.baseurl }}/images/year-of-the-fox/14.png)

I tried a few command injection attempts (such as `ls`), but it looks like certain commands are being filtered.

![Image]({{ site.baseurl }}/images/year-of-the-fox/15.png)

A possible way around this filter is to use Base64 encoding. Let's encode the `ls` command:

```bash
echo -n 'ls' | base64

# Output: bHM=
```

And it works! The filter doesn't seem to recognize the encoded command.

![Image]({{ site.baseurl }}/images/year-of-the-fox/16.png)

Getting a reverse shell should be straightforward now:

- Start a listener on our machine.
- Base64-encode a reverse shell command.
- Send the encoded payload through the injection point.
- Sit back and enjoy a well-deserved coffee while waiting for the connection!

TO-BE-CONT

**that's it guys i hope you found this useful .**

**Special thanks to [Tryhackme](https://tryhackme.com)**
	

![Image]({{ site.baseurl }}/images/cat.jpeg)