# Sleuthkit intro
## tags: picoCTF 2022 Forensics sleuthkit
#### 100 points
### Description
##### Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

-   [Download disk image](https://artifacts.picoctf.net/c/164/disk.img.gz)
-   Access checker program: `nc saturn.picoctf.net 52472`

Download the disk image. The file has .gz extension, you can extract it by using gzip command.
```console
gzip -d disk.img.gz
```
Now it decompressed to disk.img.
To find the size of a Linux partition, we need to use mmls sleuthkit. We can use the mmls command directly without arguments because it will autodetect.
```console
mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```
By using mmls, we can see the layout of the actual disk. There are two types of disk images: physical and logical. The physical disk image is where you can see the entire disk or partition, like in the output above. While the logical disk image only outputs the data that has not been deleted.

The Linux row must be our key to get the flag. Now connect to `saturn.picoctf.net 52472` by using netcat command.
```console
nc saturn.picoctf.net 52472
What is the size of the Linux partition in the given disk image?
Length in sectors
```
The checker is looking for length in sectors. We can look back to our mmls to get the length. `0000202752`, enter the value size to get the flag.
```console
What is the size of the Linux partition in the given disk image?
Length in sectors: 0000202752
0000202752
Great work!
picoCTF{mm15_f7w!}
```
Flag: picoCTF{mm15_f7w!}