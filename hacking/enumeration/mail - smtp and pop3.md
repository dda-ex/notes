# SMTP and POP3

## Connect to SMTP server
```bash
nc -nv [ip] 25
```

## Connect to POP3 server
```bash
nc -nv [ip] 110
```

```bash
telnet [ip] 110
```

## Basic commands 
### Authentication
```bash
USER [username]
PASS [password]
		
STAT - Show number of messages
LIST - As STAT but by message
RETR - Read message
DELE - Delete message
RSET - Reset session
TOP  - Read by lines 
QUIT - quit
```

## SPOOF MAIL
### spoofcheck
```bash
./spoofcheck.py [domain]
```
SpoofCheck requiere a virtual env in python 2 - venvP2

## MailSniper and Spraying Toolkit
### Load module 
```powershell
Import-module MailSniper.ps1
```

### Enumerate NetBIOS name of the target domain
```powershell
Invoke-DomainHarvestOWA -ExchHostname mail.[domain]
```

### Validate usernames
```powershell
Invoke-UsernameHarverstOWA -ExchHostname mail.[domain] -Domain [domain] -UserList [names] -OutFile [valid_names]
```

### Password spray attack
```powershell
Invoke-PasswordSprayOWA -ExchHostname mail.[domain] -UserList [valid_names] -Password [password]
```

### Get global address list from a user
```powershell
Get-GlobalAddressList -ExchHostname mail.[domain] -Username [domain]\[user] -Password [password] -OutFile [gal.txt]
```

## GC - Zone Identifier
Zone identifier allows to trust and download a file via email-client and not be tainted with the "Mark of the Web" MOTW.
```powershell
gc [file] -Stream Zone.Identifier
```

0 => Local computer
1 => Local intranet
2 => Trusted sites
3 => Internet
4 => Restricted Sites


