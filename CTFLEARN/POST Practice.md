# POST Practice
## tags: CTFLearn Web Intelagent

#### 40 points Medium
### Description
This website requires authentication, via POST. However, it seems as if someone has defaced our site. Maybe there is still some way to authenticate? http://165.227.106.113/post.php

we can use cUrl to send HTTP POST request to the site. 
```
$ curl http://165.227.106.113/post.php
<h1>This site takes POST data that you have not submitted!</h1><!-- username: admin | password: 71urlkufpsdnlkadsf -->
```

It seems we need username and password data to get the flag. Use -d to include the data of username and password into the body of HTTP request

```
$ curl "http://165.227.106.113/post.php" -d "username=admin&password=71urlkufpsdnlkadsf"
<h1>flag{p0st_d4t4_4ll_d4y}</h1>
```

Or

We can also use Python to send HTTP request by importing request.
First, make it sure request is install
```
$ python -m pip install requests
```

Python script
``` python
#!/usr/bin/python3

import requests

url = "http://165.227.106.113/post.php"

# Data to be sent in the request body (if it's a POST request)
data = {
        'username': 'admin', 
        'password': '71urlkufpsdnlkadsf'
}

# Making a POST request with headers
response = requests.post(url, data=data)

print(response.text)
```