---
description: How a flow sends a message through the Flow CLI.
placement: system
dependencies: []
---

## The CLI

The CLI is `flow`, called with one datom argument. It speaks to the running Flow Nexus, 0.50.

```sh
flow 'Send.{ Recipient SendableMessage }'
```

## The Send input

```ethos
Send.SendRequest
SendRequest.{ Recipient SendableMessage }
Recipient.[ Address Up ]
Address.{ Aspect Topic Layer }
Aspect.[ Psyche Mind Field ]
Topic.String                              ; an uncapitalized camelCase identifier
Layer.[ Primary Secondary Tertiary Quaternary ]
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

Up is the layer above the sender, in its aspect and topic.

The address takes the model name in the next version.

The priority decides delivery. An awake recipient receives every priority at once, and HardAbrupt alone interrupts; MiddleAbrupt arrives at the next tool boundary. An asleep recipient queues Soft and is woken by MiddleAbrupt or HardAbrupt.

Text is a String, written in guillemets: «text». A datom holding an apostrophe is passed through a shell variable, since the argument is single-quoted.

A Result answers an Order and a Done closes a Task; a Result naming a Task, or a Done naming an Order, is refused Unresolved. The Answerable repeats the original request byte for byte, escapes included, and a Task its Minutes too: a Result matches an Order the recipient sent the sender and that was delivered, a Done an open Task the recipient sent the sender. No match is Unresolved; more than one is Ambiguous.

## Examples

```sh
flow 'Send.{ Address.{ Psyche core Secondary } Soft.Order.«Review the drain fix.» }'
flow 'Send.{ Up Soft.Notice.«The build is green.» }'
flow 'Send.{ Address.{ Mind core Secondary } MiddleAbrupt.Question.«Which revision?» }'
flow 'Send.{ Address.{ Mind core Secondary } Soft.Task.{ 30 «Review the fix.» } }'
flow 'Send.{ Address.{ Psyche core Secondary } Soft.Psyche.{ «the drain» «Fix it today.» } }'
flow 'Send.{ Address.{ Mind core Secondary } Soft.Result.{ Order.«Review the fix.» «Reviewed; green.» } }'
flow 'Send.{ Address.{ Mind core Secondary } Soft.Done.{ Task.{ 30 «Review the fix.» } «Reviewed; green.» } }'
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
                 NoLayer NotConfigured NoneAbove NotMessage Taken.Address
                 Unidentified.SeatEvidence Store.String NotSendServer.Process
                 Oversized.SendPayloadSize Direct.String TopicRefused.Topic
                 Unresolved Ambiguous MinutesRefused.MinutesRefusal ]
MinutesRefusal.[ Zero Negative Unreachable ]
```

Failed.ReceiptUncertain on a Soft or MiddleAbrupt Send means the message was placed in the recipient's pane without a receipt; it is delivered, and is not sent again.

```datom
Sent.{ Claude 7a89916f-3849-5122-89ac-f99fb99b9f70 37888ad9-4633-45a3-8e65-c191568ffb17 }
SendRefused.Unknown.Address.{ Field verifyNoSuchTopic Quaternary }   ; Soft to a metaflow Flow does not hold
Failed.{ RecipientUnavailable.{ Field verifyNoSuchTopic Quaternary } } ; MiddleAbrupt or HardAbrupt to one
SendRefused.TopicRefused.BadTopic
SendRefused.MinutesRefused.Zero
SendRefused.Unresolved                                                ; a Result or Done naming no open request
```
