# Task 4 — Frontend & Backend Integration

Connects the Task 1 frontend to the Task 2/3 backend using `fetch()` and async/await — no page reloads, real error handling.

## What this demonstrates
- **Live data loading**: on page load, the frontend fetches Hero, About, Skills, Experience, Projects, and Contact Info from the API in parallel (`Promise.all`) and renders them into the DOM
- **Graceful degradation**: if the backend is unreachable, the page falls back to static placeholder content instead of showing a blank/broken page
- **Real error handling**: every fetch is wrapped in try/catch, checks `response.ok` before trusting the result, and shows the user a clear message rather than failing silently
- **Working contact form**: submissions are validated client-side, then POSTed to the backend and persisted to the database — not just simulated
- **XSS-safe rendering**: all text pulled from the API is escaped before being inserted into the DOM
- **CORS configured correctly** between the frontend (served separately) and the backend API

## How to run
1. Start the backend (see `Backend/README.md` equivalent setup — `pip install -r requirements.txt`, `python seed.py`, `uvicorn app.main:app --reload`)
2. Serve the `Frontend/` folder with any static server (e.g. `python -m http.server 5500`)
3. Open `index.html` in the browser — content loads live from the running backend

## Files
- `Frontend/index.html`, `index_Style.css`, `index_Script.js` — the integrated frontend
- `Backend/` — the API being called (identical to Task 2/3)
