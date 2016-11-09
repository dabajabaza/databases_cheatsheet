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
* backup database with password prompt
 * pg_dump -U username -W -f /path/mydb.sql dbname
* restore database
 * \i /path/mydb.sql --slashes is important
 * dbname < /path/mydb.sql
* show pg_config file location
 * SHOW config_file
* alter column type
 * alter table table_name alter column column_name type varchar(2048) using column_name::varchar;
