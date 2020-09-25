---
title: "SQLAlchemy and Postgres Tips & Tricks"
date: 2020-05-27T23:39:51-07:00
draft: true
---

This post is primarily documentation for my future self, but I felt like I should at least share it!


## Bulk Inserts with ON CONFLICT DO NOTHING

```python
import sqlalchemy

users: List[models.User] = []
users = [
    User(name='alice'),
    User(name='bob'),
]
user_dicts = [u.__dict__ for u in users]

# Batch all of the readings into a single INSERT INTO ... VALUES ([...]) statement
insert_stmt = sqlalchemy.dialects.postgresql.insert(
    models.User.__table__
).on_conflict_do_nothing()
engine.execute(insert_stmt, user_dicts)
```
