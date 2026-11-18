# Services and ports

All host endpoints below use the placeholder `HOST_IP`. These are historical records, not a fresh port scan. “Screenshot” means displayed by the supplied dashboard, not independently validated service health. Unknown ports are deliberately not guessed.

| Service | Runtime / owner | Port or endpoint | Evidence / dependency |
|---|---|---|---|
| SSH | Host | TCP 22, verify | Manual; Linux account ADMIN_USER |
| Cockpit | Host | HTTPS 9090 | Manual; Linux login; 45Drives file-sharing integration |
| Samba | Host | TCP 445 | Manual; external SSD/HDD mounts; exact share names unknown |
| Docker | Host daemon | Local socket; no remote API established | Apps and Wings depend on it |
| Portainer | Docker | HTTPS 9443 | Manual; manages app stacks |
| Home Assistant | Docker, homeassistant | HTTP 8123 | Manual + screenshot; integrations not inventoried |
| Homarr | Docker, homarr | HTTP 7575 | Manual + screenshot; dashboard, collector requests, Docker socket |
| Pelican Panel | Docker, pelican-panel | HTTP 8085; /admin | Manual; SQLite and application key |
| Wings | Native wings.service | HTTP API 8080; SFTP TCP 2022 | Manual; Panel, Docker, /srv/gameservers |
| Host collector | Host Python | HTTP 8765/metrics | /opt/lab-host-metrics/server.py |
| Docker collector | Host Python | HTTP 8766/docker | /opt/lab-docker-metrics/server.py; Docker stats |
| Router/Tailscale collector | Host Python | HTTP 8767/router and /tailscale | /opt/lab-router-metrics/server.py; router SSH |
| Game collector | Host Python | HTTP 8768/games | /opt/lab-game-metrics/server.py; panel API and Docker |
| OpenWrt | Router ROUTER_IP | SSH used; exact listening port verify | WAN ROUTER_WAN_IP; upstream UPSTREAM_IP |
| Tailscale | OpenWrt subnet router | Advertises LAN_CIDR | Screenshot + manual; route approval/client acceptance/ACL |
| Minecraft / Homestead | Wings game container | TCP 25565 | Successful connection in manual; stopped in screenshot |
| Terraria | Panel inventory | Planned allocation 7777; verify protocol | Listed stopped in screenshot; installation not demonstrated |
| Satisfactory | Panel inventory | Planned allocation 7778; extra ports unknown | Listed stopped in screenshot; installation not demonstrated |
| Valheim | Egg imported per manual | Planned 2456–2458; verify protocol | Fourth screenshot entry is clipped; not identified from image |
| BruFin | Docker, brufin | Unknown | Running container and dashboard tile in screenshot; mounts/image/API unknown |
| Paperless-ngx | Docker, paperless | Unknown | Screenshot; two documents shown, processing Unknown |
| Paperless database | Docker, paperless-db | Unknown; internal/public binding unverified | Screenshot; engine, credentials and mounts unknown |
| Paperless Redis | Docker, paperless-redis | Unknown; internal/public binding unverified | Screenshot; exact role/configuration unverified |
| Windows / Tiny11 Pro | KVM/libvirt guest | Guest GUEST_IP:3389; host entry HOST_IP:3389 | Screenshot shows stopped, 4 vCPU, 8 GiB RAM, 80 GiB virtual disk |
| RDP forwarding | Host proposed NAT service | TCP + UDP 3389 | UDP remains unresolved; installed rules require inspection |
| Windows dashboard controls | Unknown backend | Unknown | Start button visible; no backend route, auth or implementation known |
| Paperless dashboard integration | Unknown collector/direct API | Unknown | Widget visible; do not assume it uses an existing collector |
| Weather widget | Unknown provider | Unknown | Screenshot only; provider/API key not established |

Do not expose collectors, Docker socket, Panel/Wings management or document-management endpoints publicly. No credentials are embedded. See [10 - Security and Credentials](Security.md).
