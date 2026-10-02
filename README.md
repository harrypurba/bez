# Bez

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-harryopurba%2Fbez-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/harryopurba/bez)
[![GitHub](https://img.shields.io/badge/GitHub-harrypurba%2Fbez-181717?logo=github&logoColor=white)](https://github.com/harrypurba/bez)
[![Docker pulls](https://img.shields.io/docker/pulls/harryopurba/bez)](https://hub.docker.com/r/harryopurba/bez)
[![Image size](https://img.shields.io/docker/image-size/harryopurba/bez/latest)](https://hub.docker.com/r/harryopurba/bez)

Bez is a small and fast PostgreSQL client that runs in your browser.
It is one small Docker image. There is nothing else to install.

## Features

- Browse tables and their rows, with paging
- Insert, edit, clone, and delete rows
- Look at table structure
- Run your own SQL
- See the SQL that Bez runs for every action
- Copy selected table cells as tab-separated text

## See the SQL behind every action

Every time Bez runs SQL on your database, it shows that SQL in a bar at the bottom of the page.
This includes browsing, filtering, inserting, editing, cloning, deleting, and your own queries.

- Each entry shows the SQL, the values it used, how long it took, and how many rows it returned or changed.
- The values are listed under the SQL as `$1`, `$2`, and so on. This is how PostgreSQL receives them: the SQL and the values are sent separately.
- Click **copy as sql** to copy the SQL with the values already filled in. You can paste it into the SQL editor.
- If a statement fails, it stays in the log with its error message.
- The log keeps the last 200 entries in your browser. It is emptied when you reload the page. Click **clear** to empty it sooner.

The log can show real data from your tables. Close it before you share your screen.

## Quick start

```bash
docker run --rm -p 127.0.0.1:8080:8080 harryopurba/bez
```

Open http://localhost:8080 and type your database connection details.

## Try it with Docker Compose

This starts Bez and a test PostgreSQL database together.
Save this as `docker-compose.yml`:

```yaml
services:
  bez:
    image: harryopurba/bez
    ports:
      - "127.0.0.1:8080:8080"
    depends_on:
      - db

  db:
    image: postgres:17
    environment:
      POSTGRES_USER: demo
      POSTGRES_PASSWORD: demo
      POSTGRES_DB: demo
```

Run `docker compose up`, open http://localhost:8080, and connect with
host `db`, port `5432`, user `demo`, password `demo`, database `demo`.

## Connect to your database

Where is your database? Use the matching host name:

- **On your own computer:** use `host.docker.internal` as the host.
  On Linux, also add `--add-host=host.docker.internal:host-gateway` to the `docker run` command.
- **In another Docker container:** put both containers on the same Docker network.
  Then use the container name as the host.
- **On a remote or cloud server (RDS, Supabase, and so on):** paste a full connection string (DSN), for example:
  `postgres://user:password@host:5432/db?sslmode=require`

The form with host, port, user, and password always uses `sslmode=disable` (no TLS).
If your server needs TLS, use a connection string instead.

You can also start Bez already connected to a database:

```bash
docker run --rm -p 127.0.0.1:8080:8080 \
  -e DATABASE_URL="postgres://user:password@host.docker.internal:5432/db" \
  harryopurba/bez
```

## Settings

| Variable       | Default | What it does                                    |
|----------------|---------|-------------------------------------------------|
| `PORT`         | `8080`  | The port Bez listens on inside the container    |
| `DATABASE_URL` | not set | Connect to this database when Bez starts        |

## Image tags

- `latest` is the newest version.
- Version tags are also available on Docker Hub.

The image works on `linux/amd64` and `linux/arm64` (this includes Apple Silicon Macs and ARM servers).
The container runs as a normal user, not as root.

## Status

Bez supports PostgreSQL only for now.
