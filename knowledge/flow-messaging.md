---
description: How a flow sends a message through the Flow CLI.
placement: system
dependencies: []
---

## The CLI

The CLI is `flow`, called with one datom argument.

```sh
flow Send.{ Recipient Delivery SendableMessage }
```

## The Send input

The Signal ethos declares the query and its request:

```ethos
Send.SendRequest
SendRequest.{ Recipient Delivery SendableMessage }
```

```ethos
Address.{ Aspect Topic Layer }
Recipient.[ Address Up ]
Delivery.[ Queue Wake ]
Aspect.[ Psyche Mind Field ]
Layer.[ Primary Secondary Tertiary Quaternary ]
Said.{ Context.String Verbatim.String }
AnswerableTask.{ Minutes String }
Minutes.Integer
SendableRequest.[ Order.String
                  Question.String
                  Psyche.Said
                  Psyches.Vector<Said>
                  Result.{ Answerable String }
                  Notice.String
                  Task.AnswerableTask
                  Done.{ Answerable String } ]
SendableMessage.[ HardAbrupt.SendableRequest
                  MiddleAbrupt.SendableRequest
                  Soft.SendableRequest ]
```

Recipient is an Address, or Up.

Delivery is Queue or Wake. Written with two fields, Recipient and SendableMessage, the Send takes Delivery Wake.

SendableMessage is HardAbrupt, MiddleAbrupt or Soft, carrying Order, Question, Psyche, Psyches, Result, Notice, Task or Done.

Text is a String, written in guillemets: «text».

## Examples

```sh
flow Send.{ Address.{ Psyche core Secondary } Soft.Order.«Review the drain fix.» }
```

A Notice up, held in the queue until the recipient is next delivered to:

```sh
flow Send.{ Up Queue Soft.Notice.«The build is green.» }
```

A Question that interrupts at the next tool boundary:

```sh
flow Send.{ Address.{ Mind core Secondary } MiddleAbrupt.Question.«Which revision?» }
```

A Psyche carrying context and the verbatim words:

```sh
flow Send.{ Address.{ Mind core Secondary } Soft.Psyche.{ «context» «verbatim» } }
```

A Task with its Minutes:

```sh
flow Send.{ Address.{ Mind core Secondary } Soft.Task.{ 30 «Review the fix.» } }
```

## The replies

A send is answered with one of:

```ethos
SendAccepted.VisibleSendAcceptance
SendRefused.VisibleRefusal
Sent.VisibleSendReceipt
Failed.VisibleSendFailure
```

- SendAccepted: a VisibleSendAcceptance, a DeliveryCursor and a DeliveryState (Queued, Attempting, Retryable, Uncertain, Delivered, Failed or Withdrawn).
- Sent: a VisibleSendReceipt, a NativeReceipt.
- SendRefused: a VisibleRefusal, among them Locked, Asleep, NoLayer, NoneAbove, TopicRefused, Unresolved, Ambiguous and MinutesRefused.
- Failed: a SendFailure reason: RecipientUnavailable, QueueNotPermitted, Refused, ReceiptUncertain or NotSent.
