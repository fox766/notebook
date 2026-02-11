# Database

## Create Table and Drop Table

![image-20250325081346039](../assets/cs61a/image-20250325081346039.png)

![image-20250325081438211](../assets/cs61a/image-20250325081438211.png)

## Modifying the table

**Insert**

![image-20250325081751406](../assets/cs61a/image-20250325081751406.png)

**Update**

![image-20250325082433705](../assets/cs61a/image-20250325082433705.png)

![image-20250325082638671](../assets/cs61a/image-20250325082638671.png)

Note: not equivalent to drop a table; if you delete all rows in a table, the table still exists.

## Python and SQL

```python
import sqlite3

db = sqlite3.connection("n.db")
db.execute("CREATE TABLE nums AS SELECT 2 UNION SELECT 3;")
db.execute("INSERT INTO nums VALUE (?), (?), (?);", range(4, 7))
print(db.execute("SELECT * FROM nums;").fetchall())
# db.execute("SELECT * FROM nums;") returns a cursor object
db.commit()
```

## SQL Injection Attack

![image-20250325090455400](../assets/cs61a/image-20250325090455400.png)

![image-20250325090926767](../assets/cs61a/image-20250325090926767.png)

## Database Connections