# docker-postgresql-postgis

This project provides a PostgreSQL/PostGIS environment using Docker on macOS (Apple Silicon).
You connect to the database using local pgAdmin, QGIS, or any other SQL client.

## Features

- PostgreSQL 16 with PostGIS (installed via custom image)
- Isolated Docker environment (no local pollution)
- Data persisted inside the project folder
- Works natively on Apple Silicon (arm64)
- Connect via `127.0.0.1:5432` from local tools

Directory Structure
```
.
├─ compose.yml
├─ Dockerfile
├─ .env
├─ initdb/
│   └─ 01-create-ext.sql
└─ _data/
    └─ postgres/   (created automatically)
```

## Build & Run
```
# Build custom PostGIS image
docker compose build

# Start database
docker compose up -d

# Stop
docker compose down

# Remove all data (reset)
docker compose down -v && rm -rf _data/postgres
```

## Connect with pgAdmin (Local App)

1. Open pgAdmin.

2. Register a new server:
    - Name: Local PostGIS (Docker)
    - Host: 127.0.0.1
    - Port: 5432
    - Maintenance DB: postgres
    - Username: value from .env
    - Password: value from .env

## Notes

- Docker Desktop should be allocated 8–12GB RAM for better PostGIS performance.
- To adjust PostgreSQL performance settings, modify the command: section in compose.yml.
