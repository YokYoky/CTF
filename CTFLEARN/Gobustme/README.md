CTFLEARN WRITEUP
Gobustme

Some ghosts made this site 👻, it's a little spooky but theres a bunch of stuff hidden around.

gobustme.ctflearn.com

inside the site there's a video and a lyric of a ghost buster video.
in the lyric video there's two hyperlink which gobustme and common wordlist
![ctflearn_Gobustme_docu](https://user-images.githubusercontent.com/89176758/185881277-853a1107-af4d-4f6f-8ebb-7ab6da7af578.PNG)

in the gobuster link there's a tutorial about gobuster.
https://www.securitynewspaper.com/2019/11/04/bruteforce-any-website-with-gobuster-step-by-step-guide/
after reading the article you can find out how gobuster works.

after you know how it works then lets proceed to second hyperlink which is common wordlist.

you need to install gobuster in your terminal if your os dont have it.

Now use your knowledge about gobuster


gobuster dir -u https://gobustme.ctflearn.com/ -w common.txt

the command above is my take of the example in the gobuster site guide. You can experiment on your own.

after running the command your terminal will look like this
![ctflearn_Gobustme_docu_gobuster](https://user-images.githubusercontent.com/89176758/185882105-8ca5c905-436f-4afd-8fc3-2acf4e1f232f.PNG)

you see the results are bunch of url with directories.
with the help of these you can find the flag.


the flag is hidden in http://gobustme.ctflearn.com/hide/

Flag: CTFlearn{gh0sbu5t3rs_4ever}
