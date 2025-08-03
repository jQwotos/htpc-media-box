Just another HTPC Media Box Docker Compose

# Tech and stuff
- Docker for containers
- Docker compose for multi-containers
- Caddy as the reverse proxy to get into each app and simplifying HTTPS to make browsers happy
- Tailscale for VPN
- Jellyfin for media hosting
- Beszel for system monitoring
- Flaresolverr for Cloudflare mitigation
- Prowlarr as an indexer manager
- Radarr for movies
- Sonarr for TV series
- qBittorrent as torrent client

I run tailscale natively on the host, and provide the Caddy container access to the tailscaled daemon through tailscaled.sock. This let's it can retrieve and renew the Tailscale TLS certificate for HTTPS.

When setting up Radarr, Sonarr, Prowlarr, use the container names since they're all in the same default network for the project.

Note that you won't be able to access any of the services without Tailscale since Caddy is expecting them to come from a specific tailscale MagicDNS domain.

Replace the `machine.tailscaledomain.ts.net` inside of the `Caddyfile` with your MagicDNS domain.

Copy the `.env.template` to `.env` and change the LFS (large file storage) env variable to your largest mounted partition.

# Port Mappings

- 8191 – flaresolverr
- 9696 – prowlarr
- 7878 – radarr
- 8989 – sonarr
- 8080 – qbittorrent
