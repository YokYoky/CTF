CTFlearn

Digital Forensics 30pts Easy

Simple Steganography
Think the flag is somewhere in there. Would you help me find it? hint-" Steghide Might be Helpfull"

download the jpeg file

I used xdg-open to view the image and it looks normal minions image.

![Minions1](https://user-images.githubusercontent.com/89176758/196023086-800b6fe0-e2d2-4ce0-aeec-4557c2ec1a04.PNG)


After that, I used exiftool Minions1.jpeg and the two lines that caught my eye are the keywords: myadmin and the IPTC digest. I tried to based64 -d the IPTC but I didn't get any. 
So I used strings Minion1s.jpeg and then I noticed a familiar line, myadmin, and I knew this was related to the challenge. 
I re-read the challenge description to find more clues " Steghide Might be Helpful". I don't know anything about steghide, so I did my research, and based on my research it's a steganography tool. You can extract and encrypt a file.

I read a document about steghide https://linuxhint.com/steghide-beginners-tutorial/
in the documentation, there's a tutorial how to extract a file.

I used the example of the documentation 

steghide extract -sf Minions1.jpeg

After entering this command, it will ask for a passphrase. We already have a clue what a passphrase is. myadmin

i tried myadmin and it works. It gives me raw.txt file

Use cat command to view the txt file
and this give us a AEMAVABGAGwAZQBhAHIAbgB7AHQAaABpAHMAXwBpAHMAXwBmAHUAbgB9

Decode it by using base64
echo 'AEMAVABGAGwAZQBhAHIAbgB7AHQAaABpAHMAXwBpAHMAXwBmAHUAbgB9' | based64 -d

-d = decode

this give us the flag: CTFlearn{this_is_fun}
