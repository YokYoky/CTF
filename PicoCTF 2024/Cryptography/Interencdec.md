# Interencdec
## tags: Cryptography, base64, browser_webshell_solvable, caesar

### Author: NGIRIMANA SCHADRACK
#### 50 points
### Description
Can you get the real meaning from this file.Download the file [here](https://artifacts.picoctf.net/c_titan/109/enc_flag).

Solution:

The encrypted flag is this `YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyMHdNakV5TnpVNGZRPT0nCg==` i tried to decode it in base64 and caesar cipher but it doesnt make sense, so i just experiment decoding until it make sense.

I used cyberchef to decode it better, i decode it first to base64 then to caesar cipher and increase the box height, until it make sense.

![[decode.png]]

It still doesn't make sense, so I try to decode it again to base64. Once I did this, it showing some result that i'm getting close. I just increase the box height until i got in 47, it result some curly bracket with words, i tried to submit it as a flag but it didn't work.

![[decode1.png]]

I experiment to decode it again to caesar cipher, I used different site to decode it. I increase the shift until to 85 that output the flag. 

![[decode2.png]]

**Flag:** picoCTF{caesar_d3cr9pt3d_f0212758}