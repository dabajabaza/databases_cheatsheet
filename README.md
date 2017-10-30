# Databases Cheatsheet

## PostgreSQL

### useful queries

- _**show db tables**_
```sql
   SELECT * FROM pg_catalog.pg_tables;
```
- _**show tables without system tables**_
```sql
   SELECT * FROM pg_catalog.pg_tables WHERE schemaname != 'pg_catalog' AND schemaname != 'information_schema';
```
- _**list all databases**_
-  `\l`
- _**show tables \tables and sequences \tables and views**_
-  `\dt \d \dS`
- _**use database**_
-  `\c dbname`
- _**alter column type e.g. boolean to integer**_
```sql
   ALTER TABLE tbname ALTER colname SET DEFAULT null;

   ALTER TABLE tbname ALTER colname TYPE INTEGER USING CASE WHEN colname = false THEN 0 ELSE 1 END;

   ALTER TABLE tbname ALTER colname SET DEFAULT 0;
   COMMIT;
```
  
### backup, export database

- _**whole**_
-  `pg_dump -U username -f /path/dump.sql dbname`
- _**schema only**_
-  `pg_dump -U username -s -f /path/dump.sql dbname`
- _**single table**_
-  `pg_dump -U username -d dbname -t tbname > dump.sql`
- _**single table data only**_
-  `pg_dump -U username --data-only --table=tablename sourcedb > dump.sql`
- _**export data to csv**_
```sql
   COPY (SELECT * FROM table1) TO '/path/to/csv/data.txt' (format CSV);
```

### restore, import database

- _**restore database**_
-  `\i /path/dump.sql`
- _**single table to database**_
-  `psql dbname < dump.sql`
- _**extracting single table out of the large dump**_
-  `pg_restore --data-only --table=tablename fulldump.pg > dump.pg`
- _**import data from csv**_
```sql
   COPY table1(col1, col2, col3) FROM '/path/to/csv/data.txt' WITH (FORMAT csv);
```
- _**import data from csv - include the header row**_
```sql
   COPY table1 FROM '/path/to/csv/data.txt' DELIMITER ',' CSV HEADER;
```

### useful system commands

- _**show pg_config file location**_
```sql
  SHOW config_file
```
- _**connect as admin**_
- `psql -h localhost postgres postgres`
- _**drop all active sessions**_
```sql
  ALTER DATABASE db CONNECTION LIMIT 1;
  SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'db';
```

## MySQL

### restore, import database

- _**import table with the same name from one database to another**_
```sql
   CREATE TABLE db1.table1 SELECT * FROM db2.table1;
```
- _**import data from csv file. Basename of a file mult be equal to tablename**_
- `mysqlimport -u user -p -c column1,column2 --fields-terminated-by=; database_name table_name.txt`
