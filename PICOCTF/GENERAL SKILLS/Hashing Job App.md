Author: LT 'syreal' Jones       
# Description   
If you want to hash with the best, beat this test!

use nc command to connect to given address and port
```console
nc saturn.picoctf.net 50363
```

```console
Please md5 hash the text between quotes, excluding the quotes: 'armed robbery'
Answer:
```
Use online string to md5 hash converter or use python / bash script. Then enter the md5 hashed to terminal. Repeat the process until you get the flag.
```console
Please md5 hash the text between quotes, excluding the quotes: 'armed robbery'
Answer: 
986ad0db60b8d3d46281880f693a5926
986ad0db60b8d3d46281880f693a5926
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'bad dogs'
Answer: 
60cc96ffdc458c98395d6e7b6878a6e9
60cc96ffdc458c98395d6e7b6878a6e9
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'cleaning the bathroom'
Answer: 
0c8acab58314dbcf54dbc158470a8047
0c8acab58314dbcf54dbc158470a8047
Correct.
picoCTF{4ppl1c4710n_r3c31v3d_3eb82b73}
```

Below are the python and bash script

python script
```python
#!/usr/bin/env python3

import hashlib

while True:
        string = input("Enter string to convert to md5 hash (enter quit to quit): ") #input string
        hash = hashlib.md5(string.encode()) # convert the string to byte equivalent so it can be hash

        if string == "quit":
                break

        print(hash.hexdigest()) # returns encoded data to hexadecimal format
```

bash script
```bash
#!/usr/bin/env bash

while true
do
    read -p "Enter string to md5 hash: " string # inpit string
    echo -n $string | md5sum | awk '{print $string}' # print the md5 encoded string
done

```
Flag: picoCTF{4ppl1c4710n_r3c31v3d_3eb82b73}
