# Troubleshooting

## Panel UI works but health check fails

The manual records an original health check targeting port 80 while the configured panel listener answered on another port. A corrected listener-aware HTTP/PHP-FPM check was proposed; deployment was not confirmed. Test the actual listener and preserve existing secrets during a stack update.

## Wings node offline

Check service state, Docker dependency, mounted data, scheme/port, panel reachability and node credentials. A previous failure involved copying a masked token ID. An unauthenticated 401 response can establish reachability, but cannot establish authenticated node health. Do not start a second debug daemon alongside the running service.

## RDP UDP remains at zero

The later user observation remains unresolved. Check guest listener/firewall, client negotiation, host packet arrival, destination, source restriction and forwarding rule order. Zero NAT counters alone do not identify the failing component.

## Dashboard stale or disks absent

Test the collector before editing the widget. Check its credentials and response shape privately. For disks, confirm mount, cable, power and kernel messages before permitting writes. Do not initialize existing disks or prune volumes as a first response to storage problems.

## Later chat reconciliation

See [25 November changes](Changes-2026-11-25.md), [router DNS](Router-DNS.md), [applications](Application-Updates.md) and [access/retired work](Access-and-Retired-Experiments.md). These supersede older inventory statements where explicitly identified. This update used chat evidence, not a live audit.
