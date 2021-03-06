# BASIC MYSQL

## Add user with password --
` GRANT USAGE ON db_name.table_name TO 'user'@'host' IDENTIFIED BY 'password goes here'; `

## Show user perms/grants --
` SHOW GRANTS FOR 'user'@'host'; `

## Show users --
` SELECT User,Host,Password FROM mysql.user; `

## Show Users per database --
` SELECT user,host from mysql.db where db="<Database Name>"; `

## List databases --
` SHOW DATABASES; `

## Select Database --
` USE db_name; `

## List tables in a db --
` SHOW TABLES; `

## Table Information + format --
` DESCRIBE table_name; `

## Create database --
` CREATE DATABASE db_name; `

## Select specific columns from table --
` SELECT col_name FROM table_name; `
	
## Total database size for a specific database --
` SELECT table_schema "Database Name", data_length, index_length, (data_length + index_length)/(1024*1024) "Total size in MB"from information_schema.TABLES WHERE table_schema LIKE 'db_name' GROUP BY table_schema\G `

## Show all MyISAM Tables and their size in Bytes --
` SELECT TABLE_SCHEMA,TABLE_NAME,ENGINE,DATA_LENGTH from INFORMATION_SCHEMA.TABLES where engine = 'MyISAM' and TABLE_SCHEMA not IN('mysql','information_schema','performance_schema'); `

## Select all tables where the storage engine is MyISAM, and the tables aren't system tables --
` SELECT TABLE_SCHEMA,TABLE_NAME,ENGINE from INFORMATION_SCHEMA.TABLES where engine = 'MyISAM' and TABLE_SCHEMA not IN('mysql','information_schema','performance_schema'); `

## Replication status --
` SHOW slave STATUS; `

## Master status --
` SHOW master STATUS; `
