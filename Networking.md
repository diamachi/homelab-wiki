# Networking

The documented topology has an upstream router, an OpenWrt LAN router, a Linux host and a libvirt NAT guest network. OpenWrt advertises the home subnet through Tailscale. Trusted remote clients require an approved subnet route, accepted client routes and appropriate access rules; management services are not intended for public forwarding.

The supplied records include SSH, Samba, Cockpit, Portainer, Home Assistant, Homarr, Pelican, Wings, game services and private collectors. Real addresses and endpoint inventory are kept in the private vault. Verify actual listener bindings and router firewall behavior rather than assuming a dashboard entry proves exposure.

Later user output shows IPv4 forwarding enabled and Docker/libvirt chains present while UFW was inactive. That does not imply an absence of kernel firewall rules. Docker-published ports also require exposure review. Do not blindly enable a firewall or flush forwarding rules over a remote management session.

## Later chat reconciliation

See [25 November changes](Changes-2026-11-25.md), [router DNS](Router-DNS.md), [applications](Application-Updates.md) and [access/retired work](Access-and-Retired-Experiments.md). These supersede older inventory statements where explicitly identified. This update used chat evidence, not a live audit.
