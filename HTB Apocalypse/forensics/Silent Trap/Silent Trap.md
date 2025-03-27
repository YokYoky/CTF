# Challenge
Silent Trap

A critical incident has occurred in Tales from Eldoria, trapping thousands of players in the virtual world with no way to log out. The cause has been traced back to Malakar, a mysterious entity that launched a sophisticated attack, taking control of the developers' and system administrators' computers. With key systems compromised, the game is unable to function properly, which is why players remain trapped in Eldoria. Now, you must investigate what happened and find a way to restore the system, freeing yourself from the game before it's too late.

# Flags
1. What is the subject of the first email that the victim opened and replied to?

```
frame contains "email"
```
![](HTB%20Apocalypse/forensics/Silent%20Trap/assets/Pasted%20image%2020250323175149.png)
follow tcp the first one
![](HTB%20Apocalypse/forensics/Silent%20Trap/assets/Pasted%20image%2020250323175233.png)
![](HTB%20Apocalypse/forensics/Silent%20Trap/assets/Pasted%20image%2020250323175332.png)

```
Game Crash on Level 5
```

2. On what date and time was the suspicious email sent? (Format: YYYY-MM-DD_HH:MM) (for example: 1945-04-30_12:34)
based from earlier, `shadowblade@email.com` must be the suspicious email. Filter it then follow the first tcp 
![](HTB%20Apocalypse/forensics/Silent%20Trap/assets/Pasted%20image%2020250323180128.png)
![](HTB%20Apocalypse/forensics/Silent%20Trap/assets/Pasted%20image%2020250323180258.png)
```
2025-02-24_15:46
```

2. What is the MD5 hash of the malware file?
	 i found the malware but i got stuck getting the md5 hash because the file is password protected. After the event ended, reading from other writeup the password is already in front of my eyes. Lesson learned, Think critically and observe more.

3. What credentials were used to log into the attacker's mailbox? (Format: username:password)

4. What is the name of the task scheduled by the attacker?

5. What is the API key leaked from the highly valuable file discovered by the attacker?