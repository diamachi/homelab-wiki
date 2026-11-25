# Windows VM and RDP

A Windows guest behind libvirt NAT is documented. A previous systemd socket proxy provided TCP access; a replacement using kernel DNAT for TCP and UDP was proposed.

The suggested rule set has three parts per transport: destination NAT for inbound RDP, explicit forwarding permission before a libvirt reject rule, and permission for established return traffic. A oneshot system service was proposed to install/remove only the dedicated rules.

Installation and reboot persistence were not independently verified. The user reported the UDP counter remained zero. That alone does not locate the failure or establish that the client never attempted UDP.

Validate the guest listener, guest firewall, client transport negotiation and packet arrival at both physical and virtual interfaces. Keep a known working access method available while changing forwarding.

## Later chat reconciliation

See [25 November changes](Changes-2026-11-25.md), [router DNS](Router-DNS.md), [applications](Application-Updates.md) and [access/retired work](Access-and-Retired-Experiments.md). These supersede older inventory statements where explicitly identified. This update used chat evidence, not a live audit.
