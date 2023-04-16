# Who is it
## tags: picoCTF 2023 Forensics email
### Author: Junias Bonou
#### 100 points
### Description
##### Someone just sent you an email claiming to be Google's co-founder Larry Page but you suspect a scam. Can you help us identify whose mail server the email actually originated from? Download the email file [here](https://artifacts.picoctf.net/c/499/email-export.eml). Flag: picoCTF{FirstnameLastname}

To identify who is the sender of this email, we can look at up in email header. In linux terminal I used less command to view the header of the email. Then searched for Received or Received from, this is where you can see the IP address of the sender.

Now, we can look it up the IP in whois. WHOIS is a public database that has list of all register domain name.

```console
$ whois 173.249.33.206
```
The command above will output alot of information, now search for the name of the original sender
```console
person:         Wilhelm Zwalina
address:        Contabo GmbH
address:        Aschauer Str. 32a
address:        81549 Muenchen
phone:          +49 89 21268372
fax-no:         +49 89 21665862
nic-hdl:        MH7476-RIPE
mnt-by:         MNT-CONTABO
mnt-by:         MNT-GIGA-HOSTING
created:        2010-01-04T10:41:37Z
last-modified:  2020-04-24T16:09:30Z
source:         RIPE
```
Flag: picoCTF{WilhelmZwalina}