# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Spendly" — a Flask + SQLite expense tracker built as a step-by-step teaching scaffold. Much of it is intentionally unimplemented; placeholders are labelled with the step number they belong to (e.g. "coming in Step 3").

## Commands

```bash
source venv/bin/activate          # venv is local (gitignored)
pip install -r requirements.txt
python app.py                     # dev server, debug=True, http://localhost:5001 (port 5001, not Flask's default 5000)
pytest                            # pytest + pytest-flask are installed; no tests exist yet
pytest path/to/test_file.py::test_name   # single test
```

No linter or build step is configured.

## Architecture

- `app.py` — single Flask app with all routes. `/`, `/register`, `/login` render templates; `/logout`, `/profile`, `/expenses/add`, `/expenses/<int:id>/edit`, `/expenses/<int:id>/delete` are string-returning placeholders to be replaced step by step. There are no POST handlers, sessions, or secret key yet.
- `database/db.py` — currently only a comment spec for Step 1: `get_db()` (SQLite connection with `row_factory` and foreign keys on), `init_db()` (`CREATE TABLE IF NOT EXISTS`), `seed_db()` (sample data). The SQLite file is `expense_tracker.db` (gitignored).
- `templates/` — Jinja templates extending `base.html` (navbar, `title`/`head`/`content` blocks, Google Fonts). Links use `url_for('<endpoint>')`, where endpoint names are the route function names in `app.py`.
- `static/css/style.css` (single stylesheet) and `static/js/main.js` (currently empty).

When implementing a placeholder route, keep its existing function name, since templates link to it via `url_for`.
