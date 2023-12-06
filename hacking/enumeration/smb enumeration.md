# SMB enumeration

## Configuration
add to /etc/samba/smb.conf
```bash
[global]
client min protocol=NT1
```

```bash
sudo nbtscan -r [ip][/mask]
```

## Enumerate Hostname
```bash
nmblookup -A [ip]
```

## List Shares
```bash
smbmap -H [ip/hostname]
smbmap -H [ip/hostname] -u guest -p "" -d .
smbmap -H [ip/hostname] -u "user" -p "pass" -d "domain"
smbmap -H [ip/hostname] -u "user" -p "pass" -d .
smbmap -H [ip/hostname] -u administrator -p [pass] -d . -L
````

```bash
smbclient -L \\\\[ip] -U "domain\user"%pass
```

```bash
nmap --script smb-enum-shares -p 139,445 [ip]
```

```bash
smbclient -N //10.10.10.3/tmp --option='client min protocol=NT1'
```

## Check Null Sessions
```bash
smbmap -H [ip/hostname]
rpcclient -U "" -N [ip]
smbclient \\\\[ip]\\[share name]
```

```bash
smbclient -N -L \\\\[ip]
```

## Check for Vulnerabilities 
```bash
nmap --script smb-vuln* -p 139,445 [ip]
nmap --script smb-enum* -p 139,445 [ip] --script-args smbusername=[username],smbpassword=[password]
```

## Overall Scan 
```bash
enum4linux -a [ip]
```

## Manual Inspection
```bash
smbver.sh [ip] (port) [Samba]
```

## Execute commands
```bash
smbmap -H [ip/hostname] -u [user] -p [pass] -d . -x 'ipconfig'
```

## Upload / Download files
```bash
smbmap -H [ip/hostname] -u [user] -p [pass] -d . --upload '[path/file]' '[C$\file]'
smbmap -H [ip/hostname] -u [user] -p [pass] -d . --download '[C$\file]'
```
