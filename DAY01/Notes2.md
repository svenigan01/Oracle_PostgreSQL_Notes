# Fundamentals PostgreSQL (1–5)

## 1. AWS CloudShell / psql prompt
```
postgres=>
```

## 2. Check Current Database
```sql
select current_database();
```

### Output
```
 current_database 
------------------
 postgres
(1 row)
```

---

## 3. Check PostgreSQL Version
```sql
select version();
```

### Output
```
PostgreSQL 17.7 on aarch64-unknown-linux-gnu, compiled by aarch64-unknown-linux-gnu-gcc (GCC) 10.5.0, 64-bit
(1 row)
```

---

## 4. Check Current User
```sql
select current_user;
```

### Output
```
 current_user 
--------------
 postgres
(1 row)
```

---

## 5. Create Database
```sql
create database salesdb;
```

### Output
```
CREATE DATABASE
```

---

## 6. List Databases
```sql
select datname from pg_database;
```

### Output
```
  datname  
-----------
 template0
 rdsadmin
 template1
 postgres
 salesdb
(5 rows)
```

---

## 7. List Schemas
```sql
select schema_name from information_schema.schemata;
```

### Output
```
    schema_name     
--------------------
 public
 finance
 information_schema
 pg_catalog
(4 rows)
```

---

## 8. Create Table
```sql
create table customers(
 id serial primary key,
 name varchar(20),
 email varchar(20)
);
```

### Output
```
CREATE TABLE
```

---

## 9. View Table Data
```sql
select * from customers;
```

### Output
```
 id | name | email 
----+------+-------
(0 rows)
```

---

# End of Fundamentals (1–5)
