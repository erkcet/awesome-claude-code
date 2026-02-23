# CLAUDE.md — Homelab / Infrastructure Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Machines

### Server 1

- **Hostname:** <!-- e.g., media-server -->
- **OS:** <!-- e.g., Ubuntu 24.04 LTS -->
- **IP (Local):** <!-- e.g., 192.168.1.100 -->
- **IP (Tailscale):** <!-- e.g., 100.x.x.x -->
- **SSH:** `ssh user@192.168.1.100`
- **CPU / RAM / Storage:** <!-- e.g., i5-12400, 32 GB, 4x4TB RAIDZ1 -->

## Services

| Service | Type | Port | Config | Notes |
|---------|------|------|--------|-------|
| Plex | systemd | 32400 | `/var/lib/plexmediaserver/...` | Media streaming |
| Sonarr | systemd | 8989 | `/var/lib/sonarr/config.xml` | TV show management |
| Radarr | systemd | 7878 | `~/.config/Radarr/config.xml` | Movie management |
| Traefik | Docker | 80/443 | `/opt/traefik/traefik.yml` | Reverse proxy |

## API Keys

<!-- Store sensitive keys here only if this file is private / not committed to a public repo -->

| Service | Key |
|---------|-----|
| Sonarr | `your-api-key` |
| Radarr | `your-api-key` |

## Storage / Paths

| Purpose | Path |
|---------|------|
| Movies | `/tank/movies` |
| TV Shows | `/tank/tv` |
| Downloads | `/tank/downloads` |
| Backups | `/opt/backups` |

## Common Commands

```bash
# Check all services
systemctl list-units --type=service --state=running

# Docker containers
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"

# ZFS pool status
zpool status

# Disk usage
df -h /tank

# Restart a service
sudo systemctl restart sonarr

# View logs
journalctl -u sonarr -f --no-hostname
```

## Backups

- **Script:** `/opt/backups/backup.sh`
- **Schedule:** Weekly, Sundays at 4 AM (crontab)
- **Retention:** 4 weeks
- **Location:** `/opt/backups/`

## Network

- **Domain:** <!-- e.g., home.example.com -->
- **DNS:** <!-- e.g., Cloudflare, Pi-hole -->
- **VPN:** <!-- e.g., Tailscale, WireGuard -->
- **Reverse Proxy:** <!-- e.g., Traefik, Caddy, nginx -->

## Notes

<!-- Gotchas, workarounds, things Claude should know -->
