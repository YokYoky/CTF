# PcapPoisoning
## tags: picoCTF 2023 Forensics pcap
### Author: Mubarak Mikail
#### 100 points
### Description
##### How about some hide and seek heh? Download this [file](https://artifacts.picoctf.net/c/376/trace.pcap) and find the flag.

Download the file by using wget.

Open the pcap file with wireshark.

Analyze each protocol by following stream.

In FTP protocol, we can see source IP 172.16.0.2 request to dst 10.253.0.6 username and password. this seems like FTP login connection.

analyze the FTP protocol by following TCP stream, then we have a TCP retransimission SYN going on. The flag is hidden in TCP protocol.

Flag: picoCTF{P64P_4N4L7S1S_SU55355FUL_f621fa37}

