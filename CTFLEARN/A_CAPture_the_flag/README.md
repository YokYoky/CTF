their are two ways to find the flag, wireshark or using string  

In wireshark, open wireshark, click open a capture a file then select the pcap file 
use http filter, examine the capture packet to find some possible key to flag 
we found GET /?msg=(based64) we know this is base64 because of / =
now decode it to string to get the flag 

flag{AFlagInPCAP}

2nd method use string 
strings flag\ \(4\) | grep -i "GET /" 
find the get /?msg=(base64) 

my first try is use the wireshark and use http filter after that i have no idea what to do next.  
I actually have no idea how i got the flag. with the help of some clue in comment section in ctflearn 
