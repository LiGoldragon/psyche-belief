---
description: The Flow Nexus, version 1, which launches a flow from a complex the user defined, is being designed or judged against what the living wants it to be.
dependencies: [vision-ethos]
---

# The Flow Nexus, version 1

## Vocabulary

A flow is one run of a model in a harness. A perma flow is a flow that continues through a succession of runs, one entity across them. A flow complex, said complex, is several flows defined together: each flow's model, harness, workspace and beliefs, and which flow speaks to which. A metaflow is every complex running on one host, with that host's keys and roles; a laptop runs one, a server may run several.

## The machine is defined, never built in

Everything that can be configured is configuration. The Nexus holds the vocabulary a definition is written in, as Ethos types; the user writes definitions in datom, the way Nix defines an operating system; a running flow is a definition in action. A complex is named by the user, and the Nexus runs it without knowing its name beforehand. A definition is one datom of its own: it is added, replaced or removed alone, and the metaflow is the set of them. No layer, role or anatomy is in the Rust.

## The vocabulary of a definition

```ethos
Library
[ herdr:[ Pane ]
  belief:[ ModuleName ] ]
[ ComplexName.String
  FlowName.String
  Harness.[ Claude Codex ]
  ModelName.String
  Effort.[ Low Medium High ]
  Workspace.[ Path.String             ; a directory that exists
              Temporary ]             ; made for this run
  Missing.[ Refuse                     ; what to do when
            Notice ]                   ;   a belief is absent
  Beliefs.{ Vector<ModuleName> Missing }
  Member.{ FlowName Harness ModelName
           Effort Workspace Beliefs }
  Complex.{ ComplexName Vector<Member> }
  FlowId.Integer
  Brief.String ]
[]
[]
```

## Signal

```ethos
Signal
[ flow:[ Complex ComplexName FlowName
         FlowId Brief ModuleName ] ]
[ Define.Complex                     ; add or replace one
  Launch.{ ComplexName FlowName Brief }
  Stop.FlowId ]
[ Defined.ComplexName
  Launched.FlowId
  Refused.[ UnknownComplex.ComplexName
            UnknownFlow.FlowName
            NoBelief.Vector<ModuleName>
            HerdrDown
            BeliefDown ]
  Stopped.FlowId ]
[]
```

## Emission

The Flow Nexus runs nothing itself. Its way out is two sockets: the Belief Nexus composes the flow's beliefs into its workspace, the herdr Nexus makes the pane and starts the harness in it. Its translator is the client of both.

```ethos
Emission
[ flow:[ Member Brief FlowId ]
  herdr:[ Pane Outcome ] ]
[ Furnish.{ Member FlowId }           ; beliefs into the workspace
  Open.{ Member FlowId Brief } ]      ; pane made, harness started
[ Furnished.Outcome
  Opened.{ Pane Outcome } ]
[]
```

## Memory

```ethos
Memory
[ flow:[ Complex FlowId ComplexName FlowName ]
  herdr:[ Pane ] ]
[ Definition.Complex
  Flow.{ FlowId ComplexName FlowName Pane
         State.[ Running Ended ] }
  Answer.[ Succeeded Failed ] ]
```

```datom
; the user defines a complex: one datom, added alone
Define.{ designer
         [ { fable Claude claude-fable-5-1 Medium
              Path.«/home/li/primary»
              { [ spirit:core vision:nexus-v1 ] Refuse } } ] }
Defined.designer
; and launches a flow of it
Launch.{ designer fable «Read the version one book» }
Launched.7
```
