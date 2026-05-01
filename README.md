# Miru Discovery

Tiny static endpoint serving the current production backend URL for [Miru](https://mirulife.top).

Clients (DMG / APK) fetch `lookup.json` at startup to discover which VPS to connect to. This means the backend can move without redistributing binaries.

## How to rotate VPS

1. Edit `backend_url` in `lookup.json`
2. `git push` to main
3. GitHub Pages rebuilds (~1 min); Cloudflare CDN refreshes (60s TTL)
4. All clients connect to the new VPS on next startup

## Resilience

If this endpoint is unreachable, clients fall back to a bundled-default URL hard-coded at build time. So a Cloudflare/GitHub outage does **not** break existing installs — only delays VPS rotations.
