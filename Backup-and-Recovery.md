# Backup and Recovery

The supplied manual describes a recommended backup policy, not a configured or restore-tested backup system. Preserve host mount/network configuration, Samba accounts, application stacks and data, dashboard keys and exports, panel application key and SQLite database, Wings node configuration, game worlds and collector scripts/credentials.

Stop games gracefully before offline copies. Stop the panel before copying its live SQLite files or use a supported consistent backup method. Database-backed workloads and VM disks need consistent backup procedures. External exFAT targets require archives to preserve ownership, modes and symlinks.

Rebuild in dependency order: OS/network, verified mounts and Samba, Docker and application data, dashboards, collectors, panel and Wings, then games. Restore panel inventory and game directories together to preserve UUID mapping. Test one game and restore target at a time; never restore over the only working copy. Keep encrypted off-host copies and separate recovery keys.

## Later chat reconciliation

See [25 November changes](Changes-2026-11-25.md), [router DNS](Router-DNS.md), [applications](Application-Updates.md) and [access/retired work](Access-and-Retired-Experiments.md). These supersede older inventory statements where explicitly identified. This update used chat evidence, not a live audit.

The encrypted backup set created for the later audio experiment was explicitly deleted during its cleanup. Do not assume it remains available. Router pre-change backups were a separate set. No full-system disk image or tested end-to-end restore is established.
