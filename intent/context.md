---
description: A value, fact or field is placed at a layer, or a layer is found carrying another layer's fact.
dependencies: []
---

## Every layer carries its own context

A value at any layer carries the context it makes sense in, and each
layer carries only its own facts.

```mermaid
flowchart TB
    v["a value a system of ours takes"] --> c["typed configuration"]
    v --> d["a field of the datom it is given"]
    t["a third-party program"] -- "is given" --> e["a variable, itself configuration"]
```
