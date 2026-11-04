---
description: The Belief Nexus, version 1, which holds the belief modules and furnishes workspaces with them in place of Curriculum, is being designed or judged against what the living wants it to be.
dependencies: [vision-ethos]
---

# The Belief Nexus, version 1

The Belief Nexus holds the belief modules and furnishes workspaces with them. Belief is the word: what a model believes when it starts. It replaces Curriculum. Its memory is its own; a definition in the Flow Nexus refers to a module by name only, and a name may resolve to nothing: the Belief Nexus answers which names are missing, and what is done about it is the definition's policy, never the Nexus's.

## Signal
A registered repository is watched: when its main moves, every workspace furnished with a module it changed is furnished again, and the Flow Nexus is told which flows now run on old belief, so a perma flow can be refreshed on it. A module is named by kind and subject; its placement, system prompt or skill, is read from the module's own front matter.

```ethos
Signal
[ belief:[ Repository ModuleName
           Workspace Placement ] ]
[ Register.Repository
  Resolve.Vector<ModuleName>
  Furnish.{ Workspace Vector<ModuleName> }
  Subscribe ]
[ Registered.Repository
  Resolved.{ Vector<ModuleName>
             Vector<ModuleName> }
  Furnished.{ Placement Vector<ModuleName> }
  Subscribed
  Changed.{ Repository                ; pushed: main moved
            Vector<ModuleName>        ;   modules changed
            Vector<Workspace> }       ;   workspaces refurnished
  Refused.[ UnknownRepository.Repository
            Unwritable.Workspace ] ]
[]
```

```ethos
Signal
[ belief:[ Repository ModuleName
           Workspace Placement ] ]
[ Register.Repository                ; a module source
  Resolve.Vector<ModuleName>
  Furnish.{ Workspace Vector<ModuleName> } ]
[ Registered.Repository
  Resolved.{ Vector<ModuleName>       ; found
             Vector<ModuleName> }     ; missing
  Furnished.{ Placement
              Vector<ModuleName> }    ; missing, left out
  Refused.[ UnknownRepository.Repository
            Unwritable.Workspace ] ]
[]
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
  Placement.{ SystemPrompt.String    ; the bundle file written
              Skills.String } ]      ; the skills directory
[]
[]
```

## Emission

Furnishing is writing: the spirit and intent modules into one system-prompt bundle, every other module into the harness's skills directory of the workspace.

```ethos
Emission
[ belief:[ Workspace ModuleName Placement ] ]
[ Write.{ Workspace Vector<ModuleName> } ]
[ Written.Placement ]
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
Furnish.{ /home/li/primary
          [ { Spirit core } { Vision nexus-v1 }
            { Vision none } ] }
Furnished.{ { /home/li/primary/.bundle
              /home/li/primary/.claude/skills }
            [ { Vision none } ] }
```
