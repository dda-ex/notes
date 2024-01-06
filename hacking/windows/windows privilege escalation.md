# Windows privilege escalation
```cmd
whoami

net user

systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"

tasklist /SVC

netsh advfirewall show currentprofile

netsh advfirewall firewall show rule name=all

schtasks /query /fo LIST /v

wmic product get name, version, vendor

wmic qfe get Caption, Description, HotFixID, InstalledOn 
```


After execute exploit suggester, it is important check the next link
https://github.com/SecWiki/windows-kernel-exploits

I prefer WES-NG https://github.com/bitsadmin/wesng

