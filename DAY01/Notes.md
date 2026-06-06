# Oracle & PostgreSQL Notes

## SQL, Procedures, and Functions

### Check Data Files

```sql
SELECT file_name,
       tablespace_name,
       bytes / 1024 / 1024 AS size_mb
FROM dba_data_files;
```

### Describe Data Dictionary View

```sql
DESC dba_data_files;
```

### View All Data Files

```sql
SELECT *
FROM dba_data_files;
```

---

## PL/SQL Examples

### Update a Record

```sql
DECLARE
    s_orderid SALES.ORDER_ID%TYPE := 129512;
BEGIN
    UPDATE SALES
    SET SALES_AMOUNT = 100
    WHERE ORDER_ID = s_orderid;

    COMMIT;
END;
/
```

### Delete a Record

```sql
DECLARE
    s_orderid SALES.ORDER_ID%TYPE := 129512;
BEGIN
    DELETE FROM SALES
    WHERE ORDER_ID = s_orderid;

    COMMIT;
END;
/
```

---

## Tablespace Management

### Check Data File Sizes

```sql
SELECT file_name,
       tablespace_name,
       bytes / 1024 AS size_kb
FROM dba_data_files;
```

### Resize an Existing Data File

```sql
ALTER DATABASE DATAFILE
'C:\APP\SRIOR\PRODUCT\26AI\ORADATA\FREE\USERS01.DBF'
RESIZE 20M;
```

### Add a Data File to a Tablespace

```sql
ALTER TABLESPACE users
ADD DATAFILE
'C:\APP\SRIOR\PRODUCT\26AI\ORADATA\FREE\USERS02.DBF'
SIZE 5M;
```

### Check Whether a Tablespace is Bigfile or Smallfile

```sql
SELECT tablespace_name,
       bigfile
FROM dba_tablespaces
WHERE tablespace_name = 'USERS';
```

---

## Create and Drop Tablespaces

### Create a Smallfile Tablespace

```sql
CREATE SMALLFILE TABLESPACE test_ts
DATAFILE 'C:\APP\SRIOR\PRODUCT\26AI\ORADATA\FREE\TEST01.DBF'
SIZE 10M;
```

### Drop a Tablespace

```sql
DROP TABLESPACE test_ts;
```

### Drop a Tablespace Including Contents and Datafiles

```sql
DROP TABLESPACE test_ts
INCLUDING CONTENTS AND DATAFILES;
```

---

## Database Information

### Check Database Name, Open Mode, and Role

```sql
SELECT name,
       open_mode,
       database_role
FROM v$database;
```

---

## Useful DBA Views

| View              | Purpose                      |
| ----------------- | ---------------------------- |
| `DBA_DATA_FILES`  | Information about data files |
| `DBA_TABLESPACES` | Tablespace information       |
| `V$DATABASE`      | Database status and role     |
| `V$INSTANCE`      | Instance information         |
| `DBA_USERS`       | User accounts                |
| `DBA_TABLES`      | Table metadata               |
| `DBA_SEGMENTS`    | Space usage by objects       |

---

## Oracle Architecture Notes

### CDB (Container Database)

A CDB contains:

* Root Container (`CDB$ROOT`)
* Seed Database (`PDB$SEED`)
* One or more Pluggable Databases (PDBs)

### PDB (Pluggable Database)

A PDB is a portable collection of schemas, objects, and data that appears to an application as a separate database.

Useful commands:

```sql
SHOW PDBS;
```

```sql
ALTER SESSION SET CONTAINER = FREEPDB1;
```

```sql
SHOW CON_NAME;
```

---

## PostgreSQL Equivalent Concepts

| Oracle            | PostgreSQL         |
| ----------------- | ------------------ |
| Database Instance | PostgreSQL Cluster |
| CDB               | Cluster            |
| PDB               | Database           |
| Tablespace        | Tablespace         |
| Datafile          | Managed Internally |
| Schema            | Schema             |
| PL/SQL            | PL/pgSQL           |

### PostgreSQL Databases

```sql
SELECT datname
FROM pg_database;
```

### PostgreSQL Tablespaces

```sql
SELECT *
FROM pg_tablespace;
```

### PostgreSQL Database Size

```sql
SELECT pg_size_pretty(pg_database_size(current_database()));
```
