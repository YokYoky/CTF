# I Wont Let You Down
## Tags: Miscellaneous
**Author: @proslasher**
**50 points easy**

OK Go take a look at this IP:  
Connect here: [http://155.138.162.158](http://155.138.162.158) # USING ANY OTHER TOOL OTHER THAN NMAP WILL DISQUALIFY YOU. DON'T USE BURPSUITE, DON'T USE DIRBUSTER.

I clicked the site and I got rickroll. It also give a hint to use nmap

So i used nmap to the given ip
```console
$ nmap 155.138.162.158
```
it outputs open port 22, 25, 80, and 8888

I try one more time to scan the ip address with arguments
```console
$ sudo nmap -O -A 155.138.162.158
```
```console
8888/tcp open     sun-answerbook?
| fingerprint-strings: 
|   GetRequest: 
|     We're no strangers to love
|     know the rules and so do I (do I)
|     full commitment's what I'm thinking of
|     wouldn't get this from any other guy
|     just wanna tell you how I'm feeling
|     Gotta make you understand
|     Never gonna give you up
|     Never gonna let you down
|     Never gonna run around and desert you
|     Never gonna make you cry
|     Never gonna say goodbye
|     Never gonna tell a lie and hurt you
|     We've known each other for so long
|     Your heart's been aching, but you're too shy to say it (say it)
|     Inside, we both know what's been going on (going on)
|     know the game and we're gonna play it
|     feeling
|     Don't tell me you're too blind to see
|     Never gonna give you up
|     Never gonna let you down
|     Never gonna run around and desert you
|     Never gonna make you cry
|     Never gonna say goodbye
|     Never gonna tell a lie and hurt you
|     Never gonna give you up
|     Never gonna let you down
|     Never gonna run around and dese
|   NULL: 
|     We're no strangers to love
|     know the rules and so do I (do I)
|     full commitment's what I'm thinking of
|     wouldn't get this from any other guy
|     just wanna tell you how I'm feeling
|     Gotta make you understand
|     Never gonna give you up
|     Never gonna let you down
|     Never gonna run around and desert you
|     Never gonna make you cry
|     Never gonna say goodbye
|     Never gonna tell a lie and hurt you
|     We've known each other for so long
|     Your heart's been aching, but you're too shy to say it (say it)
|     Inside, we both know what's been going on (going on)
|     know the game and we're gonna play it
|     feeling
|     Don't tell me you're too blind to see
|     Never gonna give you up
|_    Never gonna let you down
```
the port 8888 has fingerprint-strings, the flag must be here somewhere, so i try to open it in my browser ip_address:port

once you open it in the browser the end of the strings there is a flag
**Flag:** flag{93671c2c38ee872508770361ace37b02}