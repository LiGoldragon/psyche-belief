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
          Command Text Keys Outcome Label State ] ]
[ Create.Workspace
  Start.{ Pane Command Label }
  Prompt.{ Pane Text }
  Press.{ Pane Keys }
  Close.Pane
  List.Session
  Subscribe.Session ]
[ Created.Outcome
  Started.Outcome
  Prompted.Outcome
  Pressed.Outcome
  Closed.Outcome
  Listed.Outcome
  Subscribed.Outcome
  Changed.{ Pane State } ]           ; pushed, each change
[]
```

## Meta

Configure sets one value of the configuration at a time, never the whole; a subscription follows the configuration as it changes. SubscriberCapacity is positive, and an active subscription follows it.

```ethos
Signal
[]                                   ; imports
[ Configure.Set ]                    ; inputs: one value at a time
[ Configured.{ Set Owner             ; outputs: the value set,
               Readiness }           ;   its owner, readiness
  ConfigureRefused.ConfigurationRefusal ] ; or why it was not
[ Set.[ HerdrPath.PathValue          ; types: one per field;
        CallTimeout.Timeout          ;   translator-owned
        OutputLimit.ByteLimit
        TextBudget.BudgetValue
        StartTimeout.Timeout         ;   Nexus-owned
        Polling.Timeout
        FrameCapacity.ByteLimit
        TransportTimeout.Timeout
        SubscriberCapacity.Integer   ;   positive
        Peers.Vector<Peer> ]         ;   the peers admitted
  Owner.[ Nexus Translator ]         ; who answers for a field
  SettingName.[ HerdrPath            ; a field, by name
                CallTimeout
                OutputLimit
                TextBudget
                StartTimeout
                Polling
                FrameCapacity
                TransportTimeout
                SubscriberCapacity ]
  Readiness.[ Awaiting.Vector<SettingName> ; fields still unset
              Ready ]
  PathValue.String
  Timeout.Integer
  ByteLimit.Integer
  NodeLimit.Integer
  DepthLimit.Integer
  BudgetValue.{ NodeLimit DepthLimit }
  Message.String
  SocketPath.String
  UserId.Integer
  ProcessId.Integer
  Peer.{ SocketPath                  ; tentative: a peer
         UserId                      ;   translator, checked
         ProcessId }                 ;   by kernel credentials
  BootstrapRefusal.{ SocketPath      ; the target is not up
                     Message }
  ConfigurationRefusal.[ Invalid.{ Owner ; why a value was refused
                                   SettingName
                                   Message }
                         Unavailable.BootstrapRefusal ] ]
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
  Command.{ AgentName                ; what starts in the pane
            AgentKind
            Executable
            Vector<String> }         ;   its arguments
  AgentName.String
  AgentKind.[ Pi Claude Codex Gemini ; herdr's agent kinds
              Cursor Devin Agy Cline
              Omp Mastracode Opencode
              Copilot Kimi Kiro Droid
              Amp Grok Hermes Kilo
              Qodercli Qwen Maki ]
  Program.String
  Executable.[ Configured            ; the kind's program
               Explicit.Program ]
  Text.String                        ; what is typed
  Keys.Vector<String>
  ErrorCode.String
  ExitStatus.Integer
  Message.String
  Refusal.{ ErrorCode                ; herdr refused
            Option<ExitStatus>
            Message }
  MemoryRefusal.Message
  SocketPath.String
  TransportRefusal.{ SocketPath      ; the connection was refused
                     Message }
  Label.String
  State.[ Open Busy Idle Dead ]
  Attempt.[ Settled                  ; how the last attempt on
            Uncertain ]              ;   the pane ended
  Known.{ Pane Label State           ; an owned pane
          Attempt }
  ObservedEffect.[ Done              ; what herdr was seen to do
                   Created.Pane
                   Listed.Vector<Known> ]
  StorePhase.[ BeforeEmission        ; when the store failed
               Observed.ObservedEffect
               Uncertain ]
  StoreRefusal.{ MemoryRefusal       ; the store failed
                 StorePhase }
  Outcome.[ Done                     ; how every attempt ends
            Created.Pane
            Listed.Vector<Known>
            Refused.Refusal
            Unknown.Pane
            AttemptInProgress.Pane
            Unavailable.TransportRefusal
            Uncertain
            StoreRefused.StoreRefusal ] ]
[]
[]
```

## Operation

One attempt per input. An attempt reads and writes Memory and sends one Emission; every attempt ends in the shared Outcome. The Operation turns what the Emission observed into the shared Outcome.

```ethos
Operation
[ herdr:[ Session Pane Workspace     ; imports
          Command Text Keys Label ]
  :herdr:AttemptOutcome.Outcome ]
[ Creating.Workspace                 ; attempts
  Starting.{ Pane Command Label }
  Prompting.{ Pane Text }
  Pressing.{ Pane Keys }
  Closing.Pane
  Listing.Session
  Subscribing.Session ]
[ Created.AttemptOutcome             ; every attempt ends in
  Started.AttemptOutcome             ;   the shared Outcome
  Prompted.AttemptOutcome
  Pressed.AttemptOutcome
  Closed.AttemptOutcome
  Listed.AttemptOutcome
  Subscribed.AttemptOutcome ]
[]
```

## Emission

The herdr command line, as a type. The translator turns it into the call. Its outcome is what the translator observed, raw and its own type. Listing is two emissions, PaneList and AgentList, one herdr call each.

```ethos
Emission
[ herdr:[ Session PaneId Pane Root   ; imports
          Variable Command Text
          Keys State Refusal ] ]
[ Herdr.{ Session Verb } ]           ; emissions: one call
[ ExternalOutcome ]                  ; outcomes: observed, raw
[ Verb.[ WorkspaceCreate.{ Root      ; types
                           Vector<Variable> }
         AgentStart.{ PaneId         ; Timeout comes from
                      Command        ;   the configuration
                      Timeout.Integer }
         AgentPrompt.{ PaneId Text }
         Keys.{ PaneId Keys }
         PaneClose.PaneId
         PaneList                    ; Listing's two calls
         AgentList ]
  TerminalId.String
  WorkspaceId.String
  TabId.String
  PaneListing.{ Pane TerminalId      ; a pane herdr listed
                WorkspaceId TabId }
  AgentListing.{ Pane TerminalId     ; an agent herdr listed
                 WorkspaceId TabId
                 State }
  ExternalOutcome.[ Done             ; what the translator
                    Started.State    ;   observed
                    Created.Pane
                    Panes.Vector<PaneListing>
                    Agents.Vector<AgentListing>
                    Refused.Refusal
                    Uncertain ] ]
```

```rust
impl Emittable for Herdr {
    type Outcome = ExternalOutcome;
    fn emit(&self, t: &Translator) -> ExternalOutcome {
        let mut argv = vec!["--session".into(),
                            self.session.0.clone()];
        argv.extend(self.verb.argv());
        t.call(&t.herdr_path, &argv)
    }
}
```

## Memory

For the proof of concept, Memory lasts as long as the process.

```ethos
Memory
[ herdr:[ Known ] ]                  ; imports
[ Owned.Known                        ; records: each owned pane
  Answer.[ Succeeded Failed ] ]      ; every change returns it
```

```datom
; typed at the CLI
Prompt.{ { main wQ:pT } «Land the messaging line» }
; the reply
Prompted.Done
```
