# Application details from later chats

The 22 November Docker capture establishes these image references and published mappings. Tags can be mutable and this is not today's live inventory.

| Application | Captured image | Host → container | Recorded state |
|---|---|---|---|
| BruFin | diamachi/brufin:v0.6.3 | TCP 8780 → 8080 | Healthy; host binding was all IPv4 interfaces |
| Motrix | motrixapp/motrix-server:2.4.3 | TCP HOST_IP:9999 → 8080 | Healthy; captured as LAN-address-bound |
| Paperless-ngx | ghcr.io/paperless-ngx/paperless-ngx:latest | TCP HOST_IP:8301 → 8000 | Healthy; captured as LAN-address-bound |
| Paperless database | postgres:18 | Container TCP 5432; no host publication shown | Healthy |
| Paperless queue/cache companion | valkey/valkey:9-alpine | Container TCP 6379; no host publication shown | Container up |
| Pelican Panel | ghcr.io/pelican/panel:latest | TCP 8085 → 8085 | Healthy in capture |

A container-exposed port without a host mapping is not evidence of a published host port. The exact Paperless connection configuration is still not exported; database/queue relationships follow the stack's named companions and require configuration confirmation.

## BruFin

Server port is 8780; do not confuse it with Wings API port 8080. Preserve the existing data volume during upgrades. Release/image publication alone is not proof of deployment, but the later captured image specifically shows v0.6.3 on the server. A stopped Mac preview does not mean the homelab service stopped.

## Motrix

aria2 performs most download work. A recorded sample of about 52% Docker CPU represents roughly 9% of six cores, not 52% of the entire machine. The trace showed split=16 and max-connection-per-server=64 during a large download. These are recorded workload settings, not recommended defaults or proof of a fault.

The external SSD mount was repaired during the audio project's backup/recovery work. Audio cleanup deliberately retained this repair. Recheck mount presence before starting writes; do not undo it while removing unrelated audio packages. aria2 RPC authentication exists; keep its secret private. Ports seen only inside the container are not automatically public listeners.

## Homarr and monitoring

Homarr and Portainer had direct Docker socket mounts in user-pasted inspection output. Other running containers in that inspection did not show a direct socket mount. Docker socket access is powerful; do not infer that either application caused daemon load without a controlled test.

The redesign used a separate preview board. Its latest verified layout combines greeting, uptime, weather and overview, integrates all four drives into that overview, adds readable container names/sample times and themes the AdGuard card. Desktop and phone were checked. The original board remained unchanged. A speed-test service was active in a captured service check, but its endpoint, schedule and implementation are not supplied here.
