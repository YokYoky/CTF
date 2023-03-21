# Lookey here
## tags: picoCTF 2021 Forensics
#### 100 points
### Description
##### Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download the data [here.](https://artifacts.picoctf.net/c/124/anthem.flag.txt)

I used less command to see the contents of the file. The file has a lot of texts in it.

We need to filter for our flag by using grep command. Based on hint, search for known prefix for flag.

We know, known prefix flag in picoCTF is picoCTF{}

```console
cat anthem.flag.txt | grep picoCTF{.*}
```
The .* select all contents inside of a bracket.

The command above will output:
```console
we think that the men of picoCTF{gr3p_15_@w3s0m3_4c479940}
```
you can modify the command to remove the text before the flag.

**Flag: picoCTF{gr3p_15_@w3s0m3_4c479940}**