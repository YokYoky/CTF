# Sleuthkit apprentice
## tags: picoCTF 2022 Forensics sleuthkit disk
#### 200 points
### Description
##### Download this disk image and find the flag. Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.

-   [Download compressed disk image](https://artifacts.picoctf.net/c/137/disk.flag.img.gz)

Download the compressed disk image then extract it using gzip command.

Use autopsy to analyze the disk image.
```console
sudo autopsy
[sudo] password for yoky: 

============================================================================

                       Autopsy Forensic Browser 
                  http://www.sleuthkit.org/autopsy/
                             ver 2.24 

============================================================================
Evidence Locker: /var/lib/autopsy
Start Time: Wed Mar 29 01:39:31 2023
Remote Host: localhost
Local Port: 9999

Open an HTML browser on the remote host and paste this URL in it:

    http://localhost:9999/autopsy

Keep this process running and use <ctrl-c> to exit
```
paste the link to your browser to use autopsy. Create a host and a case, then insert your image file.
![[Pasted image 20230329195821.png]]

Analyze each partition to find the flag. Choose File analysis from the tab, then enter flag keyword in File Name Search.
Found the flag in **mount** /3/ **name** disk.flag.img-360448-614399

![[Pasted image 20230329200207.png]]

check each file to find the flag. In /3/root/my_folder/flag.uni.txt
![[Pasted image 20230329200555.png]]
The ? seems like whitespaces. Use sed or tr command to remove whitespaces.
```console
$ echo " p i c o C T F { b y 7 3 _ 5 u r f 3 r _ a d a c 6 c b 4 } " | tr -d ' '           
picoCTF{by73_5urf3r_adac6cb4}
```
or
```console
$ echo " p i c o C T F { b y 7 3 _ 5 u r f 3 r _ a d a c 6 c b 4 } " | sed 's/ //g'        
picoCTF{by73_5urf3r_adac6cb4}
```
Flag: picoCTF{by73_5urf3r_adac6cb4}


