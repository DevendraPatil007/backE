PGADMIN — WHAT IT IS AND HOW TO INSTALL IT

1. What pgAdmin is
   pgAdmin is a graphical administration and management tool for
   PostgreSQL databases. Instead of writing raw SQL in a terminal
   (psql), it gives you a browser-based UI to view tables, run
   queries, manage users/roles, inspect schemas, and visualize query
   plans.

2. Installation options

   OPTION A: Desktop app (Windows/Mac/Linux) — simplest for local dev
   - Download the installer from the official site:
     https://www.pgadmin.org/download/
   - Run the installer for your OS (pgAdmin 4 is the current version).
   - It installs as a standalone desktop app that opens pgAdmin in an
     embedded browser window.

   OPTION B: Via pip (Python package, runs as a local web server)
```bash
pip install pgadmin4
```
   Then run it with:
```bash
pgadmin4
```
   This starts a local web server and opens pgAdmin in your default
   browser (usually at http://127.0.0.1:5050).

   OPTION C: Docker (common for teams/servers, avoids local install)
```bash
docker run -p 5050:80 \
  -e "PGADMIN_DEFAULT_EMAIL=admin@example.com" \
  -e "PGADMIN_DEFAULT_PASSWORD=yourpassword" \
  -d dpage/pgadmin4
```
   Then visit http://localhost:5050 — useful if you don't want pgAdmin
   installed directly on your machine, or you're already running
   Postgres in Docker too.

3. After installing
   - On first launch, pgAdmin asks you to set a master password (this
     is separate from your Postgres database password — it just locks
     the pgAdmin app itself).
   - You then add a "Server" connection: right-click Servers → Register
     → Server, and enter your Postgres host, port (default 5432),
     username, and password to connect to an actual database.

4. Which option to pick
   - Just working locally on your own machine → Option A (desktop app)
     is easiest, no terminal needed.
   - Already comfortable in Python/pip workflows → Option B.
   - Already using Docker for Postgres itself → Option C keeps
     everything containerized together.

     commands 
     python3 -m venv venv && source venv/bin/activate && pip install pgadmin4 && pgadmin4