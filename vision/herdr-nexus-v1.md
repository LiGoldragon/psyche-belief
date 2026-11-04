---
description: The herdr Nexus, the one component that owns every pane and runs herdr, is being designed or built against what the living wants it to be.
dependencies: [vision-ethos]
---

# The herdr Nexus

The herdr Nexus owns every pane. It is the one component that runs herdr; when herdr changes, it changes, and nothing else does. It is built first, because it proves the translator and the CLI alone, and it is kept usable by hand: any flow, or the living, drives a pane through `herdr-nexus 'Prompt.{ … }'`.

## Signal
The herdr Nexus also observes: a pane's state is read from herdr and pushed to subscribers as it changes, so the Flow Nexus learns a harness has died without a hook. A pane carries a label, the address of the flow in it, so a listing reads as the metaflow does.

```ethos
Signal
[ herdr:[ Session PaneId Pane Workspace
          Command Text Keys Outcome Label ] ]
[ Create.Workspace
  Start.{ Pane Command Label }
  Prompt.{ Pane Text }
  Press.{ Pane Keys }
  Close.Pane
  List.Session
  Subscribe.Session ]
[ Created.Pane
  Started.Outcome
  Prompted.Outcome
  Pressed.Outcome
  Closed.Outcome
  Listed.Vector<Known>
  Subscribed
  Changed.{ Pane State } ]           ; pushed, each change
[ Label.String
  State.[ Open Busy Idle Dead ]
  Known.{ Pane Label State } ]
```

```ethos
Signal
[ herdr:[ Session PaneId Pane Workspace
          Command Text Keys Outcome ] ]
[ Create.Workspace                   ; inputs
  Start.{ Pane Command }
  Prompt.{ Pane Text }
  Press.{ Pane Keys }
  Close.Pane ]
[ Created.Pane                       ; outputs
  Started.Outcome
  Prompted.Outcome
  Pressed.Outcome
  Closed.Outcome ]
[]
```

## Library

```ethos
Library
[]
[ Session.String                     ; the herdr session
  PaneId.String                      ; herdr's name for a pane
  Pane.{ Session PaneId }
  Root.String                        ; a directory
  Variable.{ Name.String Value.String }
  Workspace.{ Session Root
              Vector<Variable> }
  Command.{ Program.String
            Vector<String> }         ; what starts in the pane
  Text.String                        ; what is typed
  Keys.Vector<String>
  Outcome.[ Done
            Uncertain
            Refused.{ Code.Integer
                      Message.String } ] ]
[]
[]
```

## Operation

One attempt per input. An attempt reads and writes Memory and sends one Emission; it ends in its outcome.

```ethos
Operation
[ herdr:[ Pane Workspace Command Text Keys ] ]
[ Creating.Workspace                 ; attempts
  Starting.{ Pane Command }
  Prompting.{ Pane Text }
  Pressing.{ Pane Keys }
  Closing.Pane ]
[ Created.Pane                       ; what each ends in
  Ended                              ;   the emission went out
  Failed.[ Unknown.Pane              ;   not in Memory
           StoreRefused ] ]
[]
```

## Emission

The herdr command line, as a type. The translator turns it into the call.

```ethos
Emission
[ herdr:[ Session PaneId Workspace
          Command Text Keys Outcome ] ]
[ Herdr.{ Session Verb } ]           ; emissions: one call
[ Outcome ]                          ; outcomes
[ Verb.[ WorkspaceCreate.Workspace   ; types
         AgentStart.{ PaneId Command }
         AgentPrompt.{ PaneId Text }
         Keys.{ PaneId Keys }
         Kill.PaneId ] ]
```

```rust
impl Emittable for Herdr {
    type Outcome = Outcome;
    fn emit(&self, t: &Translator) -> Outcome {
        let mut argv = vec!["--session".into(),
                            self.session.0.clone()];
        argv.extend(self.verb.argv());
        t.call(&t.herdr_path, &argv)
    }
}
```

## Memory

```ethos
Memory
[ herdr:[ Pane Workspace ] ]
[ Known.{ Pane Workspace
          State.[ Open Closed ] }
  Answer.[ Succeeded Failed ] ]
```

```datom
; typed at the CLI
Prompt.{ { main wQ:pT } «Land the messaging line» }
; the reply
Prompted.Done
```
