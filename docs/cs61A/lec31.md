# Declaring Programming

## Database Management Systems

A table is a collection of records, which are rows that have a value for each column.

The Structured Query Language(SQL) is really popular.

SQL is a <u>declarative language</u>

> declarative language

![image-20250323200058821](../assets/cs61a/image-20250323200058821.png)

In declarative language, it's up to the interpreter to choose how to get the desired result, so an import thing for the interpreter is how to do the work the most efficiently.

```sql
create table cities as
	select 38 as latitude, 122 as longtitude, "Berkeley" as name;
```

![image-20250323200600378](../assets/cs61a/image-20250323200600378.png)

when you union a table, the order is not guaranteed.

## SQL

![image-20250323201133398](../assets/cs61a/image-20250323201133398.png)

![image-20250323202113511](../assets/cs61a/image-20250323202113511.png)

*Note: to use union, u do need tables that have the same number of columns and same type of data in each column, but don't need to have the same name of the column, for ONLY the first selected table's name will be used.*

![image-20250323202511692](../assets/cs61a/image-20250323202511692.png)

![image-20250323203758697](../assets/cs61a/image-20250323203758697.png)

![image-20250323205748875](../assets/cs61a/image-20250323205748875.png)