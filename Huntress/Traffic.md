# Traffic
## Tags: Forensics
**Author: @JohnHammond**
**50 points medium**

We saw some communication to a sketchy site... here's an export of the network traffic. Can you track it down?  
  
Some tools like [`rita`](https://github.com/activecm/rita) or [`zeek`](https://github.com/zeek/zeek) might help dig through all of this data!

download the attached file

I did not use tool mention above. What i did is extract the traffic.7z
```console
$ 7z e traffic.7z
$ ls
capture_loss.00:00:00-01:00:00.log.gz    notice.00:00:00-01:00:00.log.gz
capture_loss.01:00:00-02:00:00.log.gz    notice.01:00:00-02:00:00.log.gz
capture_loss.02:16:42-03:00:00.log.gz    notice.02:20:05-03:00:00.log.gz
capture_loss.03:00:00-03:53:19.log.gz    notice.03:00:00-03:53:19.log.gz
capture_loss.03:53:19-03:53:21.log.gz    ocsp.00:00:00-01:00:00.log.gz
conn.00:00:00-01:00:00.log.gz            ocsp.01:00:00-02:00:00.log.gz
conn.01:00:00-02:00:00.log.gz            ocsp.02:00:00-02:01:50.log.gz
conn.02:00:00-02:01:50.log.gz            ocsp.02:16:08-03:00:00.log.gz
conn.02:15:56-03:00:00.log.gz            ocsp.03:00:00-03:53:19.log.gz
conn.03:00:00-03:53:19.log.gz            packet_filter.02:15:42-03:00:00.log.gz
conn.03:53:19-03:53:21.log.gz            reporter.00:00:00-01:00:00.log.gz
conn-summary.00:00:00-01:00:00.log.gz    reporter.03:53:19-03:53:19.log.gz
conn-summary.01:00:00-02:00:00.log.gz    software.02:15:51-03:00:00.log.gz
conn-summary.02:00:00-02:01:50.log.gz    ssl.00:00:00-01:00:00.log.gz
conn-summary.02:15:56-03:00:00.log.gz    ssl.01:00:00-02:00:00.log.gz
conn-summary.03:00:00-03:53:19.log.gz    ssl.02:00:00-02:01:50.log.gz
conn-summary.03:53:19-03:53:21.log.gz    ssl.02:15:47-03:00:00.log.gz
dns.00:00:00-01:00:00.log.gz             ssl.03:00:00-03:53:19.log.gz
dns.01:00:00-02:00:00.log.gz             stats.00:00:00-01:00:00.log.gz
dns.02:00:00-02:01:50.log.gz             stats.01:00:00-02:00:00.log.gz
dns.02:15:46-03:00:00.log.gz             stats.02:15:42-03:00:00.log.gz
dns.03:00:00-03:53:19.log.gz             stats.03:00:00-03:53:19.log.gz
files.00:00:00-01:00:00.log.gz           stats.03:53:19-03:53:21.log.gz
files.01:00:00-02:00:00.log.gz           stderr.02:15:41-03:53:21.log.gz
files.02:00:00-02:01:50.log.gz           stdout.02:15:41-03:53:21.log.gz
files.02:15:51-03:00:00.log.gz           traffic.7z
files.03:00:00-03:53:19.log.gz           weird.00:00:00-01:00:00.log.gz
http.00:00:00-01:00:00.log.gz            weird.02:16:09-03:00:00.log.gz
http.01:00:00-02:00:00.log.gz            weird.03:00:00-03:53:19.log.gz
http.02:15:51-03:00:00.log.gz            x509.00:00:00-01:00:00.log.gz
http.03:00:00-03:53:19.log.gz            x509.01:00:00-02:00:00.log.gz
known_hosts.02:15:46-03:00:00.log.gz     x509.02:15:48-03:00:00.log.gz
loaded_scripts.02:15:42-03:00:00.log.gz  x509.03:00:00-03:53:19.log.gz
```
then I used gzip to decompress all gz files
```console
gzip -d *.gz
```
I used grep to find the sketchy site
```console
cat *.log | grep sketchy
1631060682.734045       CV4RZs2lVS3K3dKGQj      10.24.0.2       61108   1.1.1.1 53      udp   9027     0.043605        sketchysite.github.io   1       C_INTERNET      1       A       0     N
```
![Image Alt Text](sketchy.png)
**Flag:** flag{8626fe7dcd8d412a80d0b3f0e36afd4a}
