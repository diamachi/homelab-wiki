# Hardware and Storage

The supplied operations snapshot records an Intel Core i5-9500T (6 cores/6 threads), 32 GB DDR4, a 128 GB OS SSD and a 256 GB ext4 data SSD. External exFAT SSD/HDD storage is shared over Samba. Ubuntu Server is recorded as the host OS; the precise installed release needs local verification.

Docker image layers remain on the OS drive. Application and game persistence use a separate mounted data filesystem. Check that data mounts exist before starting writers, so an absent mount does not redirect writes onto the root disk.

External disks contain existing data. Identify them before mount or recovery work. exFAT mount options control much of its permissions behavior; archives are needed to preserve Unix metadata in backups stored there. UUIDs, labels and actual mount paths are omitted.

## Later chat reconciliation

See [25 November changes](Changes-2026-11-25.md), [router DNS](Router-DNS.md), [applications](Application-Updates.md) and [access/retired work](Access-and-Retired-Experiments.md). These supersede older inventory statements where explicitly identified. This update used chat evidence, not a live audit.

The cooling discussion identifies an HP EliteDesk 800 G5 Mini in assistant messages; the exact model should still be checked locally. The user confirms vertical placement with a perforated panel facing the room. External fan installation was discussed only; Docker polling was a hypothesis without a returned controlled-test result.
