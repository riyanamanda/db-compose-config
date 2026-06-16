# Local Development Data Stack

This repository provides a local development stack using Docker/Podman Compose.

Services included:
- PostgreSQL 17
- MySQL 8.4
- Redis 7
- RabbitMQ 4 (with management UI)
- MinIO (S3-compatible object storage)

## Prerequisites

- Docker Desktop with `docker compose`, or
- Podman with `podman-compose`

## Start The Stack

Docker:

```bash
docker compose -f compose.yml up -d
```

Podman:

```bash
podman-compose -f compose.yml up -d
```

## Stop The Stack

Docker:

```bash
docker compose -f compose.yml down
```

Podman:

```bash
podman-compose -f compose.yml down
```

## Services, Ports, And Credentials

### PostgreSQL
- Host: `localhost`
- Port: `5432`
- Username: `postgres`
- Password: `postgres`
- Container: `postgres_db`

### MySQL
- Host: `localhost`
- Port: `3306`
- Username: `root`
- Password: `root`
- Container: `mysql_db`

### Redis
- Host: `localhost`
- Port: `6379`
- Container: `redis_db`

### RabbitMQ
- AMQP Port: `5672`
- Management UI: `http://localhost:15672`
- Username: `admin`
- Password: `admin`
- Container: `rabbitmq`

### MinIO
- API: `http://localhost:9000`
- Console: `http://localhost:9001`
- Access Key: `minioadmin`
- Secret Key: `minioadmin`
- Container: `minio`

## Persistent Data

The following directories/volumes persist service data:
- `./postgres_data`
- `./mysql_data`
- `./minio_data`
- `redis_data` (named volume)
- `rabbitmq_data` (named volume)

## Reset All Data

Warning: this permanently removes all local database/message/object data for this stack.

Docker:

```bash
docker compose -f compose.yml down -v
```

Podman:

```bash
podman-compose -f compose.yml down -v
```

Then remove bind-mounted data directories if needed:

```bash
rm -rf postgres_data mysql_data minio_data
```

On Windows PowerShell:

```powershell
Remove-Item -Recurse -Force postgres_data, mysql_data, minio_data
```