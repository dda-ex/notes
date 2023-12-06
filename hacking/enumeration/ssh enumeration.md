# SSH enumeration

## identify cipher algos
```bash
nmap -p22 [IP] --script ssh2-enum-algos
```

## ssh keys
```bash
nmap -p22 [IP] --script ssh-hostkey --script-args ssh_hostkey=full
```
Copy the ssh-rsa

## ssh check logins
```bash
nmap -p22 [IP] --script ssh-auth-methods --script-args="ssh.user=student"
nmap -p22 [IP] --script ssh-auth-methods --script-args="ssh.user=admin"
```