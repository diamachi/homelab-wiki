# Containers and Applications

The supplied manual records Docker Engine 29.1.0, with Portainer, Home Assistant, Homarr and Pelican Panel containers. Recorded image tags include LTS, stable and latest; these are mutable historical references rather than reproducible restore versions.

Portainer manages application stacks. Native Wings manages game containers; do not manually recreate those containers through Portainer. Preserve deployed stack definitions, volumes and secret environment values before any recreation.

Homarr has Docker socket integration, which grants powerful host access. Keep it private. The application data filesystem is separate from Docker's image-layer storage. Existing volumes were not migrated in the documented setup.

