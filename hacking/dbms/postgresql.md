# POSTGRESQL

HeidiSQL is a good alternative to connect.

## Connection
```bash
psql -U <myuser> # Open psql console with user
psql -h <host> -U <username> -d <database> # Remote connection
psql -h <host> -p <port> -U <username> -W <password> <database> # Remote connection
```

## Basic commands databases and tables
- `\list` to list the databases
- `\c [DATABASE]` to select the database `[DATABASE]`
-  `\d` to list the tables
- `\du+` get users roles

## Read users passwd
```sql
SELECT usename, passwd from pg_shadow;
```

### Read files of the system
```sql
CREATE TABLE demo(t text);
COPY demo from '[FILENAME]';
SELECT * FROM demo; 
```

