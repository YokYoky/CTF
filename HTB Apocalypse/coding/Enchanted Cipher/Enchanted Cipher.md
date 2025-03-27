# Challenge
Enchanted Cipher

The Grand Arcane Codex has been corrupted, altering historical records. Each entry has been encoded with a shifting cipher that changes every N characters. Your task is to decode a given string and restore the original message.

The Grand Arcane Codex has been corrupted, altering historical records. Each entry has been encoded with an **enchanted shifting cipher** that encrypts a plaintext composed of 3–7 randomly generated words.

The cipher operates as follows:

- Alphabetical characters are processed in groups of 5 (ignoring non-alphabetical characters).
- For each group, a random shift between 1 and 25 is chosen and applied to every letter in that group.
- After the encoded message, an additional line indicates the total number of shift groups, followed by another line listing the random shift values used for each group.

Your quest is to decode the given input and restore the original plaintext.

## Example

### Input

```
ibeqtsl
2
[4, 7]
```

### Output
```
example
```

First, I need to understand how the cipher works:

1. Characters are processed in groups of 5 alphabetical characters
2. Each group is shifted by a random value between 1-25
3. The input includes the ciphertext, number of shift groups, and the shift values used

For the example:

- Ciphertext: "ibeqtsl"
- Number of groups: 2
- Shift values: [4, 7]

Let's decode:

- Split into groups: "ibeqt", "sl"
- First group "ibeqt" with shift 4: Shifting back means subtracting 4
    - i → e (i - 4 = e)
    - b → x (b - 4 = x)
    - e → a (e - 4 = a)
    - q → m (q - 4 = m)
    - t → p (t - 4 = p)
- Second group "sl" with shift 7: Shifting back means subtracting 7
    - s → l (s - 7 = l)
    - l → e (l - 7 = e)

Combining: "examp" + "le" = "example"

```python
def decode_cipher(ciphertext, shifts):
    plaintext = ""
    alphabet = "abcdefghijklmnopqrstuvwxyz"
    
    # Count only alphabetical characters for grouping
    alpha_count = 0
    group_index = 0
    
    for char in ciphertext:
        if char.isalpha():
            # Determine which shift group this character belongs to
            if alpha_count % 5 == 0 and alpha_count > 0:
                group_index += 1
            
            # Get the shift value for this group
            shift = shifts[group_index]
            
            # Decrypt by shifting backwards (subtracting the shift value)
            char_lower = char.lower()
            pos = alphabet.index(char_lower)
            new_pos = (pos - shift) % 26
            new_char = alphabet[new_pos]
            
            # Maintain the original case
            if char.isupper():
                new_char = new_char.upper()
                
            plaintext += new_char
            alpha_count += 1
        else:
            plaintext += char
    
    return plaintext

# Read input
ciphertext = input()
num_groups = int(input())
shifts = eval(input())  # This reads the list of shift values

# Decode and print the result
decoded_text = decode_cipher(ciphertext, shifts)
print(decoded_text)
```

![[HTB Apocalypse/coding/Enchanted Cipher/assets/Pasted image 20250324173235.png]]