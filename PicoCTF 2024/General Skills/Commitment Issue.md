# Commitment Issue
## tags: General Skills, browser_webshell_solvable, git

### Author: Jeffery John
#### 50 points
### Description
I accidentally wrote the flag down. Good thing I deleted it!You download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/137/challenge.zip)

Solution:
unzip the file, the txt file says TOP SECRET.

Based from git log
![[gitlog.png]]
The flag is created then removed, 

`git reset --hard HEAD~1`
after using this git command, it go back to where before your commit

the file now return the flag.
**Flag:** picoCTF{s@n1t1z3_cf09a485}