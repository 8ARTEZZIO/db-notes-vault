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

| **Operator** | **Use**                          |
|--------------|----------------------------------|
| `$gt`        | Greater than                     |
| `$lt`        | Less than                        |
| `$in`        | In list                          |
| `$exists`    | Field exists                     |
| `$regex`     | Pattern matching                 |
| `$inc`       | Increment value                  |
| `$set`       | Set or overwrite a value         |
| `$push`      | Append to array field            |

## 📚 9. Working with Users & Orders (Example)

```python
users = db["users"]
orders = db["orders"]

# Insert user
user_id = users.insert_one({"email": "bart@example.com"}).inserted_id

# Insert order referencing user
orders.insert_one({
    "user_id": user_id,
    "items": [
        {"name": "Mouse", "qty": 2},
        {"name": "Keyboard", "qty": 1}
    ],
    "total": 69.97
})
```

## 🧪 10. Testing & Tips

<ul>
    <li>Use MongoDB Compass to visually check your data.</li>
    <li>Collections and fields are created automatically when you insert.</li>
    <li>Use <code>_id</code> field for document IDs (MongoDB auto-generates it unless provided).</li>
    <li>Always sanitize user input if building for the web.</li>
</ul>

## Summary Table

| **SQL Concept** | **MongoDB (PyMongo)**         |
|------------------|-------------------------------|
| Table            | Collection                    |
| Row              | Document                      |
| Column           | Field                         |
| Primary Key      | `_id`                         |
| Query            | `find()`, `find_one()`        |
| Insert           | `insert_one()`, `insert_many()` |
| Update           | `update_one()`, `update_many()` |
| Delete           | `delete_one()`, `delete_many()` |
