# Windows VM and RDP

A Windows guest behind libvirt NAT is documented. A previous systemd socket proxy provided TCP access; a replacement using kernel DNAT for TCP and UDP was proposed.

The suggested rule set has three parts per transport: destination NAT for inbound RDP, explicit forwarding permission before a libvirt reject rule, and permission for established return traffic. A oneshot system service was proposed to install/remove only the dedicated rules.

Installation and reboot persistence were not independently verified. The user reported the UDP counter remained zero. That alone does not locate the failure or establish that the client never attempted UDP.

Validate the guest listener, guest firewall, client transport negotiation and packet arrival at both physical and virtual interfaces. Keep a known working access method available while changing forwarding.
