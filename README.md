<p align="center">
  <img src="assets/icon.png" alt="JDownloader logo" width="128">
</p>

<h1 align="center">aac-jdownloader</h1>

<p align="center">Self-hosted deployment definition for JDownloader 2, a download manager with a web interface.</p>

<p align="center">
  <a href="https://github.com/jlesage/docker-jdownloader-2"><img alt="Upstream" src="https://img.shields.io/badge/upstream-jlesage%2Fdocker--jdownloader--2-blue?logo=github"></a>
  <img alt="Image" src="https://img.shields.io/badge/image-jlesage%2Fjdownloader--2%3Av26.09.1-2496ED?logo=docker&logoColor=white">
  <a href="https://github.com/jlesage/docker-jdownloader-2/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-green"></a>
</p>

## About

JDownloader 2 is a download manager that handles many hosters and link types, with
features such as link grabbing, queue management, automatic extraction and bandwidth
control. This deployment runs JDownloader 2 inside a container and exposes its graphical
interface in the browser, so downloads can be managed from any device on the network.

Key features (as provided by upstream):

- Download manager with queue and bandwidth control
- Automatic extraction of archives after download
- Web-based access to the JDownloader interface (no client installation needed)
- Persistent configuration and download state in a single volume
- Dark mode for the web interface

## Upstream

- Project: <https://github.com/jlesage/docker-jdownloader-2>
- Application: <https://jdownloader.org>
- Container image: `jlesage/jdownloader-2:v26.09.1`
- License: MIT (upstream container project; JDownloader 2 itself has its own license)

## Quick start (Docker Compose)

The Compose file is rendered from `service.yml` by the App-as-Code template engine. For a
manual run, the external networks used for routing must exist first:

```bash
docker network create services-secured
docker network create services-exposed

docker compose up -d
```

The web interface is then available on port `5800`.

## Configuration

Environment variables (defaults from `service.yml`):

| Variable | Default | Description |
|---|---|---|
| `TZ` | `Europe/Berlin` | Time zone |
| `UMASK` | `000` | File creation mask for downloaded files |
| `DARK_MODE` | `1` | Enable dark mode in the web interface (`1` = on) |
| `PUID` | `1000` | User ID the application runs as |
| `PGID` | `1000` | Group ID the application runs as |
| `USER_ID` | `0` | User ID passed to the container |

No secrets are required for this service.

Ports:

| Port | Protocol | Purpose |
|---|---|---|
| `5800` | TCP | Web interface (`web`) |

Volumes:

| Mount | Description |
|---|---|
| `config` -> `/config` | JDownloader configuration and data |

## Deploy with App-as-Code

1. Edit `service.yml`. It is the single source of truth for image, ports, environment,
   volumes and per-stage overrides. Do not edit the rendered output.
2. Pushing to `main` (or a configured stage branch) runs the service pipeline, which renders
   the manifests with `aac-template-engine` and triggers the deployment.
3. Releases of this definition are published under <https://github.com/app-as-code/aac-jdownloader>.

## Credits and license

JDownloader 2 is developed by its respective authors. The container image is maintained by the
upstream container project and licensed under MIT. This repository only contains the deployment
definition and is not a fork of the application. The icon is taken from the dashboard-icons
collection; see [`assets/ICON_SOURCE.md`](assets/ICON_SOURCE.md) for sources and licenses.
