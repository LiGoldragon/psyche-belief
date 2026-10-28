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

How badly the living wants one thing never stops another.

A flow does not block on an unrelated issue.
