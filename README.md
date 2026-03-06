# LoginProject

Simple signup/login/logout demo with Node.js, Express, PostgreSQL (Supabase), sessions, and a basic HTML page.

## Stack
- Node.js + Express
- PostgreSQL via Supabase (pooled connection)
- express-session + connect-pg-simple
- Frontend: plain HTML/JS in public/index.html

## Setup
1) Install deps:
   npm install

2) Env file:
   - Copy .env.example to .env
   - Fill in:
     DATABASE_URL=postgres://postgres:<PASSWORD>@<HOST>.pooler.supabase.com:6543/postgres
     SESSION_SECRET=<any-long-random-string>
     PORT=3000

3) Create session table in Supabase (SQL editor):
   create table if not exists session (
     sid varchar primary key,
     sess json not null,
     expire timestamp(6) not null
   );
   create index if not exists idx_session_expire on session (expire);

4) Run dev server:
   npm run dev

## Usage
- Open http://localhost:3000
- Sign Up (email + password >= 8 chars)
- Log In with same credentials
- “Who am I?” checks the session
- Log Out ends the session

## Notes
- Uses Supabase pooled URL (port 6543).
- SSL cert checks are disabled in code for local dev (`rejectUnauthorized: false`).
- Keep real secrets out of git; only commit .env.example.
