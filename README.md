# Lab Hub

Lab Hub is a single-page "control centre" dashboard for a home lab. A static page (`index.html`) shows cards for the services running on a few machines and pings each one from the browser to show whether it is up. An nginx container serves the page and reverse-proxies `/mc/` to the Mission Control service (a separate repository, `mission-control`).

This was an experiment and has been superseded; the repository is kept for reference. The service addresses in the page are `192.0.2.x` documentation placeholders, so the status dots will not turn green until you replace them with your own LAN addresses.

## Stack

- Plain HTML, CSS and JavaScript (no build step), with a retro "CRT" visual theme
- nginx (static hosting and reverse proxy)
- Docker Compose

## Running

Lab Hub expects a sibling checkout of `mission-control` (`../mission-control`), which the compose file builds.

```bash
cp .env.example .env        # set OC_TOKEN
export SSH_USER=<ssh user for your lab machines>   # defaults to "user"
docker compose up --build
# open http://localhost:8090  (Mission Control is proxied at /mc/)
```

Edit `index.html` and the `PI1_HOST` / `PI2_HOST` / `PI3_HOST` values in `docker-compose.yml` to match your own hosts.

## Project layout

- `index.html` - the dashboard (cards, clock, client-side up/down checks)
- `nginx.conf` - serves the page and proxies `/mc/` to the Mission Control container
- `docker-compose.yml` - nginx plus the Mission Control build

## Status

Superseded and no longer maintained.
