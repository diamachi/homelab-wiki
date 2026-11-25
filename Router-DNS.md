# Router DNS and AdGuard Home

The router chat records OpenWrt 25.12.6 and installation of AdGuard Home package 0.107.80-r1 using apk. This supersedes the older snapshot's OpenWrt version; it does not establish when or how the router was upgraded.

## Recorded final configuration

- AdGuard serves LAN DNS on TCP/UDP 53. The setup-only AdGuard port 5353 is historical, not the final DNS endpoint.
- Administration uses HTTP at `http://ROUTER_IP:3000`.
- dnsmasq DNS moved to port 54, preserving DHCP, local `.lan` names and the existing Tailscale-name forwarding arrangement.
- Cloudflare DoH (`https://cloudflare-dns.com/dns-query`) is the upstream; no fallback resolver. Bootstrap resolvers were configured separately from fallback DNS.
- HaGeZi Multi NORMAL is the only enabled blocklist.
- Statistics/recent-query data are memory-only and reset on reboot; query history is not persistently written to router flash.
- LAN hard-coded port-53 requests are redirected. This record does not claim interception of application DoH or DoT.
- DHCP/RA advertise DNS for IPv4 and IPv6 clients; AdGuard autostart was enabled.

## Recorded verification and limits

The setup verified ordinary DNS, blocking including a request addressed to an external DNS resolver, local host lookup, local-link IPv6 DNS/blocking and HTTPS internet access. The Mac had no route to the router ULA and there was no public IPv6 LAN prefix; do not label general IPv6 internet connectivity as working.

Homarr initially needed an integration added manually; later dashboard work shows an AdGuard statistics/control card in the preview. Its credentials belong in Homarr's protected integration configuration, not this repository.

## Read-only checks

From a client, substitute the router address and your actual local hostname:

```sh
nslookup example.com ROUTER_IP
nslookup pagead2.googlesyndication.com ROUTER_IP
nslookup HOST_LOCAL_NAME ROUTER_IP
```

On OpenWrt:

```sh
/etc/init.d/adguardhome status
/etc/init.d/dnsmasq status
/etc/init.d/odhcpd status
/etc/init.d/adguardhome enabled
netstat -lnptu
```

Review listeners locally. Keep web/DNS management private. Do not copy a full live YAML or router backup into a public issue.
