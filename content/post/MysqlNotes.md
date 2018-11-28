---
title: "MysqlNotes"
date: 2018-11-28T21:42:31+05:30
draft: false,
tags : [
    "Mysql",
    "Interview",
    "Sql"
]
---

`CREATE DATABASE mydb;`

`use mydb`

```
CREATE TABLE mytable
(
id
int unsigned NOT NULL auto_increment,
username
varchar(100) NOT NULL,
email
varchar(100) NOT NULL,
PRIMARY KEY
(id)
);
CREATE T  
```

`SHOW databases;`

`SHOW tables;`

`DESCRIBE databaseName.tableName;` - Show all the fields of a table

----
## Users and Roles

`CREATE USER 'user'@'localhost' IDENTIFIED BY 'password'` -  Localhost for where the user can connect from and  can only connect on the local machine where the database is hosted.


`CREATE USER 'user'@'%' IDENTIFIED BY 'some_password';` - From anywhere 


`GRANT SELECT, INSERT, UPDATE ON databaseName.* TO 'userName'@'localhost';` - Grant common, basic privileges to the user for all tables of the specified database:

`GRANT ALL ON *.* TO 'userName'@'localhost' WITH GRANT OPTION; ` - Grant all privileges to the user for all tables on all databases.(*.*)
