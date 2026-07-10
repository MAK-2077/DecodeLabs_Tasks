# Task 3 — Database Integration

Database persistence layer built with **SQLAlchemy ORM + SQLite**.

> **Note:** This is the same backend codebase as Task 2 — the database layer was built in from the start rather than bolted on afterward. This README highlights the schema/persistence-specific aspects that this week's brief asks for.

## What this demonstrates
- **Schema design**: 9 tables (`admin_user`, `pending_actions`, `hero`, `about`, `skill_categories`, `experience_items`, `projects`, `contact_info`, `contact_messages`) with Primary Keys on every table
- **Integrity constraints enforced at the database level**, not just in application code:
  - `NOT NULL` on required fields (e.g. project titles)
  - `UNIQUE` on the admin username
  - `CHECK` constraints (e.g. `sort_order >= 0`, minimum contact-message length) — verified to actually reject bad data by testing direct database inserts that bypass the API layer entirely
- **ORM bridge**: SQLAlchemy translates Python objects to database rows automatically (`db.query(Project).filter(...)`) instead of hand-written SQL strings
- **Full CRUD mapped correctly to SQL**: POST→INSERT, GET→SELECT, PUT→UPDATE, DELETE→DELETE
- **SQL injection protection**: every query goes through SQLAlchemy's parameterized query builder — no raw string concatenation anywhere in the codebase

## Setup
```bash
pip install -r requirements.txt
python seed.py
uvicorn app.main:app --reload
```

## Files
- `app/models.py` — table definitions, keys, and constraints
- `app/database.py` — SQLAlchemy engine/session setup
- `seed.py` — initial data population script
