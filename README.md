# Nitro Velocity 3D — with real backend, database & login

A browser-based 3D racing game (Three.js) with a real Node.js/Express API,
PostgreSQL database, bcrypt password hashing and JWT-based login — so a
player's profile, car, paint, wheels, best score and cash follow them to
any device, not just the browser they played in.

Controls: W/Arrow Up accelerate, S/Arrow Down brake/reverse, A/D or
Left/Right steer, Space nitro, P pause. Mobile touch controls included.

## What runs where
- **`web`** — nginx serving the static game (`index.html`, `assets/`) and
  reverse-proxying `/api/*` to the backend.
- **`api`** — Node/Express server (`backend/server.js`) with
  `/api/auth/register`, `/api/auth/login`, `GET /api/save`,
  `PUT /api/save`.
- **`db`** — PostgreSQL 16. Schema (`backend/schema.sql`) is applied
  automatically on first boot.

## Run everything locally
```
docker compose up --build
```
Then open **http://localhost:8080**.

- Postgres data persists in a named Docker volume (`db_data`) between
  restarts.
- The API listens on port 4000, the web/nginx container on 8080 (mapped
  to its internal port 10000).

## How login works in the game
On the start screen, enter a **Player ID** and a **password**:
- If that Player ID doesn't exist yet, a new account is created
  automatically (same "create / enter profile" flow as before).
- If it exists, the password is checked against the stored bcrypt hash.
- On success you get a JWT (valid 30 days) stored in the browser, and
  your car/paint/wheels/best score/cash are pulled from the database.
- **Leaving the password blank** still works — that's guest/offline
  mode, same as the original build (progress only saved to
  `localStorage` on that device).

## Deploying for free
- **Database**: a free Postgres instance from Render, Railway, Neon or
  Supabase. Set `DATABASE_URL` on the `api` service to that connection
  string.
- **API**: deploy `backend/` as a Docker/Node web service (Render,
  Railway, Fly.io free tiers all work). Set `JWT_SECRET` to a long
  random value — **do not use the default in production**.
- **Frontend**: deploy the root (`Dockerfile` + `nginx.conf`) the same
  way as before; just make sure `nginx.conf`'s `/api/` proxy target
  points at your deployed API's URL instead of the local `api:4000`
  Docker service name.

## Security notes
- Passwords are hashed with bcrypt (10 rounds) — never stored in plain
  text.
- Change `JWT_SECRET` and the Postgres password in `docker-compose.yml`
  before deploying anywhere public.
- This is still a hobby-scale setup (no rate limiting, no email
  verification/password reset). Fine for a personal project or small
  audience; a larger production launch would want those added.
