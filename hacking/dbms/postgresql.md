# POSTGRESQL

## Lista databases and tables
- `\list` to list the databases
- `\c [DATABASE]` to select the database `[DATABASE]`
-  `\d` to list the tables

### Read files of the system
```pgsql
CREATE TABLE demo(t text);
COPY demo from '[FILENAME]';
SELECT * FROM demo; 
```

