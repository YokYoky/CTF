# Challenge
Elowen Moonsong, an Elven mage of great wisdom, has discovered an ancient scroll rumored to contain the location of The Dragon’s Heart. However, the scroll is enchanted with an old magical cipher, preventing Elowen from reading it.

![](assets/Pasted%20image%2020250321220922.png)
The challenge give us a executable file, lets open this in ghidra to analyze the file.
![](assets/Pasted%20image%2020250321220955.png)
In decrypt_message function, we can see how the file works. 
```
void decrypt_message(char *param_1)

{
  int iVar1;
  long in_FS_OFFSET;
  int local_3c;
  undefined8 local_38;
  undefined4 local_30;
  undefined4 uStack_2c;
  undefined4 uStack_28;
  undefined8 local_24;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  local_38 = 0x716e32747c435549;
  local_30 = 0x6760346d;
  uStack_2c = 0x6068356d;
  uStack_28 = 0x75327335;
  local_24 = 0x7e643275346e69;
  for (local_3c = 0; *(char *)((long)&local_38 + (long)local_3c) != '\0'; local_3c = local_3c + 1) {
    *(char *)((long)&local_38 + (long)local_3c) = *(char *)((long)&local_38 + (long)local_3c) + -1;
  }
  iVar1 = strcmp(param_1,(char *)&local_38);
  if (iVar1 == 0) {
    puts("The Dragon\'s Heart is hidden beneath the Eternal Flame in Eldoria.");
  }
  else {
    puts("The scroll remains unreadable... Try again.");
  }
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
```

```
local_38 = 0x716e32747c435549;
local_30 = 0x6760346d;
uStack_2c = 0x6068356d;
uStack_28 = 0x75327335;
local_24 = 0x7e643275346e69;
```
These variables contain the encrypted password.

```
for (local_3c = 0; *(char *)((long)&local_38 + (long)local_3c) != '\0'; local_3c = local_3c + 1) {
    *(char *)((long)&local_38 + (long)local_3c) = *(char *)((long)&local_38 + (long)local_3c) + -1;
}
```
The function decrements each byte of the stored password by `1` to get the correct password.

```python
import struct

# Encrypted hex values stored in memory
encrypted_hex = [
    0x716e32747c435549,
    0x6760346d,
    0x6068356d,
    0x75327335,
    0x7e643275346e69
]

# Convert to bytes and decrypt by subtracting 1 from each byte
decrypted_bytes = b''.join(
    struct.pack("<Q", value)[:8] if isinstance(value, int) and value >= 0x100000000 else struct.pack("<I", value)[:4]
    for value in encrypted_hex
)

# Reverse the +1 encryption by subtracting 1 from each byte safely
decrypted_bytes = bytes((b - 1) % 256 for b in decrypted_bytes)

# Convert to string
decrypted_flag = decrypted_bytes.decode(errors="ignore")
print(decrypted_flag)
```

```python
HTB{s1mpl3_fl4g_4r1thm3t1c}
```


### Step-by-Step Breakdown:

1. **Imports:**
``` python
import struct
```
- We import the `struct` module, which helps with packing and unpacking data into binary formats (like integers or floats) in Python. It allows us to convert numbers into byte representations.

2. Encrypted Hex Values:
```python
encrypted_hex = [
    0x716e32747c435549,
    0x6760346d,
    0x6068356d,
    0x75327335,
    0x7e643275346e69
]
```
- This list `encrypted_hex` contains the encrypted values in hexadecimal form.
    
- Each hexadecimal value represents an encoded byte sequence. The task is to decrypt these values to retrieve the original flag.

3. Converting Hex to Bytes:
``` python
decrypted_bytes = b''.join(
    struct.pack("<Q", value)[:8] if isinstance(value, int) and value >= 0x100000000 else struct.pack("<I", value)[:4]
    for value in encrypted_hex
)
```
- **`struct.pack("<Q", value)`**: The `struct.pack()` function converts an integer (`value`) into a binary representation.
    
    - **`<Q`**: The `<` character tells the pack function to use little-endian byte order. The `Q` character stands for an unsigned long long (8 bytes, 64 bits) integer.
        
- **`struct.pack("<I", value)`**: Similarly, the `<I` format is for packing a 4-byte (32-bit) unsigned integer.
    
- **`[:8]`** and **`[:4]`**: These slices ensure that we extract only the first 8 bytes (64-bit) for larger integers or 4 bytes (32-bit) for smaller integers from the packed values.
    
- **`.join(...)`**: This joins the byte sequences into one continuous byte string, which represents the encrypted flag.
    

In essence, this part of the code is transforming the 64-bit and 32-bit integer values from `encrypted_hex` into byte sequences. The decision of whether to use 4 or 8 bytes is based on the size of the integer.

4. Decrypting the Encrypted Bytes:
```python
decrypted_bytes = bytes((b - 1) % 256 for b in decrypted_bytes)
```
- **`(b - 1) % 256`**: Here, we decrypt the bytes by reversing the encryption step, which was assumed to have incremented each byte by 1.
    
    - Subtracting `1` undoes that step, but it might cause a byte to go below `0`. The `% 256` ensures that the byte wraps around correctly (i.e., it will always stay within the range of `0` to `255`).
        
    - This effectively undoes the transformation of each byte and restores the original values.
        
- **`bytes(...)`**: The result is converted back to a bytes object, which contains the decrypted flag.

5. Converting Bytes to String:
```python
decrypted_flag = decrypted_bytes.decode(errors="ignore")
```
- **`decode()`**: The `decode()` function converts the byte sequence back into a string.
    
- **`errors="ignore"`**: This argument tells Python to ignore any errors that occur if there are invalid byte sequences during the conversion. It's a safety measure to avoid breaking the program in case the bytes don't perfectly correspond to valid characters.