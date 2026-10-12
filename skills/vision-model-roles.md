---
description: Which model seat thinks, designs, delegates or speaks to the living is decided, or a model is named natively.
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

Every seat runs at medium effort, except the OpenAI Quaternary.

## Delegation ceiling

Each tier has a ceiling on what subflows it may launch. Conservative by
default: prefer the lower tier.

### Codex side (energy tiers)

Luna launches only Luna. Terra launches Terra or Luna, not Sol. Sol is not
launched lightly; it is getting expensive. Astra launches Sol, Terra, and
Luna — try Terra and Luna first. Astra is main-flow only: no flow ever
launches an Astra subflow.

### Claude side (model names)

Haiku is ultra-low power. Sonnet launches Sonnet and Haiku. Opus launches
Sonnet and Haiku, and sometimes Opus, but rarely. Fable launches Opus and
Sonnet often, and Haiku for small jobs. Fable is main-flow only: no flow
ever launches a Fable subflow.

## One declaration sets the model everywhere

The model is declared once, as typed configuration in Flow, mutated only
through the meta wire. Skill variables carry that value by name into every
skill, launcher and brief. Nothing else holds a model name, so a launcher
never writes one by hand and no flow is born on a seat by accident.

## Native names use aspect and model

Every native main session is titled `<Aspect> <Model> <FLOW_ID>`. The model
display is derived through the authoritative display map from the exact
observed native model identifier; an unmapped identifier blocks readiness.
Versions and variants remain visible. Thus the Medium
Mind seat on `gpt-5.6-sol` is `Mind Sol <FLOW_ID>`; it is never titled Mind
Medium or Mind Soul.

Power remains a separate typed behavioral property. High, Medium, Low, and
Ultra Low determine peer equivalence, delegation ceilings, and escalation;
they are not substituted into the native title.

Horizontal communication joins aspects at equivalent behavioral power.
Vertical communication stays within one aspect and normally advances one rung
at a time. If the adjacent rung is absent or unavailable, routing advances to
the next running rung in that direction, so Low may reach High when Medium is
not running. The missing rung is reported as a gap; it does not make the
message disappear.

Aspect, exact model identifier, model display, behavioral power, Flow ID, and
native binding remain separate typed facts. The title grants none of the
identity, authority, availability, or routing those facts establish.

Horizontal routing selects the unique eligible cell in the target aspect at
the sender's behavioral power. Vertical routing selects the nearest eligible
rung in the requested direction within the same aspect. Busy is still
eligible. Missing or unavailable needs fresh lifecycle and route evidence.
Multiple bindings for one cell are an unresolved conflict, never fanout. No
eligible cell yields an explicit undeliverable result. Resolve the binding
immediately before each attempt. A fallback has succeeded only when the exact
recipient accepts it; an ambiguous attempt remains attached to that recipient
and is reconciled instead of being resent to another rung.
