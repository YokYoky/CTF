# Where am i?
## Tags: OSINT
**Author: @proslasher**
**50 points easy**

Your friend thought using a JPG was a great way to remember how to login to their private server. Can you find the flag?

Download the attached file.

I used exiftool to examine the jpg file, the image description caught my interest, so i tried to decode it and it give me a flag.
```console
$ exiftool PXL_20230922_231845140_2.jpg 
ExifTool Version Number         : 12.57
File Name                       : PXL_20230922_231845140_2.jpg
Directory                       : .
File Size                       : 1641 kB
File Modification Date/Time     : 2023:10:09 21:04:25+08:00
File Access Date/Time           : 2023:10:09 21:08:47+08:00
File Inode Change Date/Time     : 2023:10:09 21:04:26+08:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Little-endian (Intel, II)
Image Description               : ZmxhZ3tiMTFhM2YwZWY0YmMxNzBiYTk0MDljMDc3MzU1YmJhMik=
```
**Flag:** flag{b11a3f0ef4bc170ba9409c077355bba2)