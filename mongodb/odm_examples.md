# 📝 MongoDB ODM Notes (MongoEngine + Python)

---

## 📦 What is an ODM?

- **ODM = Object Document Mapper**
- Similar to SQLAlchemy ORM, but for **NoSQL (MongoDB)**
- Maps **MongoDB documents to Python classes**
- No need to write raw MongoDB queries

---

## ⚙️ Setup Instructions

### 1. Install MongoEngine:
```bash
pip install mongoengine
```
### 2. Connect to MongoDB:
```python
from mongoengine import connect

# Connect to local MongoDB
connect('ecommerce_db')
```

---

## Define Models(Collections)
```python
from mongoengine import Document, StringField, FloatField, IntField

class Product(Document):
    name = StringField(required=True)
    description = StringField()
    price = FloatField(required=True)
    stock = IntField(default=0)
```

---

## Insert Documents
```python
# Create and save a product
p = Product(
    name="Bluetooth Headphones",
    description="Wireless and noise-cancelling",
    price=89.99,
    stock=10
)
p.save()
```

---

## Query Documents
```python
# Get all products
products = Product.objects()

# Filter by name
headphones = Product.objects(name="Bluetooth Headphones").first()

# More advanced filters
cheap = Product.objects(price__lt=50)
```

---

## Update Documents
```python
# Update stock
headphones.stock += 5
headphones.save()
```

---

## Delete Documents
```python
headphones.delete()
```
Or delete in bulk:
```python
Product.objects(price_lt=10).delete()
```

---

## Relationships (Reference Fields)
```python
from mongoengine import ReferenceField, ListField

class User(Document):
    email = StringField(required=True)
    name = StringField()

class Order(Document):
    user = ReferenceField(User)
    items = ListField(ReferenceField(Product))
```

---

## Sample Order Creation
```python
u = User(email="bart@example.com", name="Bart").save()
p1 = Product.objects(name="Bluetooth Headphones").first()
p2 = Product.objects(name="Wireless Mouse").first()

order = Order(user=u, items=[p1, p2])
order.save()
```

---

## ✅ Best Practices

<ul>
  <li>Use .save() to persist individual documents</li>

  <li>Use .update()/.update_one() for performance on bulk edits</li>

  <li>Use .delete() for removals</li>

  <li>Keep models lean; MongoDB is schema-less, but good structure still matters</li>
</ul>

---

## 💡 Useful Queries
|**Query**|**Description**
|-------|-------|
|<code>Product.objects()</code>|All documents|
|<code>Product.objects(name="X")</code>|Filter by field|
|<code>Product.objects(price__gt=20)</code>|Comparison operators|
|<code>Product.objects().order_by('-price')</code>|Sort results|
|<code>Product.objects().limit(5)</code>|Limit results|

---

## MongoDB Compass (Optional GUI)
<ul>
    <li>
        Download: https://www.mongodb.com/try/download/compass
        </li>
    <li>
        Allows you to view, browse, and debug your MongoDB collections visually
    </li>
</ul>

---

## Summary

|**Concept**|**MongoDB ODM Equivalent**|
|-|-|
|Table|Collection|
|Row|Document|
|Column|Field|
|Primary Key|<code>_id</code> (auto-assigned)|
|Foreign Key|<code>ReferenceField</code>|
|Relationships|Reference/List of References|
