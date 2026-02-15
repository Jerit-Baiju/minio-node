# minio-node

Single-node [MinIO](https://min.io/) deployment using Docker Compose.

This repo runs MinIO with:
- **S3 API** on container port `9000`
- **MinIO Console** on container port `9001`
- Persistent storage via a named Docker volume (`minio-data`)

## Prerequisites

- Docker Engine
- Docker Compose (v2)

## Files

- `docker-compose.yml` – MinIO service definition
- `.env.example` – example environment variables
- `.env` – local runtime values (not committed)

## Quick Start

1. Copy the env template:

```bash
cp .env.example .env
```

2. Start MinIO:

```bash
docker compose up -d
```

3. Check container status:

```bash
docker compose ps
```

4. View logs:

```bash
docker compose logs -f minio
```

## Access

Using the default values from `.env.example`:

- S3 API: `http://localhost:9010`
- Console: `http://localhost:9011`

Login credentials:
- Username: value of `MINIO_ROOT_USER`
- Password: value of `MINIO_ROOT_PASSWORD`

## Environment Variables

| Variable | Description | Example |
|---|---|---|
| `MINIO_PORT` | Host port mapped to MinIO S3 API (`9000` in container) | `9010` |
| `MINIO_CONSOLE_PORT` | Host port mapped to MinIO Console (`9001` in container) | `9011` |
| `MINIO_ROOT_USER` | MinIO admin username | `minioadmin` |
| `MINIO_ROOT_PASSWORD` | MinIO admin password | `minioadmin123` |
| `MINIO_SERVER_URL` | Public server URL used by MinIO in generated links | `https://mio1.caelium.in` |
| `MINIO_BROWSER_REDIRECT_URL` | Public console URL used for browser redirects | `https://mio1-console.caelium.in/` |

## Common Commands

Start:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

Stop and remove data volume (destructive):

```bash
docker compose down -v
```

Pull latest image:

```bash
docker compose pull
```

## Notes

- Data persists in the named Docker volume `minio-data`.
- If you run MinIO behind a reverse proxy or with HTTPS, keep `MINIO_SERVER_URL` and `MINIO_BROWSER_REDIRECT_URL` aligned with your public domain.
- For production, replace default credentials with strong secrets.
