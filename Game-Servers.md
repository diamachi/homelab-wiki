# Game Servers

The supplied manual records Pelican Panel 1.0.0-rc.3 and native Wings 1.0.0-rc.2. The panel uses SQLite. Wings owns game-container lifecycle and depends on Docker and the mounted game data filesystem.

A Homestead 2.0.1 server pack ran using Fabric 1.20.1, loader 0.19.5, launcher 1.1.2 and a Java 21 container image. The pack was extracted to the server root, preserving bundled JVM arguments and skipping an egg installer that could overwrite it. A successful client connection and clean manual stop are recorded.

Start and stop through the panel. The recorded container restart policy was `no`; restoration of running games after host reboot was not tested. Only one game at a time was intended, but resource overallocation does not enforce this policy.

Terraria, Valheim and Satisfactory eggs were imported; servers were not yet installed. Whitelist and scheduled backups remained to configure. A light-load Spark snapshot is not a capacity benchmark. Verify memory limits, ports and startup behavior from deployed settings before tuning.

