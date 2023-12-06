Simple Backdoor in C

This is my first Windows Backdoor

Alternative with bash
```bash
ncat -knvlp 50005 | tee test.txt
```

Compilation of the client
```bash
i686-w64-mingw32-gcc -o back.exe backdoor_mod.c -lwsock32 -lwininet
```