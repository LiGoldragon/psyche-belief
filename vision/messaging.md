---
description: A message between flows is designed, sent or judged: its datom form, priority, per-harness delivery, or what counts as its witness.
dependencies: []
---

## A message is a datom, and it arrives as one

The message body is a datom that lands in the recipient's prompt as a
datom-formatted object. There is no envelope around it.

## Priority is a head on the datom

    Priority.[HardAbrupt MiddleAbrupt Soft]

## Delivery is harness-specific, and the mechanism differs per tier

Hard abrupt on Codex is one Escape, and the prompt submits itself. Hard
abrupt on Claude is two Escapes — the first is taken by the input editor in
vim mode and never reaches the harness — then the prompt, then an explicit
Enter, because after an interrupt the prompt is placed in the composer
without being submitted. Middle abrupt is the terminal prompt, which a
Claude recipient receives at its next tool boundary. Soft waits for the
recipient to finish.

A pressing message wakes its recipient; a message that only queues carries what may wait.

A request to deliver a recipient's queue delivers every queued message, or nothing when none is queued.

## An interrupt witness is not a delivery witness

Inducing an interrupt, placing prompt text, submitting it, and the recipient
consuming it are four separate observations. None of them stands for
another, and a submission is never a read receipt.

## Only messages that act, deliver, or block

A flow sends only what its recipient acts on.

## A hash or an identifier is six characters

A hash or an identifier in a message is its first six characters.

## A message says what the sender intends and what it has done

A message between flows says what the sender intends to do and what it has done.

## A messaging test sends one message

A messaging test sends one message, to a flow that needs it anyway or to a Quaternary started for it and stopped after; it never goes to every flow and never wakes a Primary.

## When Flow holds a delivery

When Flow holds a delivery, the sender falls back to direct Herdr messaging: it finds the recipient's pane in the pane list, sends the text with the first words naming the sender, then Enter. The fallback changes the carrier, never the address: a message for a Primary goes to its Secondary's pane, by Flow or by Herdr alike; no flow but the Secondary writes into a Primary's pane.
