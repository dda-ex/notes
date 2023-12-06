# NFS

## Identify NFS
```bash
nmap -sV -p 111 --script=rpcinfo [ip]
nmap -p 111 --script=nfs* [ip]
```

## Mount NTFS
```bash
sudo mount -o nolock [ip]:/[share] [mount point]
sudo mount -t nfs -o vers=3 [ip]:/[share] [mount point]
```

remember use vers=3 because it doesn't try to set de permission folders
		
### Change user id
```bash
sudo sed -i -e 's/1001/1014/g' /etc/passwd
```

### Windows
```bash
mount -o anon "\\[ip]\[path]" Z:
			tree /f /a
```

## Chow mounts
```bash
showmount -e [ip]
```

# CIFS
## Identify cifs
Check smb enumeration [[smb enumeration]]

### Mount CIFS - SMB
Linux - bash
```bash
sudo mount -t cifs //[ip]/[share-name] /mnt -o username=[username],password=[password],domain=[domain]
```

Windows - PowerShell
```powershell
net use * /delete
net use z: \\x.x.x.x\c$ password /user:administrator
net use Z: \\10.0.22.92\C$ smbserver_771 /user:administrator
```
https://learn.microsoft.com/en-us/windows/win32/fileio/microsoft-smb-protocol-and-cifs-protocol-overview

```bash
smbclient //[ip]/[share] -I [ip] -N
```

```bash
smbclient -N //10.10.10.3/tmp --option='client min protocol=NT1'
```