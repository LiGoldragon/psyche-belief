---
description: CriomOS, its hosts, fixes, hardware, services, Nix code or desktop, is being designed or judged.
dependencies: [vision-nix-builds]
---

## CriomOS

CriomOS is a declarative operating system: every host is built from its declaration.

A problem in CriomOS is fixed in CriomOS by a proper fix and a proper deploy.
Every hotfix in place is removed and replaced by that fix.

CriomOS is made more modular; an anatomy of it shows what should be taken out.

## Nix code

Every store path in Nix code is the output of evaluating a package, a flake input or an option.

## Hardware

CriomOS has a hardware type, so that it supports several kinds of hardware, the Librem 5 Linux smartphone among them; a module may be gated on it.
A fix that only some hardware needs is a value in the cluster data, marked by the chip or part that makes it necessary.
A library reads the cluster's list of its hardware and answers, by processor, model and variant, which fixes a computer needs.

## Harnesses

The harnesses and their desktop apps are kept stock in at least one version, under their ordinary executable names.

## Services

A new service lives in CriomOS.
A service is updated by bringing it up at its latest version.

## Desktop

A new artifact does not open a browser tab on its own.
