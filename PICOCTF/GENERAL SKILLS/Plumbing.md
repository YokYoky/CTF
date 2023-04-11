# Plumbing
## tags: picoCTF 2021 General
#### 200 points
### Description
##### Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to jupiter.challenges.picoctf.org 7480.

Use the nc command to connect to jupiter.challenges.picoctf.org 7480
```console
nc jupiter.challenges.picoctf.org 7480
```
After connecting, it prints a lot of line of strings. To filter for the picoCTF{} we can use grep.

To use grep while doing nc command, we need to pipe "|"

Example of pipe:
```console
command 1 | command 2 | command 3
```
With the use of pipe we can get the flag by entering this command:
```console
nc jupiter.challenges.picoctf.org 7480 | grep "picoCTF{.*}"
```