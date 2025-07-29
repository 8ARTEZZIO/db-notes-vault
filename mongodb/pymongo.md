# 🐍 PyMongo – Direct MongoDB Access (No ODM)

---

## 📦 What is PyMongo?

PyMongo is the **official low-level MongoDB driver for Python**.  
It allows you to directly connect to MongoDB and work with databases, collections, and documents.

---

## ⚙️ 1. Installation

```bash
pip install pymongo
```

## 🌐 2. Connect to MongoDB

```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["ecommerce_db"]
```

## 📁 3. Create / Access a Collection

```python
products = db["products"]
users = db["users"]
```

## 📝 4. Insert Documents

```python
# Single document
products.insert_one({
    "name": "Headphones",
    "price": 49.99,
    "stock": 20
})

# Multiple documents
products.insert_many([
    {"name": "Mouse", "price": 19.99, "stock": 50},
    {"name": "Keyboard", "price": 29.99, "stock": 30}
])
```

## 🔍 5. Query Documents

```python
# All documents
for product in products.find():
    print(product)

# Find one
product = products.find_one({"name": "Mouse"})

# Filter with comparison
cheap = products.find({"price": {"$lt": 30}})
```

## ✏️ 6. Update Documents

```python
# Update one
products.update_one(
    {"name": "Mouse"},
    {"$set": {"stock": 100}}
)

# Update many
products.update_many(
    {"price": {"$lt": 30}},
    {"$inc": {"stock": 10}}
)
```

## ❌ 7. Delete Documents

```python
# Delete one
products.delete_one({"name": "Keyboard"})

# Delete many
products.delete_many({"stock": 0})
```

## 🔎 8. Useful Operators

|**Operator**|**Use**|
|-|-|
|
