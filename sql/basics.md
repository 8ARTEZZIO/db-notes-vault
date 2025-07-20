# SQL Basics

# 🧠 SQL Basics

This file contains foundational knowledge of SQL—ideal for beginners and as a refresher for more advanced developers.


## 🔹 What is SQL?

**SQL (Structured Query Language)** is a standard language used to manage and manipulate relational databases. It allows you to:

- Query data (`SELECT`)
- Insert data (`INSERT`)
- Update records (`UPDATE`)
- Delete records (`DELETE`)
- Define schemas (`CREATE`, `ALTER`, `DROP`)


## 📌 Basic Query Syntax

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1 ASC|DESC;
```

Example:

```sql
SELECT name, age
FROM users
WHERE age > 21
ORDER BY age DESC;
```


## 📥 INSERT Statement

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```


## ✏️ UPDATE Statement

```sql
UPDATE table_name
SET column1 = value1
WHERE condition;
```

## 🗑 DELETE Statement

```sql
DELETE FROM table_name
WHERE condition;
```

## ⚠️ Important Clauses

    WHERE: Filters records

    ORDER BY: Sorts results

    LIMIT: Restricts number of returned rows

    GROUP BY: Groups records by column(s)

    HAVING: Filters after grouping (unlike WHERE, which filters before)


## 🔗 Common Data Types

| Type         | Description             |
|--------------|-------------------------|
| `INT`        | Integer                 |
| `VARCHAR(n)` | Variable-length string  |
| `TEXT`       | Long-form text          |
| `DATE`       | Date                    |
| `BOOLEAN`    | True or False           |

## ✅ Best Practices

    Always use WHERE with UPDATE and DELETE to avoid unintentional data changes.

    Use LIMIT when testing queries.

    Use meaningful table and column names.

    Normalize your data where appropriate.

## 🔍 Next Steps

    Learn about JOINs for combining tables → joins.md

    Dive into constraints, keys, and indexing

    Practice with real datasets (e.g., Chinook)
