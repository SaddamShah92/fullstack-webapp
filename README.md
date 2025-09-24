# Full Stack WebApp (Django + React)

Short one-line description of the project.

## Tech stack
- Backend: Python, Django, Django REST Framework
- Frontend: React, Vite
- DB: SQLite (dev) / Postgres (prod)
- Package managers: pip, npm

## Quick start (local)
1. Backend
   ```bash
   cd backend
   python -m venv env
   source env/bin/activate         # or .\env\Scripts\activate on Windows
   pip install -r requirements.txt
   cp ../.env.example .env         # fill in values
   python manage.py migrate
   python manage.py runserver


Environment

Copy .env.example -> .env and fill values.

Do not commit .env to version control.

Contributing

Use feature branches: feature/<short-description>

Work with Pull Requests and meaningful commit messages (feat:, fix:, chore:).

License

MIT


---

# 8) Small professional practices (helpful for interviews / portfolio)
- **Branching:** Use `main` as protected production branch. Create feature branches `feature/login` or `fix/api-auth`. Open PRs even for small changes — this shows good process.  
- **Commit messages:** Follow Conventional Commits format (e.g., `feat: add user registration`, `fix: correct token refresh`).  
- **Pre-commit hooks:** Use `pre-commit` to run formatters and linters (black, isort, eslint). Example add later.  
- **CI:** Add a small GitHub Actions workflow that runs tests and builds the frontend on PRs. I can provide a starter CI yaml.  
- **Secrets:** Store deployment keys and API keys in GitHub Secrets for Actions, never in `.env` committed.

---

# 9) Optional: Minimal GitHub Actions CI (starter)
Create `.github/workflows/ci.yml`:

```yaml
name: CI

on: [push, pull_request]

jobs:
  backend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Python
        uses: actions/setup-python@v4
        with: python-version: '3.11'
      - name: Install deps
        run: |
          cd backend
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Run tests
        run: |
          cd backend
          python manage.py test --verbosity=1

  frontend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '18'
      - name: Install & build
        run: |
          cd frontend
          npm ci
          npm run build
