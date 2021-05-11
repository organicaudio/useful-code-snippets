# Dozzle - WebUI Log Viewer for Docker

Dozzle is a simple, lightweight application that provides you with a web based interface to monitor your Docker container logs live. It doesn’t store log information, it is for live monitoring of your container logs only.

## Links:
[dozzle.dev](https://dozzle.dev)
[github](https://github.com/amir20/dozzle)

## Getting Dozzle:
```
docker pull amir20/dozzle:latest
```

## Using Dozzle (via Docker Socket):
```

docker run --name dozzle -d --volume=/var/run/docker.sock:/var/run/docker.sock -p 6688:8080 amir20/dozzle:latest
Doz

```

## Using Docker (with Docker compose):
```
version: "3"
services:
  dozzle:
    container_name: dozzle
    image: amir20/dozzle:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 6688:8080
```

#### Environment variables and configuration

Dozzle follows the [12-factor](https://12factor.net/) model. Configurations can use the CLI flags or enviroment variables. The table below outlines all supported options and their respective env vars.

| Flag         | Env Variable         | Default |
| ------------ | -------------------- | ------- |
| `--addr`     | `DOZZLE_ADDR`        | `:8080` |
| `--base`     | `DOZZLE_BASE`        | `/`     |
| `--level`    | `DOZZLE_LEVEL`       | `info`  |
| n/a          | `DOCKER_API_VERSION` | not set |
| `--tailSize` | `DOZZLE_TAILSIZE`    | `300`   |
| `--filter`   | `DOZZLE_FILTER`      | `""`    |
| `--username` | `DOZZLE_USERNAME`    | `""`    |
| `--password` | `DOZZLE_PASSWORD`    | `""`    |
| `--key`      | `DOZZLE_KEY`         | `""`    |
