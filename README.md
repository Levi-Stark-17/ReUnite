# Smart Lost & Found Management System

A migrated version of the supplied Smart Lost & Found project using the existing React frontend, a Python FastAPI backend, MySQL, and the Python weighted matching engine.

## Architecture
React + TypeScript → FastAPI REST API → Service/Business Logic → SQLAlchemy → MySQL

The public side is account-free. Lost reports require OTP verification; Found reports do not. Admin APIs require JWT authentication. Matching runs server-side in Python.

## Run
### 1) MySQL
Run `database/schema.sql` in MySQL 8+.

### 2) Python backend
```bash
cd backend
pip install -r requirements.txt
cd ..
cp .env.example .env
python scripts/seed.py
uvicorn backend.app.main:app --reload --port 8000
```

### 3) React frontend
```bash
npm install
npm run dev
```

Vite proxies `/api` to `http://localhost:8000`.

## Development admin
`admin@lostandfound.local` / `Admin@12345`

Change the seeded password before any non-demo deployment.

## OTP
With `DEV_MODE=true`, generated OTP values are printed to the FastAPI server console only. They are not returned to the browser. Production should connect `otp.py` to a real email/SMS provider.

## Requirements coverage
The project is organized around the supplied FR-01–FR-23 requirements, including Lost-only OTP, Found reporting, admin approval before public visibility, report tracking, weighted Python matching, claim verification, controlled handover, audit logs, analytics, and the Unclaimed → Open for Collection → Collection Request → Collected → Closed workflow.

See `README_MYSQL.md` and the supplied consolidated requirements PDF for more detail.
