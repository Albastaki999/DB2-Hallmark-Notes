# DB2 Important commands

Get DB2 Instance

```
db2 get instance
```

Start/Run DB2 instance

```
db2start
```

Create Database

```
db2 create database TESTDB
```

Drop Database

```
db2 drop database <dbname>
```

Activate Database

```
db2 activate database <dbname>
```

Deactivate Database

```
db2 deactivate database <dbname>
```

Connect with the Database

```
db2 connect to TESTDB
```

Check your connection state

```
db2 get connection state
```

Check database servers

```
select current server from sysibm.sysdummy1
```

Create table

```
db2 "
CREATE TABLE EMPLOYEE VARCHAR(100),
(
    EMP_ID INT NOT NULL,
    NAME VARCHAR(100),
    SALARY DECIMAL(10,2),
    PRIMARY KEY (EMP_ID)
)
"
```

Insert into table

```
db2 "insert into EMPLOYEE VALUES (1, 'Rashid', 25000)"
```

List all tables

```
db2 "LIST TABLES"
```

Database directory

```
db2 list db directory
```

Check Active Databases

```
db2 list active databases
```

Describe Table

```
db2 describe table EMPLOYEE
```

Get Database Manager configuration

```
db2 get dbm cfg
```

Get Database configuration for a database

```
db2 get db cfg for TESTDB
```

Update an instance parameter

```
db2 update dbm cfg using <parameter> <value>
```

Update a database parameter

```
db2 update db cfg for TESTDB using <parameter> <value>
```

Location of `db2diag.log` file

```
cd /home/rashid/sqllib/db2dump
```

Steps to follow when production error occurs:

1. Check whether the instance itself is running:

   ```
   ps -ef | grep db2sysc
   ```

2. If instance is up, then check which databases are active:
   ```
   db2 list active databases
   ```
3. Check which users or applications are connected:
   ```
   db2 list applications
   ```

Force all applications to disconnect

```
db2 force applications all
```

Get all instances

```
db2ilist
```

Create an instance

```
sudo /opt/ibm/db2/V12.1/instance/db2icrt <instance_name>
```

Switch instance

```
db2set DB2INSTANCE=<instance_name>
```

Select indexes for a table

```
db2 "SELECT INDNAME, UNIQUERULE, COLNAMES
FROM SYSCAT.INDEXES
WHERE TABNAME='<Table_Name>'"
```

Find the create script for EXPLAIN PLANS

```
find ~/sqllib -name EXPLAIN.DDL
```

Execute the script inside EXPLAIN.DDL

```
db2 -tvf ~/sqllib/misc/EXPLAIN.DDL
```

- `-t` &rarr; Treat `;` as the SQL statement terminator.
- `-v` &rarr; Verbose mode (prints each SQL statement as it executes).
- `-f` &rarr; Read SQL from a file.
