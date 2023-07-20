# FindandOpen
## tags: picoCTF 2023 Forensics
### Author: Mubarak Mikail
#### 100 points
### Description
##### Someone might have hidden the password in the trace file. Find the key to unlock this [file](https://artifacts.picoctf.net/c/493/flag.zip). [This tracefile](https://artifacts.picoctf.net/c/493/dump.pcap) might be good to analyze.

i open the pcap file in wireshark to analyze the packet.

from there, the ethernet protocol has interesting strings.

use string command to output the strings of the pcap file.

combine each string then decode it

you got half the flag

use the flag to enter the password for zip file

then you complete the flag
