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

----


## Varchar(255)
Why should avoid using 255

- When a complex SELECT needs to create temporary table (for a subquery, UNION , GROUP BY , etc), the
preferred choice is to use the MEMORY engine, which puts the data in RAM. But VARCHARs are turned into CHAR
in the process. This makes VARCHAR(255) CHARACTER SET utf8mb4 take 1020 bytes. That can lead to needing
to spill to disk, which is slower.
- In certain situations, InnoDB will look at the potential size of the columns in a table and decide that it will be
too big, aborting a CREATE TABLE
---

`SELECT stack.* FROM stack JOIN Overflow ON stack.id = Overflow.id;` - To select all columns in one table on joins

```
//  TO select using IF Else
SELECT st.name,
st.percentage,
CASE WHEN st.percentage >= 35 THEN 'Pass' ELSE 'Fail' END AS `Remark`
FROM student AS st ;
```


or
```
SELECT st.name,
st.percentage,
IF(st.percentage >= 35, 'Pass', 'Fail') AS `Remark`
FROM student AS st ;
```

```
SELECT * FROM stack WHERE id BETWEEN 2 and 5;
```

```
SELECT * FROM stack WHERE id NOT BETWEEN 2 and 5;
```

`SELECT username FROM users WHERE users LIKE 'admin_';` -> admin1 - matches a single character

`SELECT * FROM users ORDER BY id ASC LIMIT 2, 3` - > From 2nd row and 3 columns

---

Backticks are mainly used to prevent an error called "MySQL reserved word"

---

## Variables 

`SET @var_string = 'my_var';`

`Select @var := '123';` - > Setting the result of select query

```
SET @start_date = '2015-07-20';

#this gets the year month value to use as the partition names

SET @start_yearmonth = (SELECT EXTRACT(YEAR_MONTH FROM @start_date));

```

---


# Performance improvement


-  Have the most efficient SQL queries
-   Design a logical schema that support the application's need (e.g. type of the columns, etc.)
-   Design trade-off to support some use case better than other
-   Relational constraints
-   Normalization
-  Checking the connection pool


- Keep statistics up to date
- Re-sequence critical tables periodically
- Disk maintenance
- All the system stuff to have a server that rocks




## Normalisation

>Organizes tables in a manner that reduces redundancy and dependency of data. 

>  A composite key is a primary key composed of `multiple columns` used to identify a record uniquely 

1NF -  Same table
2NF - Different table for relation and so on  .Used Foreign key
3NF -  Decomposing further

## [Partitioning](https://www.sqlshack.com/database-table-partitioning-sql-server/)

> Partitioning is the database process where very large tables are divided into multiple smaller parts.


----


## Stored Procedure

> Batch of SQL statements

`PL/SQL` includes procedural language elements such as conditions and loops. It allows declaration of constants and variables, procedures and functions, types and variables of those types, and triggers. It can handle exceptions (runtime errors)

```
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;


 EXEC SelectAllCustomers City = "London"; 
```

---

## Triggers

- Special type of stored procedure. 
- Not called directly like a stored procedure. 
- Trigger is called `automatically` when a data modification event is made against a table whereas a stored procedure must be called `explicitly`.