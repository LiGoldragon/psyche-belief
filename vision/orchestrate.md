---
description: Orchestrate itself — its deployment, its meta binary, or the scope of its skill — is being designed or judged.
dependencies: []
---

## Deployment

Orchestrate is deployed unconditionally, in the home, for every
user. A deployment of orchestrate includes meta-orchestrate.

## The skill

The orchestrate skill covers ordinary operations only; meta
operations are outside it.

## A shared path is locked before it is edited

A flow reserves its whole write set with a Lock before editing a shared path and releases it when editing ends; a flow's own directory is written freely, because only that flow writes there. A lock whose holder is live is messaged; a lock whose holder has no live flow and no live pane may be released by any flow, with the holder and its paths recorded.
