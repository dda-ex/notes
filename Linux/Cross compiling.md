# Cross compiling

```bash
sudo dpkg --add-architecture i386
sudo apt-get update
sudo apt-get install libwine:i386
sudo apt-get install wine32
sudo apt-get install mingw-w64

i686-w64-mingw32-gcc 42341.c -o syncbreeze_exploit.exe -lws2_32
```