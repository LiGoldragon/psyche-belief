---
description: Which model thinks, designs, delegates or speaks to the living, and in which metaflow, is decided, or a model is named natively.
dependencies: []
---

## Roles are explained by layer, not by model

Roles are explained by layer, not by model; one skill maps layer to model.

| Layer | Claude (Psyche) | OpenAI (Mind, Field) |
|---|---|---|
| Primary | Fable | Astra |
| Secondary | Opus | Sol |
| Tertiary | Sonnet | Luna |
| Quaternary | Haiku | Luna, low effort |

Every metaflow runs at medium effort, except the OpenAI Quaternary.

## Delegation ceiling

A complex judgment is made by Opus, Fable or
Astra; Sonnet and Sol are not trusted with
complex reasoning or inference.

Each layer has a ceiling on what subflows it may launch. Conservative by
default: prefer the lower layer.

### OpenAI side

Luna launches only Luna. Sol is not
launched lightly; it is getting expensive. Astra launches Sol and Luna — try Luna first. Astra is main-flow only: no flow ever
launches an Astra subflow.

### Claude side

Sonnet launches Sonnet and Haiku. Opus launches
Sonnet and Haiku, and sometimes Opus, but rarely. Fable launches Opus and
Sonnet often, and Haiku for small jobs. Fable is main-flow only: no flow
ever launches a Fable subflow.

## One declaration sets the model everywhere

The model is declared once, as typed configuration in Flow, mutated only
through the meta wire. Skill variables carry that value by name into every
skill, launcher and brief. Nothing else holds a model name, so a launcher
never writes one by hand and no flow is started in a metaflow by accident.

## Native names use aspect, topic and layer

Every native main session is titled `{ <Aspect> <Topic> <Layer> <FLOW_ID> }`.
The layer selects the configured model through the table above, so the
title names the layer, never the model.

Horizontal communication joins aspects at the same layer.
Vertical communication stays within one aspect and normally advances one layer
at a time.

Aspect, topic, layer, exact model identifier, Flow ID, and native binding
remain separate typed facts. The title grants none of the identity,
authority, availability, or routing those facts establish.

Horizontal routing selects the unique eligible cell in the target aspect at
the sender's layer.
Busy is still
eligible.
Multiple bindings for one cell are an unresolved conflict, never fanout.
Resolve the binding
immediately before each attempt.

## A grunt job goes down, not up

A simple job — a book rebuilt, a page published, a module located, a file moved — goes to a Tertiary or a Quaternary; a Secondary is never in charge of redoing a book. Once a Secondary has figured out what to do, the doing is handed down.

## A Fable flow is served

In the long term, a Fable flow does only the work that needs Fable. Every errand around it — fetching, relaying, publishing, reporting, delivering — is done for it by the flows below it, unasked, and it is never asked what another flow can find out or be ready for.
