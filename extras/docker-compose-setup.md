# Quick tutorial — Run the Postgres + pgAdmin Docker Compose

This brief guide shows how to install Docker (and WSL on Windows if needed), start the provided Docker Compose stack, and connect with `psql` and pgAdmin.

Files:
- Docker Compose: [extras/docker-compose.yaml](extras/docker-compose.yaml)

1) Install Docker
- macOS: install Docker Desktop from https://www.docker.com/products/docker-desktop and follow the installer.
- Windows: install Docker Desktop and enable WSL2 integration if prompted. If you don't have WSL2, follow Microsoft's WSL installation guide: https://learn.microsoft.com/windows/wsl/install.
- Linux: install Docker and Docker Compose following your distro's docs (example for Ubuntu):

```bash
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl enable --now docker
```

2) Start the stack
- From the repo root where `extras/docker-compose.yaml` is located, run:

```bash
# Use Docker Compose v2 syntax (recommended)
docker compose -f extras/docker-compose.yaml up -d

# Confirm containers are running
docker compose -f extras/docker-compose.yaml ps
```

The Compose file starts two services:
- `postgres-db`: Postgres 16 with DB `learning_db`, user `admin`, password `secretpassword`.
- `pgadmin`: pgAdmin web UI available on port `8080` with credentials `admin@example.com` / `adminpassword`.

3) Connect with `psql` (local machine)
- Install the `psql` client if you don't have it (macOS: `brew install libpq` and `brew link --force libpq`; Ubuntu: `sudo apt install -y postgresql-client`).
- Connect using:

```bash
psql -h localhost -p 5432 -U admin -d learning_db
# when prompted, enter: secretpassword
```

Common `psql` commands:

```sql
\l           -- list databases
\c learning_db  -- connect to learning_db
\dt          -- list tables
\d tablename -- show table schema
SELECT now();
CREATE TABLE test_demo(id serial PRIMARY KEY, txt text);
INSERT INTO test_demo(txt) VALUES('hello');
SELECT * FROM test_demo;
```

4) Connect with pgAdmin (web UI)
- Open http://localhost:8080 in your browser.
- Log in with:
  - Email: `admin@example.com`
  - Password: `adminpassword`
- Add a new server (right-click Servers → Create → Server):
  - General: Name = PostgresLab
  - Connection:
    - Hostname/address = postgres-db  (when connecting from pgAdmin container)
    - Port = 5432
    - Maintenance DB = learning_db
    - Username = admin
    - Password = secretpassword

Note: if you connect from your host machine's pgAdmin instance or a local pgAdmin app, use `localhost` as Hostname instead of `postgres-db`.

5) Useful Docker commands

```bash
# View logs
docker compose -f extras/docker-compose.yaml logs -f postgres-db

# Stop the stack
docker compose -f extras/docker-compose.yaml down

# Remove volumes (data will be lost)
docker compose -f extras/docker-compose.yaml down -v
```

6) Troubleshooting & tips
- Port conflicts: if port 5432 or 8080 is in use, edit `extras/docker-compose.yaml` ports before starting.
- Docker Desktop networking: on macOS and Linux, use `localhost` from the host; when configuring pgAdmin inside the Compose stack, use the service name `postgres-db` as the host.
- Data persistence: the Compose file mounts a named volume `postgres_data` so Postgres data survives restarts; removing volumes with `-v` will delete data.

7) Security note
- The Compose file uses simple credentials for lab purposes. Do not use these credentials in production. Consider using `.env` files and Docker secrets for real deployments.

That's it — you should now be able to run the Postgres + pgAdmin environment, connect with `psql` or pgAdmin, and start loading schemas (e.g., your Sakila-derived schema for the final project).
