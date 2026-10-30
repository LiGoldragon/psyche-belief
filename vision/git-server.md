---
description: "The cluster's own Git server is set up or changed."
dependencies: []
---

## Git Server

The cluster runs its own Git server on the node whose cluster data gives it the GitServer role. It serves thinking machines: it accepts the SSH keys the cluster data holds, carries no web interface, and mirrors every repository to GitHub as a backup.
