# Hardware and Storage

The supplied operations snapshot records an Intel Core i5-9500T (6 cores/6 threads), 32 GB DDR4, a 128 GB OS SSD and a 256 GB ext4 data SSD. External exFAT SSD/HDD storage is shared over Samba. Ubuntu Server is recorded as the host OS; the precise installed release needs local verification.

Docker image layers remain on the OS drive. Application and game persistence use a separate mounted data filesystem. Check that data mounts exist before starting writers, so an absent mount does not redirect writes onto the root disk.

External disks contain existing data. Identify them before mount or recovery work. exFAT mount options control much of its permissions behavior; archives are needed to preserve Unix metadata in backups stored there. UUIDs, labels and actual mount paths are omitted.

