# Wireshark doo... doo... doo...
## tags: picoCTF 2021 Forensics
#### 50 points
### Description
##### Can you find the flag? [shark1.pcapng.](https://mercury.picoctf.net/static/0505a462ac9beb7412596855df280f6b/shark1.pcapng)

Download the pcap file then open the capture file in wireshark.

Filter the packet data by typing in the dialog box or go to analyze tab.

To filter to a particular stream, select Analyze tab -> Follow -> TCP stream

Find the flag in different streams. In stream 5 we see a look a like flag that its encoded.

The text looks like rot13, decode it by using rot13 command or tr command. In this case I used tr command to decode it.
[rot13 in tr command](https://en.wikipedia.org/wiki/ROT13)

```console
echo "Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
It will output:
```console
The flag is picoCTF{p33kab00_1_s33_u_deadbeef}
```

Flag: picoCTF{p33kab00_1_s33_u_deadbeef}