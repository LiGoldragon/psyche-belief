---
description: A proof of concept or test is about to be deployed and the host must be chosen.
dependencies: []
---

## A proof of concept deploys on the flow's own host

A proof of concept is worked on and deployed on the host the flow is
running on. Another host is used only when the living names it.

## Testing happens on test nodes

Zeus is a stable node; testing happens on test nodes.

## Every build runs on Prometheus

Every build, test and compile runs through Nix on Prometheus, the remote builder; the laptop never runs the Rust compiler. Work that cannot go through Nix moves its files to Prometheus and runs there.

## Outside declarative deployment, call by store path

A thing tested outside declarative deployment is called by its full store path; the environment, PATH, links and session files, is changed only by a declared activation, never by hand.

## A working stack is maintained beside development

A working stack is maintained in parallel to development, always.
