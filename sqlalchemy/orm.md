# SQLAlchemy ORM – Beginner Notes

---

## 1. What is SQLAlchemy ORM?

- **ORM (Object Relational Mapper)** allows you to work with the database using **Python classes** instead of raw SQL.
- Each **class = table**, and each **object = row** in that table.
- It simplifies CRUD operations while still letting you write SQL when needed.

---

## 2. Install SQLAlchemy

```bash
pip install sqlalchemy
```

---

## 3. Core Components

  1. **Engine:** Connects your app to the database.
  2. **Session:** Handles transactions and conversations with the database.
  3. **Base:** A class used to define your tables via Python classes.

---

## 4. Setting up the Database

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

# Connect to a database
engine = create_engine('sqlite:///example.db', echo=True)

# Base class for our models (tables)
Base = declarative_base()

# Session for interacting with DB
Session = sessionmaker(bind=engine)
session = Session()
```

---

## 5. Define Models (Tables)

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    username = Column(String, nullable=False, unique=True)
    email = Column(String, nullable=False, unique=True)

    # One-to-many relationship
    posts = relationship('Post', back_populates='author')

class Post(Base):
    __tablename__ = 'posts'

    id = Column(Integer, primary_key=True)
    user_id = Column(Integer, ForeignKey('users.id'))
    content = Column(String)

    # Relationship back to User
    author = relationship('User', back_populates='posts')
```

---

## 6. Create Tables

```python
Base.metadata.create_all(engine)
```

---

## 7. Insert Data

```python
# Create user
new_user = User(username="bart", email="bart@example.com")
session.add(new_user)
session.commit()

# Add a post
new_post = Post(content="Hello World!", author=new_user)
session.add(new_post)
session.commit()
```

---

## 8. Query Data

```python
# Get all users
users = session.query(User).all()
for user in users:
    print(user.username)

# Filter data
bart = session.query(User).filter_by(username='bart').first()
print(bart.email)

# Access related posts
for post in bart.posts:
    print(post.content)
```

---

## 9. Update Data

```python
user = session.query(User).filter_by(username='bart').first()
user.email = "new_bart@example.com"
session.commit()
```

---

## 10. Delete Data

```python
user = session.query(User).filter_by(username='bart').first()
session.delete(user)
session.commit()
```

