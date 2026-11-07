---
description: How a flow sends a message through the Flow CLI.
placement: system
dependencies: []
---

## The CLI

The `flow` on PATH is the configured 0.53.1 client. It speaks to the running Flow Nexus and takes one datom argument:

```sh
flow 'Send.{ { Psyche core Fable } Soft.Notice.«The build is green.» }'
```

## Running permaflows and their routing

`flow 'Metaflows'` reads current permaflow states. `flow-meta 'Configuration'` reads their committed declarations. The table below was read from both on 2026-11-07; all 22 addresses were `Awake`. A routing description is the declaration's `Purpose` unless it names a bound role. A blank `Purpose` leaves specialized routing unknown. A declared historical task describes the configuration and grants no present authority.

| Address | Work routed there by current evidence |
|---|---|
| `{ Field protosReview Sonnet }` | Declared purpose: sole reviewer and publisher of the four exact Protos consumer candidates, under Field core Astra coordination and the explicit review brief. |
| `{ Field protosConsumers Sonnet }` | Declared purpose: implementation lane for the consumers of Protos: datom-codec first, then signal, meta-signal and the other dependents, new versions, locks, tests and pushes, after the approved dependency graph, under Field core Primary source custody. |
| `{ Field protos Sonnet }` | Declared purpose: implementation lane for Protos: the protos crate, its version, UPGRADES, tests and review, under Field core Primary source custody. |
| `{ Field core Astra }`, `{ Field core Sol }` | Specialized routing is unknown: `Purpose` is blank and no routing role is bound. |
| `{ Mind datomCodec Sol }`, `{ Mind herdrNexus Sol }`, `{ Mind nixCriomos Sol }`, `{ Mind orchestrate Sol }`, `{ Mind versionZero Astra }`, `{ Mind versionZero Sol }`, `{ Mind core Astra }`, `{ Mind core Sol }`, `{ Mind lojix Sol }`, `{ Mind flowNexus Sol }` | Specialized routing is unknown: `Purpose` is blank and no routing role is bound. |
| `{ Mind beliefNexus Astra }` | Specialized routing is unknown: `Purpose` is blank and no routing role is bound. |
| `{ Psyche book Haiku }` | `Purpose` is blank. Its bound `role:book-publishing-procedure` says it is sent a presentation source path, publishes the built page, and returns the title and link to the ordering flow. |
| `{ Psyche core Fable }`, `{ Psyche core Opus }` | Specialized routing is unknown: `Purpose` is blank and no routing role is bound. |
| `{ Psyche core Sonnet }` | `Purpose` is blank. Its bound `role:psyche-core-tertiary` receives the living's notice of a book comment, asks the appropriate flow to relay the comments, and relays a request for a proposal or design whole to Psyche core Opus. |
| `{ Psyche criomos Opus }` | Declared purpose: fix the CriomOS infrastructure audit findings and report effects to Psyche core Primary. This recorded task is not current work authority. |
| `{ Psyche restart Opus }` | Declared purpose: implement Flow 0.51.3 Restart in the same native session and report effects to Psyche core Primary. This recorded historical task is not current work authority. |

Read both queries again before routing work: state and configuration can change independently.

## The Send input

An address names its model: { Psyche core Fable }, { Mind core Astra }. Any model stands in any aspect. The recipient is the address, written bare.

```ethos
Send.SendRequest
SendRequest.{ Recipient SendableMessage }
Recipient.Address
Address.{ Aspect Topic Model }
Aspect.[ Psyche Mind Field ]
Topic.String                              ; an uncapitalized camelCase identifier
Model.[ Fable Opus Sonnet Haiku Astra Sol Luna Terra ]
Said.{ Context.String Verbatim.String }   ; what his words were about, and his words whole
Minutes.Integer
AnswerableTask.{ Minutes String }
Answerable.[ Order.String
             Task.AnswerableTask ]
SendableRequest.[ Order.String
                  Question.String
                  Psyche.Said
                  Psyches.Vector<Said>
                  Result.{ Answerable String }  ; answers the request it names, written whole
                  Notice.String
                  Task.AnswerableTask
                  Done.{ Answerable String } ]
SendableMessage.[ HardAbrupt.SendableRequest
                  MiddleAbrupt.SendableRequest
                  Soft.SendableRequest ]
```

The priority decides delivery. An awake recipient receives every priority at once, and HardAbrupt alone interrupts; MiddleAbrupt arrives at the next tool boundary. An asleep recipient queues Soft and is woken by MiddleAbrupt or HardAbrupt.

Text is a String, written in guillemets: «text». A text keeps its ordinary spaces. A datom holding an apostrophe is passed through a shell variable, since the argument is single-quoted.

A Result answers an Order and a Done closes a Task; a Result naming a Task, or a Done naming an Order, is refused Unresolved. The Answerable repeats the original request byte for byte, escapes included, and a Task its Minutes too: a Result matches an Order the recipient sent the sender and that was delivered, a Done an open Task the recipient sent the sender. No match is Unresolved; more than one is Ambiguous.

## Examples

```sh
flow 'Send.{ { Psyche core Opus } Soft.Order.«Review the drain fix.» }'
flow 'Send.{ { Mind core Astra } MiddleAbrupt.Question.«Which revision?» }'
flow 'Send.{ { Mind core Astra } Soft.Task.{ 30 «Review the fix.» } }'
flow 'Send.{ { Psyche core Fable } Soft.Psyche.{ «the drain» «Fix it today.» } }'
flow 'Send.{ { Mind core Astra } Soft.Result.{ Order.«Review the fix.» «Reviewed; green.» } }'
flow 'Send.{ { Mind core Astra } Soft.Done.{ Task.{ 30 «Review the fix.» } «Reviewed; green.» } }'
```

## The replies

```ethos
Sent.NativeReceipt                         ; placed and received by the seat
SendAccepted.{ DeliveryCursor DeliveryState }
SendRefused.VisibleRefusal
Failed.{ SendFailureReason }
NativeReceipt.{ HarnessKind NativeSessionId NativePromptId.String }
DeliveryState.[ Queued Attempting Retryable.RetryCause Uncertain
                Delivered.NativeReceipt Failed.VisibleRefusal Withdrawn ]
SendFailureReason.[ RecipientUnavailable.Address
                    QueueNotPermitted
                    Refused.VisibleRefusal
                    ReceiptUncertain
                    NotSent.String ]
VisibleRefusal.[ Locked Held.Lock Awake Asleep Lapsed Unknown.VisibleUnknown
                 NotConfigured NotMessage Taken.Address
                 Unidentified.SeatEvidence Store.String NotSendServer.Process
                 Oversized.SendPayloadSize Direct.String TopicRefused.Topic
                 Unresolved Ambiguous MinutesRefused.MinutesRefusal ]
VisibleUnknown.[ Address.Address Lock.Lock Flow Key.Key ]
MinutesRefusal.[ Zero Negative Unreachable ]
```

Failed.ReceiptUncertain on a Soft or MiddleAbrupt Send means the message was placed in the recipient's pane without a receipt; it is delivered, and is not sent again.

```datom
Sent.{ Claude 7a89916f-3849-5122-89ac-f99fb99b9f70 37888ad9-4633-45a3-8e65-c191568ffb17 }
SendAccepted.{ 116 Uncertain }
SendRefused.Unknown.Address.{ Field verifyNoSuchTopic Haiku }   ; an address Flow does not hold
SendRefused.TopicRefused.BadTopic
SendRefused.MinutesRefused.Zero
SendRefused.Unresolved                                           ; a Result or Done naming no open request
```

## When the Flow Nexus cannot deliver

When a Send to a running flow is refused or fails, the message is typed into that flow's herdr pane by hand. Herdr lists each agent with its pane, its native session and the title it shows; the pane is chosen by the title and the session, both checked just before the prompt.

```sh
herdr agent list                       # each agent: pane_id, agent_session, terminal_title
herdr agent get <pane>                   # one pane, its session and state, checked before typing
herdr agent prompt <pane> "$text"    # the message, written as a delivered datom
```

The text is the message as a delivered one reads, with its sender, so the recipient reads it as any other:

```datom
[ { Sender.{ Psyche core Opus } Soft.Notice.«Relayed from Mind core Astra, its words: …» } ]
```

Herdr answers agent_prompted when the text is submitted. That is a submission and not a read: the recipient's own reply is the read. A recipient whose Flow address cannot deliver answers through whatever route reaches the sender, and says so in its reply text.
