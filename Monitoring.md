# Monitoring

Homarr reads four lightweight host-side Python HTTP collectors: host metrics, Docker metrics, router/Tailscale metrics and Pelican game metrics. These are separate from container workloads. Collector URLs and local script paths are retained only in the private vault.

Host metrics use turbostat and system files; reported system watts are estimates, not wall-meter measurements. Storage discovery may omit a disconnected drive rather than render it offline. Docker CPU percentages can exceed 100% across cores.

The router collector uses an SSH monitoring key. The game collector uses a read-only application API, paginated server inventory and container UUID matching, with a cached response refreshed every ten seconds. Its service-active signal for Wings does not prove authenticated connectivity. Player counts were not implemented; missing metrics do not prove a server was deleted.

The documented HTTP collectors have no authentication and should remain on trusted networks with access restrictions. Credentials belong in protected host files, outside widget configuration. Preserve actual board exports, widget source, collector scripts and units; screenshots are not restore artifacts.

