# 🔨 Self-Hosted Git: Forgejo

I am migrating my repositories from GitHub to a self-hosted Forgejo instance running on a dedicated Proxmox VM. This reduces dependency on external services and grants full control over my code storage.

## ⚙️ VM Configuration

- **OS**: Linux (Debian/Ubuntu)
- **Role**: Git Server
- **Access**: Reverse Proxy via Traefik (planned)

## 🐳 Docker Composition

The service is deployed using Docker Compose for easy management and upgrades.

```yaml
services:
  server:
    image: codeberg.org/forgejo/forgejo:13.0.3
    container_name: forgejo
    environment:
      - USER_UID=1000
      - USER_GID=1000
    restart: always
    networks:
      - forgejo
    volumes:
      - ./forgejo:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports:
      - '3000:3000'
      - '222:22'

networks:
  forgejo:
    external: false
```

## 💾 Storage & Backup

- **Data**: All repositories and database files are stored in `./forgejo` which is mounted to `/data` inside the container.
- **Backup**: This directory is included in the regular VM file backup schedule.