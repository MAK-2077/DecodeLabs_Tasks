# Task 2 — Backend API Development

A backend API built with **Python + FastAPI + SQLite**.

> **Note:** This backend was built with database persistence from the start (SQLAlchemy ORM), so this same codebase also satisfies Task 3's database integration requirements — see that folder for the schema/constraints-focused writeup of the identical code.

## What this demonstrates
- **RESTful API design**: resources named as nouns (`/projects`, not `/getProjects`), HTTP methods carrying the verb (GET/POST/PUT/DELETE/PATCH)
- **Full CRUD** across 7 resources: Hero, About, Skills, Experience, Projects, Contact Info, Contact Messages
- **Input validation**: automatic via Pydantic — required fields, length limits, email format — rejecting bad requests before any business logic runs
- **Correct HTTP status codes**: `200` OK, `201` Created, `204` No Content, `401` Unauthorized, `404` Not Found, `422` Validation Error, `423` Locked, `428` Precondition Required
- **Authentication**: JWT bearer tokens protecting all write operations; GET endpoints stay public
- **Self-documenting**: FastAPI auto-generates interactive Swagger docs at `/docs`
- **Security hardening beyond the brief's minimum**: login lockout after repeated failed attempts, email-based two-factor confirmation on every write action, security response headers

## Setup
```bash
pip install -r requirements.txt
python seed.py
uvicorn app.main:app --reload
```
Visit `http://127.0.0.1:8000/docs` for interactive API documentation.

## Files
- `app/main.py` — FastAPI app entrypoint, middleware, routing
- `app/models.py` — SQLAlchemy database models
- `app/schemas.py` — Pydantic request/response validation schemas
- `app/auth.py` / `app/two_factor.py` — authentication and 2FA logic
- `app/routers/` — one router per resource
- `seed.py` — populates the database with initial content and an admin account
