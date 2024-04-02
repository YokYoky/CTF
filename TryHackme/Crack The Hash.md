# Level 2

This task increases the difficulty. All of the answers will be in the classic [rock you](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) password list.

You might have to start using hashcat here and not online tools. It might also be handy to look at some example hashes on [hashcats page](https://hashcat.net/wiki/doku.php?id=example_hashes).

#### Hash: F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85

solution: 

First, i check what kind of hash algo is the given hash, [Hash analyzer](https://hashes.com/en/tools/hash_identifier) the has type is SHA-256.

with the help of hashcat we can crack this hash, 1400 is the hash mode of SHA-256 in hashcat. Save the hash in txt file.


`hashcat -m 1400 -a 0 hash.txt /usr/share/wordlists/rockyou.txt`

output:
```
f09edcb1fcefc6dfb23dc3505a882655ff77375ed8aa2d1c13f640fccc2d0c85:paule
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 1400 (SHA2-256)
Hash.Target......: f09edcb1fcefc6dfb23dc3505a882655ff77375ed8aa2d1c13f...2d0c85
Time.Started.....: Sun Mar 31 20:40:58 2024 (0 secs)
Time.Estimated...: Sun Mar 31 20:40:58 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:   273.2 kH/s (0.57ms) @ Accel:512 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 78848/14344384 (0.55%)
Rejected.........: 0/78848 (0.00%)
Restore.Point....: 77824/14344384 (0.54%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: superhot -> jasonf
Hardware.Mon.#1..: Temp: 62c Util: 78%

Started: Sun Mar 31 20:39:43 2024
Stopped: Sun Mar 31 20:41:01 2024
```

**Answer:** paule

--------------------------------------------------------------------
#### Hash: 1DFECA0C002AE40B8619ECF94819CC1B

solution:

based from [Hash analyzer](https://hashes.com/en/tools/hash_identifier) the Possible algorithms: NTLM
`$ hashcat -m 1000 hashh.txt /usr/share/wordlists/rockyou.txt`

output:
```
1dfeca0c002ae40b8619ecf94819cc1b:n63umy8lkf4i             
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 1000 (NTLM)
Hash.Target......: 1dfeca0c002ae40b8619ecf94819cc1b
Time.Started.....: Sun Mar 31 21:52:30 2024 (3 secs)
Time.Estimated...: Sun Mar 31 21:52:33 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  1688.1 kH/s (0.21ms) @ Accel:512 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 5239808/14344384 (36.53%)
Rejected.........: 0/5239808 (0.00%)
Restore.Point....: 5238784/14344384 (36.52%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: n6rebel9 -> n4any451
Hardware.Mon.#1..: Temp: 64c Util: 58%

Started: Sun Mar 31 21:51:56 2024
Stopped: Sun Mar 31 21:52:35 2024
```

**Answer:** n63umy8lkf4i

--------------------------
#### Hash: `$6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.`
Salt: aReallyHardSalt

solution: 

based from [Hash analyzer](https://hashes.com/en/tools/hash_identifier) the Possible algorithms: sha512crypt $6$, SHA512 (Unix). 1800 hash mode

**Answer:** waka99

-------------------------------------------
#### Hash: e5d8870e5bdd26602cab8dbe07a942c8669e56d6

Salt: tryhackme

solution:

sha1 with salt
`hashcat -m 110 e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme /usr/share/wordlists/rockyou.txt`

**Answer:** 481616481616