---
description: "Nix builds are made, kept or collected."
dependencies: []
---

## Nix builds

Nix builds live in the remote builder's store. A machine keeps links only to the profiles in use on it. A Nix build worth keeping is listed in one registry profile; every other Nix build is collected by how recently and how often it was used.

A flake input is the bare repository URL; the lock is the pin. A rev or a ref is written in the lock alone.

```nix
inputs.flow.url = "github:LiGoldragon/flow";   # the repository, bare; flake.lock holds the commit
```
