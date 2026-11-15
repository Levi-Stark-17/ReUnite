# Smart Lost & Found — React + Python + MySQL

This version keeps the existing React UI and replaces Firebase/Express with a Python FastAPI backend and MySQL database. The Python weighted matching engine is retained.

## Stack
- React + TypeScript + Vite
- Python 3.11+ / FastAPI
- SQLAlchemy + PyMySQL
- MySQL 8+
- JWT admin authentication
- Python matching engine

## Setup
1. Create MySQL database/user and run `database/schema.sql`.
2. Copy `.env.example` to `.env` and set `DATABASE_URL` and `SECRET_KEY`.
3. Install Python dependencies: `pip install -r backend/requirements.txt`.
4. Seed demo categories, reports and admin: `python scripts/seed.py`.
5. Start API: `uvicorn backend.app.main:app --reload --port 8000`.
6. Install frontend dependencies: `npm install`.
7. Start frontend: `npm run dev`.

## Default development admin
- Email: `admin@lostandfound.local`
- Password: `Admin@12345`

Change this immediately for any non-demo deployment.

## OTP development mode
With `DEV_MODE=true`, OTPs are **printed only in the FastAPI server console**. They are not returned to the browser. Replace the console integration with a real email/SMS provider for production.

## Architecture
React → REST API → FastAPI → Service/Business Logic → SQLAlchemy → MySQL.
The matching engine is invoked server-side and match records are persisted in MySQL.

## Requirements coverage
The implementation is structured around FR-01–FR-23 and the specified Lost-only OTP, admin approval, matching, claims, handover and unclaimed-collection workflows. See the supplied consolidated requirements PDF for the authoritative acceptance criteria.
