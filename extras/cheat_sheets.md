# 📦 Database Cheat Sheet – db-notes-vault

Quick reference for SQL, MongoDB (PyMongo), SQLAlchemy ORM, and MongoEngine ODM.

---

## 🧠 SQL vs MongoDB (PyMongo)

| **SQL Concept** | **MongoDB (PyMongo)**           |
|-----------------|---------------------------------|
| Table           | Collection                      |
| Row             | Document                        |
| Column          | Field                           |
| Primary Key     | `_id`                           |
| Query           | `find()`, `find_one()`          |
| Insert          | `insert_one()`, `insert_many()` |
| Update          | `update_one()`, `update_many()` |
| Delete          | `delete_one()`, `delete_many()` |

---

## 🔍 MongoDB Query Operators

| **Operator** | **Use**                  |
|--------------|--------------------------|
| `$gt`        | Greater than             |
| `$lt`        | Less than                |
| `$in`        | In list                  |
| `$exists`    | Field exists             |
| `$regex`     | Pattern matching         |
| `$inc`       | Increment value          |
| `$set`       | Set or overwrite a value |
| `$push`      | Append to array field    |

---

## 🧱 SQLAlchemy ORM vs MongoEngine ODM

| **SQLAlchemy (Relational)** | **MongoEngine (Document)**    |
|-----------------------------|-------------------------------|
| `Table`                     | `Document`                    |
| `Column`                    | `Field`                       |
| `ForeignKey`                | `ReferenceField`              |
| `relationship()`            | `ReferenceField`, `ListField` |
| `session.add()`             | `doc.save()`                  |
| `session.query(Model)`      | `Model.objects()`             |
| `filter_by()` / `filter()`  | `.filter(field=value)`        |
| `session.commit()`          | Auto-commit on `.save()`      |
| SQLAlchemy Migrations       | Manual / third-party tools    |

---

## 🗃 MongoEngine – Quick Snippets

```python
from mongoengine import Document, StringField, FloatField, IntField

class Product(Document):
    name = StringField(required=True)
    price = FloatField(required=True)
    stock = IntField(default=0)

# Insert
Product(name="Mouse", price=19.99, stock=20).save()

# Query
Product.objects(name="Mouse").first()

# Update
Product.objects(name="Mouse").update_one(set__stock=25)

# Delete
Product.objects(name="Mouse").delete()
```

---

## 🗄 PyMongo – Quick Snippets

```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["shop"]
products = db["products"]

# Insert
products.insert_one({"name": "Mouse", "price": 19.99, "stock": 20})

# Query
products.find_one({"name": "Mouse"})

# Update
products.update_one({"name": "Mouse"}, {"$set": {"stock": 25}})

# Delete
products.delete_one({"name": "Mouse"})
```

---

## 🧰 SQLAlchemy ORM – Quick Snippets

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

Base = declarative_base()
engine = create_engine('sqlite:///shop.db')
Session = sessionmaker(bind=engine)
session = Session()

class Product(Base):
    __tablename__ = 'products'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    price = Column(Integer)

# Insert
p = Product(name="Mouse", price=1999)
session.add(p)
session.commit()

# Query
session.query(Product).filter_by(name="Mouse").first()

# Update
p.price = 2499
session.commit()

# Delete
session.delete(p)
session.commit()
```

---

## Tips

- MongoDB collections are auto-created on insert.
