---
description: Subflows, the actual flows that replace the harness subagent tool long term, are being designed or judged.
---

## Long term: actual flows replace the harness subagent tool

A flow's questions and requests are answered and fulfilled by actual flows, each under its own system prompt, and the answers return to it asynchronously, as messages.

## A subflow's reply is a datom of a type its role declares

A subflow's reply is a datom of a type its role declares, so the flow that briefed it reads a typed value and nothing else; a failing subflow returns one variant and no report, since text not asked for in a dearer context costs that reader more than nothing.

```ethos
Reply.[ Found.Vector<Line>     ; the role's own reply type: what the briefer asked for
        Nothing ]              ; the failing variant, carrying no report
Line.{ Path.String Text.String }
```

```datom
Found.[ { vision/subflows.md «A subflow's reply is a datom» } ]
Nothing
```
