# Verify
## tags: Forensics, browser_webshell_solvable, checksum, grep

### Author: Jeffery John
#### 50 points
### Description
People keep trying to trick my players with imitation flags. I want to make sure they get the real thing! I'm going to provide the SHA-256 hash and a decrypt script to help you know that my flags are legitimate.You can download the challenge files here:

[challenge.zip](https://artifacts.picoctf.net/c_rhea/21/challenge.zip)

The same files are accessible via SSH here:`ssh -p 56673 ctf-player@rhea.picoctf.net`Using the password `84b12bae`. Accept the fingerprint with `yes`, and `ls` once connected to begin. Remember, in a shell, passwords are hidden!

- Checksum: 3ad37ed6c5ab81d31e4c94ae611e0adf2e9e3e6bee55804ebc7f386283e366a4
- To decrypt the file once you've verified the hash, run `./decrypt.sh files/<file>`.

I download the file for easy access, we are given decrypt.sh script, checksum.txt, and files.

Inside of folder `files` there are a lot of files that are SHA-256 hash. I modify the given decrypt.sh that can decode all files.
```
#!/bin/bash

# Check if the user provided a folder name as an argument
if [ $# -eq 0 ]; then
    echo "Expected usage: decrypt.sh <folder>"
    exit 1
fi

# Store the provided folder name in a variable
folder_name="$1"

# Check if the provided argument is a directory
if [ ! -d "$folder_name" ]; then
    echo "Error: '$folder_name' is not a valid directory. Please provide a valid directory."
    exit 1
fi

# Iterate through each file in the folder
for file in "$folder_name"/*; do
    # Check if the item is a file
    if [ -f "$file" ]; then
        # Decrypt the file
        decrypted_content=$(openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -salt -in "$file" -k picoCTF 2>/dev/null)
        # Check if decryption was successful and if the decrypted content contains "picoCTF"
        if [ $? -eq 0 ] && echo "$decrypted_content" | grep -q "picoCTF"; then
            echo "$decrypted_content"
            echo ""
        fi
    fi
done
```

I moved the new bash script into `files` folder then execute it `$ ./decrypt.sh .
`
**Flag:** picoCTF{trust_but_verify_e018b574}