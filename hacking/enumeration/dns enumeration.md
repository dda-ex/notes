# DNS enumeration

##  whois
```bash
whois [IP]
```

## host
#### Basic searchs
```bash
host [IP]
host [domain]
host -a [domain.com]
```

#### Consulting
```bash
host -t [ns | mx | a | pr | txt | cname] [domain]
```

#### Transfer zone
```bash
host -l [domain] [ns-server]
```

## DNSRecon
#### Transfer zone
```bash
dnsrecon -d [domain] -t axfr
```

#### Enum hostnames
```bash
dnsrecon -d [domain] -D <list> -t brt
```

## Script dns utils
```bash
#!/bin/bash
# Simple Zone Transfer Bash Script
# $1 is the first argument given after the bash script
# Check if argument was given, if not, print usage
if [ -z "$1" ]; then
 echo "[*] Simple Zone transfer script"
 echo "[*] Usage : $0 <domain name> "
 exit 0
fi
# if argument was given, identify the DNS servers for the domain
for server in $(host -t ns $1 | cut -d " " -f4); do
 # For each of these servers, attempt a zone transfer
 host -l $1 $server | grep "has address"
done
```

## NSLOOKUP
#### Basic searchs
```bat
nslookup -type=[TYPE] [domain name]
```
- A deafult from hostname to ip
- PTR from ip to hostname
- MX mailserver
- ANY all information

### Finding LDAP
```bash
nslookup -type=all _ldap._tcp.dc.[domain name]
nslookup -type=srv _ldap._tcp.[domain name]
```

### Test dns
```bash
nslookup [domain] [ns1.dns.com]
```

### Test dns
```bash
nslookup [domain] [ns1.dns.com]
```

## dig
### Basic searchs
```bash
dig [domain]
dig -x [ip]
```

### Transferzone
External domains
```bash
dig AXFR [domain] @[domain]
```

### Internal domains
```bash
dig AXFR int @[domain]
```

### Bind
```bash
dig chaos txt version.bind @[domain]
```

### Force use DNS
```bash
dig @[dns-name] [domain]
```

## wfuzz
To search hidden domains
```bash
wfuzz -c -w /usr/share/wordlists/wfuzz/general/common.txt -u https://domain.com/ -H "Host: FUZZ.domain.com"

```

## dnscan
```bash
./dnscan.py -d [domain] -w subdomains-100.txt
```
Download from git dnscan



