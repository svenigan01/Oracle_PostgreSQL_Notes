# PostgreSQL / psql Display Tips (Readable pg_stat_activity Output)

## 1. Turn OFF pager (`--More--` issue)

```sql
\pset pager off
```

Re-enable:
```sql
\pset pager on
```

---

## 2. Use Expanded Mode (Best for wide tables)

```sql
\x
SELECT * FROM pg_stat_activity;
```

Turn off:
```sql
\x off
```

---

## 3. Auto Expanded Mode (Recommended)

```sql
\x auto
```

---

## 4. Improve Table Formatting

```sql
\pset format aligned
\pset border 2
```

Alternative formats:

- Wrapped format:
```sql
\pset format wrapped
```

- CSV format:
```sql
\pset format csv
```

---

## 5. Increase Column Width

```sql
\pset columns 200
```

(or higher if needed)

---

## 6. Recommended DBA Setup

```sql
\pset pager off
\x auto
\pset columns 200
```

---

## 7. Better Query for pg_stat_activity

Use a cleaner view:

```sql
SELECT pid, usename, state, wait_event_type, wait_event, query_start, query
FROM pg_stat_activity;
```

---

## Summary

- Disable pager → avoids `--More--`
- Use `\x auto` → best readability for wide tables
- Limit columns → reduces clutter
- Select only needed columns → improves clarity
