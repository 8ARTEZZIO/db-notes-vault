# SQL Joins

# 🔗 SQL JOINs Explained

In SQL, `JOIN`s are used to combine rows from two or more tables based on a related column between them.

---

## 🧩 Types of JOINs

### 1. **INNER JOIN**
Returns only the rows that have matching values in both tables.

```sql
SELECT a.name, b.salary
FROM employees a
INNER JOIN salaries b ON a.id = b.employee_id;
```

✅ Use when: You only want records with matches in both tables.
### 2. **LEFT JOIN (or LEFT OUTER JOIN)**
Returns all rows from the left table, and the matched rows from the right table. If there's no match, NULL is returned.

```sql
SELECT a.name, b.salary
FROM employees a
LEFT JOIN salaries b ON a.id = b.employee_id;
```

✅ Use when: You want all records from the left table, even if there's no match in the right table.
### 3. **RIGHT JOIN (or RIGHT OUTER JOIN)**
Returns all rows from the right table, and the matched rows from the left table.

```sql
SELECT a.name, b.salary
FROM employees a
RIGHT JOIN salaries b ON a.id = b.employee_id;
```

✅ Use when: You want all records from the right table, even if there are no matches in the left.
### 4. **FULL JOIN (or FULL OUTER JOIN)**
Returns all records when there is a match in either left or right table. Non-matching rows will contain NULLs.

```sql
SELECT a.name, b.salary
FROM employees a
FULL JOIN salaries b ON a.id = b.employee_id;
```

✅ Use when: You want every row from both tables, matched or not.
### 5. **CROSS JOIN**
Returns the Cartesian product of two tables—every combination of rows.

```sql
SELECT a.name, b.department
FROM employees a
CROSS JOIN departments b;
```

⚠️ Use with caution—can return very large result sets.

🧠 Visual Summary
|JOIN Type	|Left Table	|Right Table	|Matches Only?  |
|-----------|-----------|-------------|---------------|
|INNER JOIN	|✅	|✅	|Yes
|LEFT JOIN	|✅	|✅ / NULL	|No
|RIGHT JOIN	|✅ / NULL	|✅	|No
|FULL JOIN	|✅ / NULL	|✅ / NULL	|No
|CROSS JOIN	|✅ x ✅	|	|N/A

🛠 Best Practices

    Always define your ON condition clearly.

    Use JOIN instead of subqueries when possible for better performance and readability.

    Start with INNER JOIN—only expand to others when your logic requires it.

🔍 Next Steps

    Practice with real-world schemas

    Explore SELF JOIN and joining multiple tables

    Learn about performance tuning using indexes

Happy joining! 🔄
