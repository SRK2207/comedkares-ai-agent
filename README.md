# ComedKares – Multilingual AI Appointment Booking Agent

Plug-and-play, multilingual (English, Hindi, Kannada), voice-first Agentic AI receptionist for healthcare clinics.

## Authoritative Docs

- [PROJECT_BIBLE.md](PROJECT_BIBLE.md) — Project vision, rules, team ownership, and quality gates.
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) — System architecture, module boundaries, concurrency & safety guarantees.
- [docs/DATABASE_SCHEMA.md](docs/DATABASE_SCHEMA.md) — PostgreSQL schema, constraints, and migration notes.
- [docs/API_CONTRACTS.md](docs/API_CONTRACTS.md) — REST API contracts and `ClinicAdapter` interface.

## Configured Stack

- **Frontend:** Next.js, TypeScript, Tailwind CSS (`frontend/`)
- **Embeddable Widget:** Lightweight clinic embed bundle (`widget/`)
- **Backend:** Python FastAPI (`backend/`)
- **Database:** Local PostgreSQL (`database/migrations/`, `database/seed/`)
- **AI & Voice:** Configurable LLM (tool calling) + STT / TTS APIs
- **Payments:** Razorpay Sandbox (server-side HMAC verification + idempotency)
- **Integrations:** Google Calendar Adapter & Mock Clinic REST API Adapter

## Quick Setup (Phase 1–2 Baseline)

1. Copy `.env.example` to `.env` and fill in your local PostgreSQL credentials, LLM/STT/TTS API keys, Razorpay test keys, and Google Calendar credentials.
2. Ensure local PostgreSQL is running and create the database:
   ```sql
   CREATE DATABASE comedkares;
   ```
3. Apply initial schema and seed data:
   ```bash
   psql "$DATABASE_URL" -f database/migrations/001_initial_schema.sql
   psql "$DATABASE_URL" -f database/seed/001_seed_clinics.sql
   ```
4. Backend dependencies are listed in `backend/requirements.txt`.

## Git Workflow

- Never commit directly to `main`.
- Branch from `main` per feature (`feat/<member>-<topic>`), run tests, and open a Pull Request.
- Coordinate before modifying `database/migrations/` or `docs/API_CONTRACTS.md`.
