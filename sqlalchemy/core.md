# SQLAlchemy Core – Database Notes

---

## 1. What is SQLAlchemy Core?

- **SQLAlchemy Core** provides a **lower-level SQL abstraction layer** compared to the ORM.  
- You work with **tables**, **columns**, and **SQL expressions** directly, rather than Python classes.  
- Think of it as writing **"Pythonic SQL"**.

---

## 2. Install SQLAlchemy

```bash
pip install sqlalchemy
```

---

## 3. Connect to a Datbase (Engine)

The engine is the starting point to talk to your database.

```python
from sqlalchemy import create_engine

# SQLite example
engine = create_engine('sqlite:///example.db', echo=True)  # echo=True logs SQL statements
```

---

## 4. Create Tables with Metadata

```python
from sqlalchemy import MetaData, Table, Column, Integer, String

metadata = MetaData()

users = Table(
    'users',
    metadata,
    Column('id', Integer, primary_key=True),
    Column('username', String, nullable=False),
    Column('email', String, unique=True)
)

# Create the table in DB
metadata.create_all(engine)
```

---

## 5. Insert Data

```python
from sqlalchemy import insert

stmt = insert(users).values(username="bart", email="bart@example.com")
with engine.connect() as conn:
    conn.execute(stmt)
    conn.commit()
```

Insert multiple rows:

```python
stmt = insert(users)
with engine.connect() as conn:
    conn.execute(stmt, [
        {"username": "alice", "email": "alice@example.com"},
        {"username": "john", "email": "john@example.com"}
    ])
    conn.commit()
```

---

## 6. Query Data

```python
from sqlalchemy import select

stmt = select(users)
with engine.connect() as conn:
    result = conn.execute(stmt)
    for row in result:
        print(row.username, row.email)
```

With filters:

```python
stmt = select(users).where(users.c.username == "bart")
```

---

## 7. Update Data

```python
from sqlalchemy import update

stmt = update(users).where(users.c.username == "bart").values(email="bart_new@example.com")
with engine.connect() as conn:
    conn.execute(stmt)
    conn.commit()
```

---

## 8. Delete Data

```python
from sqlalchemy import delete

stmt = delete(users).where(users.c.username == "john")
with engine.connect() as conn:
    conn.execute(stmt)
    conn.commit()
```

---

## 9. Transactions

```python
with engine.begin() as conn:
    conn.execute(insert(users).values(username="sam", email="sam@example.com"))
    conn.execute(insert(users).values(username="max", email="max@example.com"))
    # auto-committed on exit
```

---

## 10. Raw SQL Execution

```python
with engine.connect() as conn:
    result = conn.execute("SELECT * FROM users;")
    for row in result:
        print(row)
```

---

## 11. SQLAlchemy Core vs ORM

|Feature | Core | ORM|
|-----|-------|---------|
|Abstraction | SQL-focused | Python object-focused|
|Use Case | Data pipelines, scripts | Web apps, complex relations|
|Speed | Slightly faster (less overhead) | More convenient, but slower|

---

## 12. Best Practices

<ul>
    <li>Use metadata.create_all() once per app to ensure tables exist.</li>
    <li>Use context managers (with engine.connect()) to avoid connection leaks. </li>
    <li>Use transactions when modifying data.</li>
    <li>Keep SQLAlchemy Core for performance-heavy or SQL-centric apps.</li>
</ul>

---

## 13. Next Steps

<ul>
    <li>Explore <code>and_</code> / <code>or_</code> for complex <code>WHERE</code> clauses.</li>
    <li>Learn <code>join()</code> for multi-table queries.</li>
    <li>Practice creating <strong>indexes and constraints.</strong></li>
</ul>
