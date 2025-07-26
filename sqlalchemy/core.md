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

