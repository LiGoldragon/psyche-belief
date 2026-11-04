---
description: The metaflow, version 1, everything running on one host for one owner: three Nexuses, their definitions, and how several run side by side, is being designed or judged against what the living wants it to be.
dependencies: [vision-flow-nexus-v1, vision-herdr-nexus-v1, vision-belief-nexus-v1]
---

# The metaflow

Version 1. A metaflow is everything running on one host for one owner: three Nexuses, the definitions they run, and the flows running from them. A host may run several, each under its own name and directories.

```mermaid
flowchart TB
    d["definitions: one datom file per complex"] -- "Define, through the CLI" --> f["Flow Nexus"]
    f -- "Furnish, signal" --> b["Belief Nexus"]
    f -- "Create, Start, Prompt, signal" --> h["herdr Nexus"]
    b -- "writes the bundle and the skills" --> w["workspace"]
    h -- "runs herdr" --> p["pane: the harness, the flow"]
    p -- "Report, through the CLI, from a hook" --> f
    l["the living, at a CLI"] -- "Say" --> f
```

## A metaflow is a directory

A metaflow has a name and two directories, and a Nexus reads nothing from the environment; the CLI's two default roots come from the standard XDG variables and from nothing else. Runtime holds the sockets of its Nexuses and defaults to `$XDG_RUNTIME_DIR/metaflow/<name>/`; State holds their memories and defaults to `~/.local/state/metaflow/<name>/`. A Nexus is started with one datom, its place. The registry is the runtime root, `$XDG_RUNTIME_DIR/metaflow/`, one directory per name; a CLI resolves `<metaflow>` there and finds the sockets. Two metaflows are two names, and the stable one keeps running while the next is tried. The CLI is `<nexus-name> <metaflow> '<datom>'`: named after the Nexus; the metaflow name picks the instance. Both roots are the CLI's fixed defaults, never an argument.

```ethos
Library
[]
[ MetaflowName.String                ; main, next
  Place.{ MetaflowName               ; what every Nexus starts with
          Runtime.String             ; the sockets
          State.String } ]           ; the memories
[]
[]
```

```datom
; each Nexus, started by the metaflow's shell
{ main /run/user/1001/metaflow/main
  /home/li/.local/state/metaflow/main }
; the sockets it makes there
; <nexus>.sock  <nexus>-meta.sock  <nexus>-translator.sock  <nexus>-meta-translator.sock
; the meta CLI's text arrives at <nexus>-meta-translator.sock and becomes signal for <nexus>-meta.sock; the ordinary translator refuses meta text
; flow.sock  flow-meta.sock  flow-translator.sock  flow-meta-translator.sock
; herdr.sock herdr-meta.sock herdr-translator.sock herdr-meta-translator.sock
; belief.sock belief-meta.sock belief-translator.sock belief-meta-translator.sock
```

```sh
# the CLI: the metaflow's name, then one datom
flow-nexus main 'Launch.{ designer fable «Read the book» }'
herdr-nexus main 'Prompt.{ { main wQ:pT } «hello» }'
```

## The metaflow is a Nix shell

The repository metaflow holds the Nix that builds the three Nexuses, their translators and CLIs, and a shell that starts them in a named directory under the owner's login. It is not a sandbox: a flow in it has the owner's credentials and files. A second shell with a second name is a second metaflow.

```sh
nix develop github:LiGoldragon/metaflow -- metaflow start next
```

## Everything in a metaflow is a definition

The Nexuses hold vocabulary; the owner writes definitions in datom. A definition is one file, one datom; the definition files are the owner's sources, kept wherever he keeps them and given by Define and replaced the same way; the running set is the Flow Nexus's Memory in the State directory. A change to one definition touches no other. The Rust knows no layer, role, model name or topic.

```datom
; definitions/designer.datom: one complex
{ designer
  [ { fable Claude claude-fable-5-1 Medium
      Permanent
      Path.«/home/li/primary»
      { [ { Spirit core } { Vision nexus-v1 } ] Refuse }
      { [ Bash Edit ] [ Artifact ] }
      [ Speaks.opus Speaks.Living ] }
    { opus Claude claude-opus-4 Medium Ephemeral
      Temporary
      { [ { Spirit core } { Role worker } ] Notice }
      { [] [] }
      [ Speaks.fable Speaks.Complex.implementer ] } ]
  fable }                            ; the speaker
```
