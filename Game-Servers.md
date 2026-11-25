# Game Servers

The supplied manual records Pelican Panel 1.0.0-rc.3 and native Wings 1.0.0-rc.2. The panel uses SQLite. Wings owns game-container lifecycle and depends on Docker and the mounted game data filesystem.

A Homestead 2.0.1 server pack ran using Fabric 1.20.1, loader 0.19.5, launcher 1.1.2 and a Java 21 container image. The pack was extracted to the server root, preserving bundled JVM arguments and skipping an egg installer that could overwrite it. A successful client connection and clean manual stop are recorded.

Start and stop through the panel. The recorded container restart policy was `no`; restoration of running games after host reboot was not tested. Only one game at a time was intended, but resource overallocation does not enforce this policy.

At the earlier manual snapshot, these additional game eggs were imported but not installed. Later records establish Satisfactory was installed and the user and a friend joined it. Terraria and Valheim successful play remains unverified. Whitelist and scheduled backups remained to configure. A light-load Spark snapshot is not a capacity benchmark. Verify memory limits, ports and startup behavior from deployed settings before tuning.



## Satisfactory version checks

A later assistant interpreted attached manifests as client Steam app 526870/build 26728002 and dedicated-server app 1690800/build 26728027. The image contents were not independently re-inspected for this update. These are separate Steam apps; build-ID equality is not the compatibility criterion. No reinstall or completed update is confirmed. Use the game's compatibility message/startup changelist and back up saves before any update. For this deployment, manage lifecycle through Pelican rather than recreating a Wings-owned game in Portainer.

The user reported a new-looking session, starting items and no onboarding tasks. The onboarding explanation and local-world-transfer workflow were advice, not a confirmed transfer or a reason to delete saves.
