+++
title= "Databases"
date= 2018-08-08T19:59:38+05:30
tags = [
    "Databases",
    "SQL"
   ]
+++

- Relational databases like MySQL, PostgreSQL and SQLite3 represent and store data in tables and rows. 

- They're based on a branch of algebraic set theory known as relational algebra.

- Mongo query targets of data are technically represented as BSON (binary JASON).

- Relational databases use Structured Querying Language (SQL), making them a good choice for applications that involve the management of several 
transactions. 

- ACID -  Atomicity (each transaction be "all or nothing"), Consistency (any transaction will bring the database from one valid state to another), Isoloation (concurrent execution of transactions results in a system state that would be obtained if transactions were executed sequentially), Durability (once a transaction has been committed, it will remain so)

- Object-Relational Mapping (ORM) is a technique that lets you query and manipulate data from a database using an object-oriented paradigm



-DECODE is a function in Oracle and is used to provide if-then-else type of logic to SQL.


##### To fetch ALTERNATE records from a table. (EVEN NUMBERED)

```select * from emp where rowid in (select decode(mod(rownum,2),0,rowid, null) from emp);```

##### To select ALTERNATE records from a table. (ODD NUMBERED)
``` select * from emp where rowid in (select decode(mod(rownum,2),0,null ,rowid) from emp);```

##### Find the 3rd MAX salary in the emp table.
``` select distinct sal from emp e1 where 3 = (select count(distinct sal) from emp e2 where e1.sal <= e2.sal);```

``` Alter table table_name add(columnname1 datatype(size), columname2 datatype(size),....);```

```Alter table table_name modify(columnname1 datatype(size), columnname2 datatype(size),....);```

- Truncate table command it is used to delete all rows permanently from the table.


- DDL – Data Definition Language
DML – Data Manipulation Language


- Normalization is the process of efficiently organizing data in a database. There are two goals of the normalization process: eliminating redundant data (for example, storing the same data in more than one table) and ensuring data dependencies make sense (only storing related data in a table)

###Benefits :

-  Eliminate data redundancy
- Improve performance
- Query optimization
- Faster update due to less number of columns in one table
- Index improvement


---
- Row-level locks are placed on single records (rows) that the statements in a transaction define. The locks are placed as soon as any piece of the row is accessed.Row-level locks are always implicit, solidDB sets the locks when necessary. You cannot lock or unlock row-level locks manually.



- Table-level locks can be thought of as metadata locks; they prevent concurrent users from making schema changes (DDL operations) simultaneously or while records within the table are being changed.
-----

The binary log contains a record of all changes to the databases, both data and structure, as well as how long each statement took to execute. It consists of a set of binary log files and an index

----
Replication works like this.

The master writes all transactions into its binary log.
The slave reads the transactions from masters binary log and writes them to its relay log.
Only after that the slave executes the statements from its relay log.
binlog-do-db makes the master write only statements for the specified DB into its binary log.

replicate-do-db makes the slave just read statements from the relay log, that are for the specified DB.

replicate-do-db has no effect on the master,since there is no relay log to read from.

The LOCK TABLES part is there, so that the data is consistent. It prevents that the data on the master is modified while backing up the data is still in process.

---blem

## N+1 pro
Let's say you have a collection of Car objects (database rows), and each Car has a collection of Wheel objects (also rows). In other words,` Car -> Wheel` is a 1-to-many relationship.

Now, let's say you need to iterate through all the cars, and for each one, print out a list of the wheels. 

`SELECT * FROM Cars;
`And then for each Car:

`SELECT * FROM Wheel WHERE CarId = ?`


Alternatively, one could get all wheels and perform the lookups in memory:

`SELECT * FROM Wheel` 
This reduces the number of round-trips to the database from N+1 to 2. 