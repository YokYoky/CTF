# Challenge
Summoners Incantation

To awaken the ancient power of the Dragon's Heart, the summoners must combine magical incantation tokens. However, the tokens are delicate; no two adjacent tokens can be combined without losing their energy. The optimal incantation is the maximum sum obtainable by choosing non-adjacent tokens.

``` python
def max_energy(tokens):
    if not tokens:
        return 0
    if len(tokens) == 1:
        return tokens[0]

    prev2, prev1 = 0, tokens[0]
    for i in range(1, len(tokens)):
        current = max(prev1, tokens[i] + prev2)
        prev2, prev1 = prev1, current

    return prev1

# Example Usage
input_text = input().strip()
tokens = eval(input_text)  # Convert input string to list
print(max_energy(tokens))
```

![](HTB%20Apocalypse/coding/Summoners%20Incantation/assets/Pasted%20image%2020250321225629.png)