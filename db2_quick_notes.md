## DB2 Quick Commands

Load profile

```
. ~/sqllib/db2profile
```

List Databases

```
db2 list db directory
```

Connect to a DB

```
db2 connect to <database_name>
```

List Schemas

```
db2 "select schemaname from syscat.schemata"
```

List Application Tables

```
db2 "select tabschema, tabname
from syscat.tables
where type='T'
order by tabschema, tabname"
```

Describe Table

```
db2 describe table <schema>.<table>
```

