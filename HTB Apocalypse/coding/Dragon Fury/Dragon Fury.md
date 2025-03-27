# Challenge
Dragon Fury

In the final confrontation, the dragons unleash their fury against Malakar’s forces. Simulate the battle by computing the total damage dealt over successive rounds until victory is achieved.

```python
def find_valid_combination(damage_rounds, target_damage):

    def dfs(index, current_sum, current_combination):

        if index == len(damage_rounds):

            if current_sum == target_damage:

                return current_combination

            else:

                return None

        for damage in damage_rounds[index]:

            result = dfs(index + 1, current_sum + damage, current_combination + [damage])

            if result:

                return result

        return None

  

    return dfs(0, 0, [])

  

# Read the input

input_text = input()  # Example input: [[13, 15, 27, 17], [24, 15, 28, 6, 15, 16], [7, 25, 10, 14, 11], [23, 30, 14, 10]]

target_damage = int(input())  # Example input: 77

  

# Convert the input string to a list of lists

import ast

damage_rounds = ast.literal_eval(input_text)

  

# Find the valid combination

valid_combination = find_valid_combination(damage_rounds, target_damage)

  

# Output the result

print(valid_combination)
```

![[HTB Apocalypse/coding/Dragon Fury/assets/Pasted image 20250322232154.png]]