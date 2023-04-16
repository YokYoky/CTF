# Hideme
## tags: picoCTF 2023 Forensics Steganography
### Author: Geoffrey Njogu
#### 100 points
### Description
##### Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here.](https://artifacts.picoctf.net/c/261/flag.png)

I open the image to know what the png file looks like, it seems like picoCTF logo.

I used exiftool to gather more information about this image. With exiftool we can see the metadata of the image, the metadata of flag.png is seems normal.

Now, I used strings command to know more about the image. We can notice secret/flag.png with strings command output. Use grep to filter out unnecessary info.
```console
$ strings flag.png | grep secret
secret/UT
secret/flag.pngUT
secret/UT
secret/flag.pngUT
```

Base from what we gather from strings command, we now know the image contains another image file. 

We can use binwalk to extract the embedded file image.
```console
$ binwalk -e flag.png 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2858, uncompressed size: 3015, name: secret/flag.png
42897         0xA791          End of Zip archive, footer length: 22

                                                                                               
┌──(yoky㉿yoky)-[~/ctf/picoCTF/Forensics/hideme_2023]
└─$ ls         
flag.png  _flag.png.extracted
```

cd to the extracted file
```console
$ cd _flag.png.extracted              
                                                                                               
┌──(yoky㉿yoky)-[~/…/picoCTF/Forensics/hideme_2023/_flag.png.extracted]
└─$ ls
29  29.zlib  9B3B.zip  secret
                                                                                               
┌──(yoky㉿yoky)-[~/…/picoCTF/Forensics/hideme_2023/_flag.png.extracted]
└─$ cd secret                     
                                                                                               
┌──(yoky㉿yoky)-[~/…/Forensics/hideme_2023/_flag.png.extracted/secret]
└─$ ls
flag.png
```

Open image by using xdg-open command, then we have our flag ![[Pasted image 20230413192004.png]]

Flag: picoCTF{Hiddinng_An_imag3_within_@n_ima9e_96539bea}
%b : November