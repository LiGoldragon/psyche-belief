---
description: What truly blocks a task.
dependencies: []
---

A task blocks another only when the other needs its output; everything that does not need it goes on at once, in parallel flows.

```mermaid
flowchart TB
    a["a task"] -- "needs the output of another? yes: waits for" --> b["its output"]
    a -- "needs the output of another? no: starts now in" --> c["a parallel flow"]
```

Each task runs on its own need.

A flow blocks only on the output its task needs.
