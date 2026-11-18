# Service interaction diagram

Solid arrows show relationships recorded in the supplied manual. Dotted arrows indicate an inferred dependency or unknown implementation. None are a live audit. Group containment means deployment location; it does not mean every client can reach every port. Ports without a protocol qualification are recorded service ports, not a verified transport inventory.

```mermaid
flowchart TB
  LAN["LAN clients"]
  Remote["Approved remote clients"]
  TS["Tailscale subnet router
LAN_CIDR"]
  Upstream["Upstream router
UPSTREAM_IP"]
  Router["OpenWrt
LAN ROUTER_IP / WAN ROUTER_WAN_IP"]
  Remote --> TS
  TS --> Router
  LAN --> Router
  Upstream --- Router
  subgraph Host["lab-host · HOST_IP"]
    SSH["SSH :22 verify"]
    Cockpit["Cockpit HTTPS :9090
45Drives plugin"]
    Samba["Samba :445"]
    Engine["Docker engine / local socket"]
    subgraph Apps["Docker application workloads"]
      Portainer["Portainer HTTPS :9443"]
      HA["Home Assistant HTTP :8123"]
      Homarr["Homarr HTTP :7575"]
      Panel["Pelican Panel HTTP :8085
SQLite + app key"]
      BruFin["BruFin
port/config unknown"]
      Paper["Paperless-ngx
port/config unknown"]
      DB["paperless-db
engine/port unknown"]
      Redis["paperless-redis
port unknown"]
    end
    subgraph Metrics["Host Python collectors · HTTP"]
      HM["Host :8765/metrics"]
      DM["Docker :8766/docker"]
      RM["Router :8767/router
and /tailscale"]
      GM["Games :8768/games"]
    end
    Wings["Native Wings
API :8080 / SFTP :2022"]
    subgraph Games["Wings-owned game inventory"]
      MC["Homestead / Minecraft
TCP :25565"]
      Terra["Terraria
planned :7777"]
      Sat["Satisfactory
planned :7778 + verify"]
      Val["Valheim egg
planned :2456-2458"]
    end
    OS["OS SSD /
Docker layers"]
    Data["Data SSD /srv
panel + games"]
    External["External SSD + HDD
Samba mounts"]
    NAT["RDP host entry :3389
TCP/UDP proposal; UDP unresolved"]
    VM["Windows KVM guest
GUEST_IP:3389
4 vCPU / 8 GiB / 80 GiB"]
    Control["Windows control backend
unknown"]
    PWidget["Paperless widget data source
unknown"]
    Weather["Weather provider
unknown"]
  end
  Router -->|"LAN / approved subnet access"| Host
  Portainer -->|"manages app stacks"| Engine
  Engine -->|"runs"| Apps
  Homarr -->|"socket integration"| Engine
  Homarr -->|"GET JSON"| Metrics
  HM -->|"OS stats / turbostat"| OS
  DM -->|"CLI / socket stats"| Engine
  RM -->|"SSH monitoring key"| Router
  GM -->|"read-only application API"| Panel
  GM -->|"UUID-matched stats"| Engine
  GM -->|"service-active check"| Wings
  Panel -->|"node management"| Wings
  Wings -->|"container lifecycle via Docker"| Engine
  Wings -->|"manages"| Games
  Panel -->|"persistent data"| Data
  Games -->|"worlds / volumes"| Data
  Cockpit -->|"share administration"| Samba
  Samba --> External
  NAT -->|"libvirt NAT / VM_BRIDGE"| VM
  Homarr -.->|"control implementation unverified"| Control
  Control -.-> VM
  Homarr -.-> PWidget
  PWidget -.-> Paper
  Paper -.->|"association inferred from container names"| DB
  Paper -.->|"association inferred from container names"| Redis
  Homarr -.-> Weather
  HA -.->|"integrations not inventoried"| LAN
```

## Read the main flows

- Administration: LAN/Tailscale → host → SSH, Cockpit or application UI; Portainer manages app stacks through Docker.
- Games: Panel → native Wings → Docker game containers → /srv. Game clients use allocations, not the Panel or Wings management ports.
- Dashboard: Homarr → collectors → host statistics, Docker, router SSH and panel API. A shortcut tile alone does not establish an API integration.
- Documents: Paperless and its named database/Redis companions appear in the screenshot. Their exact configuration and dashboard data path need local retrieval.
- Windows: host RDP entry → libvirt NAT → guest; the dashboard start control exists visually, but its backend is unknown.
- Storage: OS/Docker layers remain on root; app/game persistence uses /srv; Samba exposes existing external mounts.

See [20 - Services and Ports](Services-and-Ports.md) and [22 - Command Reference](Command-Reference.md).
