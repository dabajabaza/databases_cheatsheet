# databases_cheatsheet

### PostgreSQL

* show tables
  * SELECT * FROM pg_catalog.pg_tables
* show tables without system tables
  * SELECT * FROM pg_catalog.pg_tables WHERE schemaname != 'pg_catalog' AND schemaname != 'information_schema'
* all databases
  * \l
* use database
  * \c dbname
* show tables\tables and sequences\ tables and views
  * \dt \d \dS
* backup database
  * pg_dump -U username -f /path/mydb.sql dbname
  * pg_dump -U username -s -f /path/mydb.sql dbname --schema only
  * pg_dump -U username -d dbname -t tbname > filename --single table
  * pg_dump -U username --data-only --table=tablename sourcedb > onetable.pg --single table
  * psql db < onetable.pg --restore single table to database
  * pg_restore --data-only --table=tablename fulldump.pg > onetable.pg --extracting single table out of the large dump
* backup database with password prompt
  * pg_dump -U username -W -f /path/mydb.sql dbname
* restore database
  * \i /path/mydb.sql --slashes is important
  * dbname < /path/mydb.sql
* show pg_config file location
  * SHOW config_file
* alter column type
  * alter table table_name alter column column_name type varchar(2048) using column_name::varchar;
* drop all active sessions
  * ALTER DATABASE db CONNECTION LIMIT 1;
  * SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname = 'db';
* connect as admin
  * psql -h localhost postgres postgres
* export query to csv
  * COPY (SELECT * FROM ...) TO '/tmp/filename.csv' (format CSV);

### MySQL

* import table from one database to another with the same name
  * CREATE TABLE db1.table1 SELECT * FROM db2.table1;
