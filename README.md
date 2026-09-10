# OpenSpeak container image

This repository builds a multi-architecture container image from the
[`main` branch of Elektryczna-Owca/OpenSpeak](https://github.com/Elektryczna-Owca/OpenSpeak/tree/main).
The build uses the upstream `agenda-app/Dockerfile` without modifying the
application source.

The workflow runs daily, when its build configuration changes, and when
started manually. Images are published for `linux/amd64` and `linux/arm64` to:

```text
ghcr.io/whaleyarn/openspeak
```

Available tags:

- `latest` and `main`: the most recently built upstream `main` revision.
- `sha-<commit>`: an immutable tag identifying the upstream OpenSpeak commit.

## Run

OpenSpeak requires PostgreSQL. Set `DATABASE_URL` to your database connection
string when starting the container:

```bash
docker run -d \
  --name openspeak \
  -p 3001:3001 \
  -e DATABASE_URL="postgresql://USER:PASSWORD@HOST:5432/DBNAME" \
  --restart unless-stopped \
  ghcr.io/whaleyarn/openspeak:latest
```

The application listens on port `3001` and automatically applies pending
Prisma migrations at startup. See the
[upstream deployment documentation](https://github.com/Elektryczna-Owca/OpenSpeak#production-deployment)
for PostgreSQL, reverse proxy, and subpath configuration.

## License

OpenSpeak is licensed under the
[GNU General Public License v3.0](https://github.com/Elektryczna-Owca/OpenSpeak/blob/main/LICENSE).
