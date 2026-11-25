# Services and ports

All host endpoints below use the placeholder `HOST_IP`. Updated from later chat evidence on 25 November 2026; these remain historical records, not a fresh port scan. “Screenshot” means displayed by the supplied dashboard, not independently validated service health. Unknown ports are deliberately not guessed.

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
| Terraria | Panel inventory | Policy TCP 7777 | Installation/play verification remains missing |
| Satisfactory | Pelican/Wings game | Policy: TCP/UDP 7778; TCP 8888 | User and friend joined; current runtime/allocations not audited |
| Valheim | Stopped container/egg in records | Policy UDP 2456–2458 | No successful play test established |
| BruFin | Docker, brufin; diamachi/brufin:v0.6.3 | TCP 8780 → 8080 | 22 November captured Docker output; persistent data preserved on upgrades |
| Paperless-ngx | Docker; latest tag | TCP 8301 → 8000 | 22 November capture; LAN-address-bound; mounts not exported |
| Paperless database | Docker, postgres:18 | Container TCP 5432; no host mapping shown | Captured healthy; exact connection configuration private/unexported |
| Paperless queue/cache companion | Docker, valkey/valkey:9-alpine | Container TCP 6379; no host mapping shown | Name remains paperless-redis; captured up |
| Windows / Tiny11 Pro | KVM/libvirt guest | Guest GUEST_IP:3389; host entry HOST_IP:3389 | Screenshot shows stopped, 4 vCPU, 8 GiB RAM, 80 GiB virtual disk |
| RDP forwarding | Host proposed NAT service | TCP + UDP 3389 | UDP remains unresolved; installed rules require inspection |
| Windows dashboard controls | Unknown backend | Unknown | Start button visible; no backend route, auth or implementation known |
| Paperless dashboard integration | Unknown collector/direct API | Unknown | Widget visible; do not assume it uses an existing collector |
| Weather widget | Unknown provider | Unknown | Screenshot only; provider/API key not established |

Do not expose collectors, Docker socket, Panel/Wings management or document-management endpoints publicly. No credentials are embedded. See [10 - Security and Credentials](Security.md).

## Added services and historical endpoints

| Service | Endpoint | Status |
|---|---|---|
| Motrix | Host TCP 9999 → container 8080 | Captured healthy; LAN-address-bound |
| AdGuard Home | Router TCP/UDP 53; HTTP 3000 | Cutover verified in router chat |
| dnsmasq | Router DNS port 54; DHCP retained | Configured alongside AdGuard |
| Speed-test service | Endpoint/schedule unknown | Active in captured service check |
| Windows discovery wsdd2 | Check actual listeners | Restart proposed; later user said works, without separate service output |
| Music Assistant + token helper | Historical 8095 / loopback 4416 | Removed; do not deploy from old notes |

The friend-only SMB experiment was abandoned; saved-policy cleanup still needs confirmation. No Pulse or replacement audio player deployment is established.
