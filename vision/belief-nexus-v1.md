---
description: The Belief Nexus, version 1, which holds the belief modules and furnishes workspaces with them in place of Curriculum, is being designed or judged against what the living wants it to be.
dependencies: [vision-ethos]
---

# The Belief Nexus, version 1

The Belief Nexus holds the belief modules and furnishes workspaces with them. Belief is the word: what a model believes when it starts. It replaces Curriculum. Its memory is its own; a definition in the Flow Nexus refers to a module by name only, and a name may resolve to nothing: the Belief Nexus answers which names are missing, and what is done about it is the definition's policy, never the Nexus's.

## Signal
The owner registers a belief repository at the Belief Nexus's own CLI, by his login, as he defines a complex at the Flow Nexus. A peer the meta peer list names furnishes over any registered repository.

A registered repository is watched: when its main moves, every workspace furnished with a module it changed is furnished again, and the Flow Nexus is told which flows now run on old belief, so a perma flow can be refreshed on it. A module is named by kind and subject; its front matter names its placement, system prompt or skill. The skills directory is the harness's.

```ethos
Signal
[ belief:[ Repository ModuleName      ; imports
           Workspace Location ]
  flow:[ Harness ] ]
[ Register.Repository                ; inputs: a module source
  Resolve.Vector<ModuleName>
  Furnish.{ Workspace Harness        ; the harness's
            Vector<ModuleName> }     ;   skills directory
  Subscribe ]
[ Registered.Repository              ; outputs
  Resolved.{ Vector<ModuleName>      ; found
             Vector<ModuleName> }    ; missing
  Furnished.{ Location
              Vector<ModuleName> }   ; missing, left out
  Subscribed
  Changed.{ Repository                ; pushed: main moved
            Vector<ModuleName>        ;   modules changed
            Vector<Workspace> }       ;   workspaces refurnished
  Refused.[ UnknownRepository.Repository
            Unwritable.Workspace ] ]
[]
```

```datom
Register.
  /git/github.com/LiGoldragon/psyche-belief
Registered.
  /git/github.com/LiGoldragon/psyche-belief
```

```sh
belief-nexus main '
  Register.
    /git/github.com/LiGoldragon/psyche-belief'
```

## Meta

A module's front matter names its placement; the default per Kind is a meta setting, set one value at a time, never in the Rust. The meta peer list names the peers admitted to Furnish, each bound by kernel credentials as a Nexus's peers are.

```ethos
Signal
[ belief:[ Kind Placement ] ]        ; imports
[ Configure.Set ]                    ; inputs: one value at a time
[ Configured.Set ]                   ; outputs: the value set
[ Set.[ Placement.{ Kind             ; types: the default
                    Placement }      ;   placement per Kind
        Peer.PeerBinding             ;   a peer admitted to Furnish
        RemovePeer.PeerId ]          ;   a peer removed
  UserId.Integer                     ; a login
  ProcessId.Integer
  PeerId.String                      ; a peer's name
  PeerIdentity.{ UserId ProcessId }  ; checked by kernel credentials
  PeerBinding.{ PeerId PeerIdentity } ]
```

## Library

```ethos
Library
[]
[ Repository.String                  ; a path holding
                                     ;   <type>/<subject>.md
  Kind.[ Spirit Intent Vision
         Knowledge Role ]
  ModuleName.{ Kind Subject.String }
  Workspace.String                   ; the flow's directory
  Placement.[ SystemPrompt Skill ]   ; named in front matter;
                                     ;   default per Kind: meta
  Location.{ SystemPrompt.String     ; the bundle file written
             Skills.String } ]       ; the skills directory
[]
[]
```

## Emission

Furnishing is writing: each module into the workspace's system-prompt bundle or the harness's skills directory, as its placement says.

```ethos
Emission
[ belief:[ Workspace ModuleName Location ] ]
[ Write.{ Workspace Vector<ModuleName> } ]
[ Written.Location ]
[]
```

## Memory

```ethos
Memory
[ belief:[ Repository ModuleName ] ]
[ Source.{ Repository Vector<ModuleName> }
  Answer.[ Succeeded Failed ] ]
```

```datom
Furnish.{ /home/li/primary Claude
          [ { Spirit core } { Vision nexus-v1 }
            { Vision none } ] }
Furnished.{ { /home/li/primary/.bundle
              /home/li/primary/.claude/skills }
            [ { Vision none } ] }
```
