# Remote access and abandoned experiments

## Friends: games only is the latest requested policy

The user supplied a Tailscale policy with an unrestricted owner group and a game-only friends group. The game grants identify:

| Game | Ports in the policy |
|---|---|
| Minecraft | TCP 25565 |
| Terraria | TCP 7777 |
| Valheim | UDP 2456–2458 |
| Satisfactory | TCP/UDP 7778 and TCP 8888 |

These are recorded grants, not proof every allocation is listening or every game is installed. The friend successfully joined Satisfactory according to the user. Network grants do not manage saves or game lifecycle.

A later shared-folder experiment temporarily included TCP 445. The user then requested removal of that experiment and the assistant produced a game-only policy again. No final saved-policy result is available. Treat friend SMB access as **intended removed, application unverified**; do not claim it is definitely blocked today.

The Samba share-removal command produced NT_STATUS_NOT_FOUND for its security entry. That is not a complete cleanup verification. Recheck effective shares and user accounts, then the saved Tailscale policy, without deleting folders or other personal shares. Owner access must remain separate from friends. The group's membership emails and exact private share names are omitted from the public documentation.

## Network audio: retired, not an active architecture component

Music Assistant 2.10.13 and a YouTube PO Token helper 2.0.2 were temporarily deployed. Library import and browser streaming were confirmed; a separate Bose A2DP playback test also passed. This did not establish a finished Music Assistant-to-Bose bridge or universal AirPlay receiver.

The user later abandoned the network-audio plan. A user-run cleanup log confirmed both project containers absent, their images removed, project data and the experiment backup directory deleted, the server's Bose pairing removed, headless audio override removed and linger restored to no. Pre-existing packages/services and the unrelated download-storage repair were retained.

Music Assistant's historical 8095 endpoint and the helper's loopback 4416 endpoint are retired records, not current service URLs. No replacement USB lo-fi player, AirPlay receiver or Home Assistant audio bridge was deployed. An EPOS USB speaker/YouTube-live player was discussed only.

## Other proposals

Pulse, PostgreSQL for Pulse, a Tailscale Serve/socat path, DuckDNS and Caddy were discussed. No installation or working OAuth/certificate deployment is evidenced. Keep them out of the active service inventory. Do not confuse this proposed PostgreSQL with the captured Paperless database.
