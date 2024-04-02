ai# Scan Surprise
## tags: Forensics, file_format, polyglot

### Author: MUBARAK MIKAIL
#### 100 points
### Description
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf).

Solution:

The file looks like an pdf format, but looking the metadata of the file it says PNG image.

Normally opening the file gives the 2nd part of the flag `1n_pn9_&_pdf_724b1287}`.

![[2ndflag.png]]

To get the 1st part of the flag, I rename the file `mv filename.pdf flag.png`

![[1stflag.png]]

Renaming the file will give the 1st part of the flag, open the renamed file to get the 1st part of the flag.

picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}