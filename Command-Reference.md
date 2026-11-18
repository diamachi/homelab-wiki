# Command reference

These commands are templates, not actions already performed. Replace uppercase placeholders with your own values before running. Service names and paths beginning with lab- are illustrative replacements, not installed configuration. Run host checks on lab-host; run router commands on OpenWrt and Windows commands inside the guest. Review outputs locally because logs, mounts and unit definitions can expose private details. Placeholders in angle brackets require actual discovered names.

## Connect and host health

```bash
ssh ADMIN_USER@HOST_IP
hostnamectl
cat /etc/os-release
lscpu
free -h
uptime
sudo systemctl --failed
sudo journalctl -p err -b --no-pager
```

## Storage and shares

```bash
lsblk -o NAME,SIZE,FSTYPE,LABEL,UUID,MOUNTPOINTS
findmnt /srv
findmnt /mnt/shared-ssd
findmnt /mnt/shared-hdd
df -hT
sudo findmnt --verify
sudo testparm -s
sudo pdbedit -L
systemctl status smbd --no-pager
```

Confirm /srv and external mounts before starting data writers. Existing external drives must retain their data; do not format them or recursively change ownership as a troubleshooting shortcut.

## Docker, services and actual ports

```bash
sudo docker ps -a --format 'table {{.Names}}	{{.Image}}	{{.Status}}	{{.Ports}}'
sudo docker compose ls
sudo docker stats --no-stream
sudo docker system df
sudo docker info --format '{{.DockerRootDir}}'
sudo ss -lntup
systemctl list-unit-files --state=enabled
systemctl list-units --type=service --all
```

For Paperless or BruFin, discover mounts and Compose locations without dumping environment values:

```bash
sudo docker inspect --format '{{json .Mounts}}' paperless
sudo docker inspect --format '{{json .Mounts}}' brufin
sudo docker inspect --format '{{ index .Config.Labels "com.docker.compose.project.working_dir" }}' paperless
sudo docker inspect --format '{{ index .Config.Labels "com.docker.compose.project.config_files" }}' paperless
```

Container names are screenshot records; verify they still exist. Never use a blanket environment dump to retrieve credentials.

## Collector responses

```bash
curl -fsS --max-time 15 http://HOST_IP:8765/metrics
curl -fsS --max-time 15 http://HOST_IP:8766/docker
curl -fsS --max-time 15 http://HOST_IP:8767/router
curl -fsS --max-time 15 http://HOST_IP:8767/tailscale
curl -fsS --max-time 15 http://HOST_IP:8768/games
systemctl status lab-host-metrics lab-game-metrics --no-pager
sudo journalctl -u lab-game-metrics -n 50 --no-pager
```

Docker/router collector unit names and Paperless/Windows widget backends remain unconfirmed. Do not guess extra endpoints.

## Panel and Wings

```bash
sudo systemctl status wings --no-pager
sudo journalctl -u wings -n 80 --no-pager
sudo docker logs --tail 100 pelican-panel
sudo docker inspect pelican-panel --format '{{json .State.Health}}'
curl -i --connect-timeout 5 http://HOST_IP:8080/api/system
```

401 without credentials demonstrates an HTTP response, not authenticated node health. Stop/start games through Pelican. In its game console, use `spark tps` and `spark healthreport` for the recorded Minecraft pack. Do not manually wrap its lifecycle with a second restart manager.

## VM and RDP

```bash
sudo virsh list --all
sudo virsh net-list --all
sudo virsh dominfo '<VM_NAME>'
systemctl status lab-rdp-nat.service lab-rdp.socket lab-rdp.service --no-pager
sudo iptables -t nat -vnL PREROUTING
sudo iptables -vnL FORWARD
sudo tcpdump -ni LAN_INTERFACE -c 40 'udp port 3389'
```

Captures can be stopped with Ctrl-C. `Windows guest` is a display name, not a verified libvirt domain name. In guest PowerShell:

```powershell
Get-NetUDPEndpoint -LocalPort 3389
Get-NetFirewallRule -Name 'RemoteDesktop-UserMode-In-UDP' | Select-Object Name,Enabled,Direction,Action
```

## OpenWrt checks — run on the router

```sh
ubus call system info
ubus call network.interface.wan status
tailscale status
ip route
```

## Deliberate service changes

Only after checking dependencies and arranging a maintenance window, the recorded native services can be restarted individually:

```bash
sudo systemctl restart wings
sudo systemctl restart lab-game-metrics
```

Restarting Wings can affect game management. Starting/stopping Windows requires the actual domain name and a deliberate choice; the screenshot's button implementation is unknown. Backup and rebuild procedures are in [18 - Recovery and Capture](Backup-and-Recovery.md); credential retrieval is in [10 - Security and Credentials](Security.md).
