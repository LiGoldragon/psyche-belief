---
description: An ethos file is written, or a type, trait or layout is judged against what the living wants ethos to be.
dependencies: [knowledge-datom, knowledge-protos]
---

## Ethos and Nexus are infrastructure

Ethos and Nexus are basic infrastructure, not examples: the wood houses are built from. Chronos is the example project built with them, short term.

## Where the golden ethos lives

```
┌──────────────────────────────────────────┐
│ vision-ethos                             │
│                                          │
│  what ethos is · its layout              │
│  its two anatomies: types and traits     │
│                                          │
│  ┌────────────────────────────────────┐  │
│  │ the ethos of ethos                 │  │
│  │ the types an ethos file is made of │  │
│  │ the first golden ethos             │  │
│  └────────────────────────────────────┘  │
└───────────────────┬──────────────────────┘
                    │ example
                    ▼
        ┌───────────────────────┐
        │ vision-flow-ethos     │
        │ the Flow Nexus, in    │
        │ ethos; its own skill  │
        └───────────────────────┘
```

The anatomy of ethos lives in vision-ethos itself, as
the first golden ethos; Flow's ethos is one example,
in its own skill.

## What Ethos is

Ethos is the schema language. Of the two main syntaxes most agents
will face, Ethos specifies the types and Datom fills them with data.

Ethos is central. The anatomy of the system, every type and every trait
it uses, is read in its ethos; an implementation is mostly the
hand-written bodies.

## Why Ethos

All the legacy languages have a high noise ratio. Some lisps came
close but lacked the correctness of Rust or Haskell; those have the
correctness but allow no higher layer of abstraction that keeps the
correctness of the whole. Ethos writes the mental model and the code
in one swoop.

## Roots

Library, Signal, Operation, Memory. No version in a file. Signal's sections are
queries and responses, since there is communication; Sema's are record
types, the rest to be decided. Signal gives a Nexus its main types and
Sema its database types.

Four roots: Library, Signal, Operation, Memory. Signal declares what a Nexus says; Operation what it does, one operation type for every effect; Memory what it remembers; Library what they share. A memory trait carries a standard successful-or-unsuccessful change and, for each version, the upgrade from the previous format; that upgrade is the very edit the type needs.

## Non-repetition

Any repetition in ethos syntax is an implementation failure. Ethos
aims to be the most terse, non-repetitive syntax ever made.

Terseness is in the low amount of noise, never in shortened words.

## Self-description

A datom object's basic CLI help emits the Ethos that describes its
anatomy. The wanted mechanism extends this: point at any object —
CLI now, Mentci later — and its Ethos prints, self-describing and
self-evident. The schema syntax serves two audiences: it trains
agents to use things properly, and it shows where the design is
lacking.

## Horizon

Ethos will eventually replace everything, Rustlang becoming its
assembly layer. Designs are chosen for that horizon; what it
enables — generator emission among it — comes in its time.

## Trait

Trait is the word for the bearer of capabilities, the same word in
ethos and in Rust; kind might be used to also mean traits.
In ethos there are no generics, only traits. Declaring a new trait
declares a new trait in the Rust world and might imply more in the
ethos world.

A capability speaks in Self, the trait's own parameters and other traits; a concrete type in an input is a trait not yet named.

## Naming

Traits are qualifier-named: Runnable, Textualizable, Structural,
Embodied. Run is not a trait. The verbs Rust imposes, Write and Read
among them, are tolerated as legacy, for cognitive ease while Rust
and ethos code are switched between so often; once ethos is the
authored language that debt is removed.

## Ethos and the Rust it generates are shown apart

An example shows the Ethos file and the Rust it generates as two blocks, each named for what it is: the Ethos, then the Rust generated from it. They never share one block, because they never share one file.

## Identity

A trait is identified as a Rust trait is, by its name and its
constraints, written as one head: Processable<[Clonable Sendable]
Serializable>. A constraint is a trait, or a bracket of traits: what
Rust writes as a generic parameter with its bounds, ethos writes as
the bounds alone, since in ethos there are no generics, only traits; a
constraint in a trait declaration is a trait, never a type. Two heads
that differ in a constraint are two traits. Which constraints belong
to the identity is not a decision to make: the ethos compiles to
Rust, and what identifies the trait identifies the trait. What else a
trait declares, its supertraits, its associated types and constants,
its capabilities, is its definition. Angle brackets hold the
constraints; they are a protos delimiter, recycled from Rust as
Result and Self are.

The Ethos:

```
Library
[ std:[ Clonable Sendable Serializable ] ]                  ; imports: where the three constraint traits come from
[]                                                          ; types
[ Processable<[Clonable Sendable] Serializable>.[ … ] ]     ; traits: the head is the identity, the name and two
                                                            ;   constraints, the first a bracket of two traits, the
                                                            ;   second one trait; the bracket after the dot holds
                                                            ;   its capabilities, its definition
[]                                                          ; associations
```

The Rust generated from it:

```rust
// The trait's identity: its name and its constraints, two generic parameters with their bounds.
// What ethos writes as the bounds alone, Rust writes as a named parameter carrying them;
// the parameter names are Rust's need, not the trait's.
pub trait Processable<A: Clone + Send, B: Serialize> { /* … */ }
```

## Declaration: File

The unit is File: one file, one Rust module. No namespace inside a
file. An ethos file is written in the sweet form: the root's head,
then the sections as siblings, the outer braces omitted. The braced
form — the root's head opening braces that hold every section — is
the canonical form. The sweet form is kept out of the main logic run:
before the text is read as ethos at all, the file is converted
mechanically to the canonical form, so the ethos reader sees only
proper ethos.

An ethos file carries no version; datom has no versions. What is
versioned is versioned in a manifest of some kind, never in the file.

A Library's sections, in order, are imports, types, traits and
associations. Every root's first section is its imports; its own
sections follow.

```
; the sweet form, as a file is written: the head, then the sections as siblings
Library
[ protos:String ]               ; imports
[ Record.{ String Integer } ]   ; types
[]                              ; traits
[]                              ; associations

; the canonical form the reader sees, after the mechanical conversion
Library.{ [ protos:String ]
          [ Record.{ String Integer } ]
          []
          [] }
```

## The type ethos

`Type` is a single-field variant carrying one declaration, so its payload is the declaration's own form, as any single-field variant's is; it is no exception to the datom.

```
Type.CommitMessage.[ Landing.⟦String⟧
                     Fix.String ]
```

## Imports

An import starts with a colon, followed by uncapitalized namespace segments separated by colons, ending in the type: `:namespace:sub:Type`. It is usable inline in a type declaration or a field, and the import section uses the same syntax: `:protos:String`, or `:protos:[ String Integer ]` for several. An explicit import and an intrinsic name mean the same thing. The names known without import depend on the Ethos object type; a Library, the standard library, knows String, Integer, Decimal, Boolean, Meaning, Vector, Option, Result, Self and Sized.

```
Library
[ :protos:[ String Textualizable ]   ; imports
  :datom:Datom ]
[ Record.{ String Datom } ]          ; types: Datom, imported
[]                                   ; traits
[ Record.[ Textualizable ] ]         ; associations: Textualizable, imported
```

The generated code carries no `use` statements; each imported name is
written fully qualified: `:protos:String` appears as `protos::String`,
`:datom:Datom` as `datom::Datom`.

An import may stand where the type is used, with no entry in the imports section. In a declaration the colon replaces the dot: `Topic:custom:Name` declares `Topic` over the type `Name` from the namespace `custom`. A field takes the import with its leading colon: `Failure.{ :protos:Error String }`. The colon marks the import; the namespace segments are uncapitalized and the type is capitalized.

```
Library
[]                              ; imports
[ Topic:custom:Name             ; an alias, inline
  Failure.{ :protos:Error       ; a field, inline
            String } ]
[]                              ; traits
[]                              ; associations
```

```
+--------------------------------------------+
| the registry                               |
+--------------------------------------------+
                      |
                      | holds uncapitalized segments
                      v
+--------------------------------------------+
| :namespace:sub                             |
+--------------------------------------------+
                      |
                      | ends in the type
                      v
+--------------------------------------------+
| :namespace:sub:Type                        |
+--------------------------------------------+
         |                          |
         | listed in                | written in
         v                          v
+-------------------+  +---------------------+
| the import        |  | a declaration or    |
| section           |  | a field, inline     |
+-------------------+  +---------------------+
```

## What a declaration turns into

A declaration turns into the Rust type with named fields, bearing the
datom traits through the derive, which Ethos Zero emits with the type.
A field is named after its type in snake case; a constructed type
type-first, `string_vector`, `lock_option`; a repeated type as first
and second.

The Ethos:

```
Library
[]                                            ; imports
[ LockId.Integer                              ; types
  LockName.String
  Lock.{ LockId LockName Vector<String> Option<Lock> }
  Generation.{ String String } ]
[]                                            ; traits
[]                                            ; associations
```

The Rust generated from it:

```rust
pub type LockId = Integer;
pub type LockName = String;
#[derive(Datomizable, Compositional)]
pub struct Lock { pub lock_id: LockId, pub lock_name: LockName, pub string_vector: Vec<String>, pub lock_option: Option<Lock> }
#[derive(Datomizable, Compositional)]
pub struct Generation { pub first_string: String, pub second_string: String }
```

## Inline types

A type may be declared where it is used. The inline struct or enum is
a full type whose derived name carries an underscore, non-idiomatic
for a Rust type, so it never collides and reads at a glance as
inferred from the sugar.

The Ethos:

```
Library
[]                                                       ; imports
[ LockId.Integer                                         ; types
  LockName.String
  Lock.{ LockId LockName }
  LockRejection.[ DuplicateName.Lock                     ;   an enum: one variant naming a defined type,
                  PathOverlap.{ Lock Lock } ] ]          ;   one declaring its payload inline
[]                                                       ; traits
[]                                                       ; associations
```

The Rust generated from it:

```rust
pub type LockId = Integer;
pub type LockName = String;
#[derive(Datomizable, Compositional)]
pub struct Lock { pub lock_id: LockId, pub lock_name: LockName }
#[derive(Datomizable, Compositional)]
pub struct PathOverlap_Data { pub first_lock: Lock, pub second_lock: Lock }
#[derive(Datomizable, Compositional)]
pub enum LockRejection { DuplicateName(Lock), PathOverlap(PathOverlap_Data) }
```

Everything is a type; there is no key-value. A type used once is declared inline where it is used; a type used in more than one place is declared once and named. A variant's payload is written in the variant and bears the variant's name; no second type is invented to hold it. Inline nesting goes about three deep; past that, the type comes from a Library.

## White braces define a struct

White braces define a struct, so a struct definition looks different from a struct value. The definition, in ethos, names the types of its positions inside white braces; the value, in datom, fills them inside plain braces.

```
Library
[]                              ; imports
[ LockId.Integer                ; types
  LockName.String
  Lock.⦃ LockId LockName ⦄ ]    ; a definition
[]                              ; traits
[]                              ; associations
```
```
{ 7 renew }
```

```
+--------------------------------------------+
| a struct                                   |
+--------------------------------------------+
         |                          |
         | is defined in            | is filled in
         v                          v
+-------------------+  +---------------------+
| white braces,     |  | plain braces,       |
| in ethos          |  | in datom            |
+-------------------+  +---------------------+
```

## A variant named as a defined type carries that type

When a variant's name is a type already defined in the library, that
type is the data the variant carries. Nothing further is written.

The Ethos:

```
Library
[]                                         ; imports
[ FilePath.String                          ; types: FilePath is an alias of String
  SyntaxError.Vector<FilePath>             ;        SyntaxError is a vector of FilePath
  GenerationFailure.[ SyntaxError          ;        an enum: the variant SyntaxError is bare here,
                      Unwritable ] ]       ;        but SyntaxError is a defined type, so it carries one
[]                                         ; traits
[]                                         ; associations
```

The Rust generated from it:

```rust
pub type FilePath = String;
pub type SyntaxError = Vec<FilePath>;
#[derive(Datomizable, Compositional)]
pub enum GenerationFailure { SyntaxError(SyntaxError), Unwritable }
```
```
GenerationFailure.SyntaxError.[ /abs/orchestrate.ethos ]     ; the datom
```

## A variant may declare its payload inline

Instead of naming a defined type, a variant may declare what it
carries in place: a vector, a struct, or an enum, each a full type
with a derived name, recursively.

The Ethos:

```
Library
[]                                                        ; imports
[ FilePath.String                                         ; types
  GenerationFailure.[ SyntaxError.Vector<FilePath>        ;   the payload declared inline: a vector
                      Unwritable.{ FilePath String } ] ]  ;   declared inline: a struct, derived name
[]                                                        ; traits
[]                                                        ; associations
```

The Rust generated from it:

```rust
pub type FilePath = String;
#[derive(Datomizable, Compositional)]
pub struct Unwritable_Data { pub file_path: FilePath, pub string: String }
#[derive(Datomizable, Compositional)]
pub enum GenerationFailure { SyntaxError(Vec<FilePath>), Unwritable(Unwritable_Data) }
```

Every variant is capitalized: Ethos reads only a capitalized symbol as a variant.

The Ethos:

```
Reply.[ Accepted.Integer   ; two variants
        Refused.String ]
```

An enum has two variants or more; an enum of one variant is refused.

The Ethos:

```
Reply.[ Accepted ]   ; refused: one variant
```

## An open enum

An open enum is an Ethos object whose capitalized words are its fixed variants. A word that is not capitalized is its implied extensible variant, a camel ID: a word-based camel-case identifier, written bare, with no variant head before it. The name camel ID is temporary. A check that a word is a word-based camel-case identifier comes long term; short term, none is made.

The metaflow topic is an open enum: its fixed variants are a constant set, such as the core topic, and the users or the machine extend it with camel IDs as they need topics.

The same mechanism carries an object that is represented unconventionally, such as a word-based hash.

```
+--------------------------------------------+
| a word in an open enum's position          |
+--------------------------------------------+
        |                        |
        | capitalized            | uncapitalized
        v                        v
+----------------+     +---------------------+
| fixed variant  |     | camel ID            |
+----------------+     +---------------------+
        |                        |
        |                        | is checked
        |                        | long term as
        |                        v
        |             +---------------------+
        |             | word-based          |
        |             | camel-case          |
        |             | identifier          |
        |             +---------------------+
        | is a                   | is a
        v                        v
+--------------------------------------------+
| value of the open enum                     |
+--------------------------------------------+
```

## Every declared type bears both traits

Ethos Zero emits `Datomizable` and `Compositional` on every struct and
enum it generates, so every ethos-declared type always bears both
traits and no declared type can exist without them. An alias bears them
through the type it names: an alias is not a new type and cannot carry
a derive.

```rust
pub type FilePath = String;                  // an alias: String already bears both
pub type SyntaxError = Vec<FilePath>;        // an alias: Vec<T> bears both for any T that does
#[derive(Datomizable, Compositional)]        // a type: always derived
pub enum GenerationFailure { SyntaxError(SyntaxError), Unwritable }
```

## The datom traits are compiled in only where text is spoken

A generated signal library bears `Datomizable` and `Compositional`
conditionally, under a feature the CLI and client enable and the Nexus
does not. The Nexus compiles the same types without any
textualization capability and without datom-codec as a dependency.

```rust
// emitted by Ethos Zero into the signal crate
#[cfg_attr(feature = "datom", derive(Datomizable, Compositional))]
pub enum Query { Lock(LockRequest), Release(LockId) }
```
```toml
# the CLI's manifest
signal-orchestrate = { version = "…", features = ["datom"] }
# the Nexus's manifest
signal-orchestrate = { version = "…" }
```

## Shapes and placement

Each section has its own parsing context; placement carries the
meaning. Head then symbol is a variant of `Query` or `Response` in a
Signal's first two sections, an alias in the types section. An enum
declaration is a vector of its variants, and uses the vector's
delimiters. Ethos may generate default implementations for Query and
Response, which is why Signal is its own root.

The Ethos:

```
Signal
[]                                                     ; imports
[ Lock.LockRequest  Release.LockId ]                   ; queries
[ Locked.Lock  Released.Lock ]                         ; responses
[ LockId.Integer                                       ; types
  LockName.String
  FlowId.String
  LockRequest.{ LockName FlowId }
  Lock.{ LockId LockName } ]
```

The Rust generated from it:

```rust
pub enum Query    { Lock(LockRequest), Release(LockId) }
pub enum Response { Locked(Lock), Released(Lock) }
pub type LockId = Integer;
pub type LockName = String;
pub type FlowId = String;
```

## White square brackets define a vector

White square brackets around an item type define a vector type, replacing the word Vector, which is so common: `⟦String⟧` is the vector of String. The vector value keeps its plain brackets in datom.

```
+--------------------------------------------+
| a vector type                              |
+--------------------------------------------+
         |                          |
         | was written as           | is written as
         v                          v
+-------------------+  +---------------------+
| the word Vector   |  | white square        |
| and angle         |  | brackets around     |
| brackets          |  | the item type       |
+-------------------+  +---------------------+
```

## Traits are explicit; bodies are hand-written

A trait is declared, never inferred; an association asserts the type
bears it. The generated Rust carries a compile-time assertion that the
type bears the trait; the interaction body is hand-written Rust.

The Ethos:

```
Library
[]                                                ; imports
[ Record.{ String Integer } ]                     ; types
[ Summarizable.[ summarize.[ String ] ] ]         ; traits
[ Record.[ Summarizable ] ]                       ; associations
```

The Rust generated from it:

```rust
#[derive(Datomizable, Compositional)]
pub struct Record { pub string: String, pub integer: Integer }
pub trait Summarizable { fn summarize(&self) -> String; }
// Compile-time assertion: Record bears Summarizable.
const _: () = {
    fn assert_record_summarizable<T: Summarizable>() {}
    let _ = assert_record_summarizable::<Record>;
};
```

An ethos declares the traits its types bear. Types that bear no trait describe a system that does nothing; such an ethos is not written.

The Ethos:

```
Library
[]                            ; imports
[ Record.{ String Integer } ] ; types
[ Summarizable.[              ; traits
    summarize.[ String ] ] ]
[ Record.[ Summarizable ] ]   ; associations
```

## Trait syntax

A simple trait opens with a bracket after the dot. Its capabilities sit
inside. The receiver after a capability's head names who is called:
`.` takes self, `!` takes mutable self, `:` takes no self. A
capability with inputs is a headed brace: inputs in a bracket, yield
in a bracket. A yield bracket holds one type.

The Ethos:

```
Library
[]                                                            ; imports
[ SinkError.[ Closed Full ] ]                                 ; types
[ Fillable.[ push!{ [ String ] [ Result<Integer SinkError> ] } ; traits
             drain![ Vector<String> ]
             create:[ Self ] ] ]
[]                                                            ; associations
```

The Rust generated from it:

```rust
#[derive(Datomizable, Compositional)]
pub enum SinkError { Closed, Full }
pub trait Fillable {
    fn push(&mut self, input: String) -> Result<Integer, SinkError>;
    fn drain(&mut self) -> Vec<String>;
    fn create() -> Self;
}
```

A complex trait opens with a brace after the dot. Inside: supertraits in
a bracket, associated types with their constraints in a bracket,
associated constants in a bracket — upper case, each the name, a dot,
and its type — and capabilities in a bracket.

The Ethos:

```
Library
[ std:Serializable ]                                ; imports
[]                                                  ; types
[ Fillable.[ create:[ Self ] ]                      ; traits
  Streamable.{ [ Fillable ]
               [ Item<Serializable> ]
               [ CAPACITY.Integer ]
               [ next![ Option<Item> ] ] } ]
[]                                                  ; associations
```

The Rust generated from it:

```rust
pub trait Fillable { fn create() -> Self; }
pub trait Streamable: Fillable {
    type Item: Serializable;
    const CAPACITY: Integer;
    fn next(&mut self) -> Option<Self::Item>;
}
```

A trait's identity is its name and its constraints, as stated in the
Identity section above.

## Associations

An association declares that a type bears a trait: the type's name, a
dot, a bracket of its traits. In the Signal and Sema roots the
associations of the query, response and record types are implied and
never written. In a Library they are the fourth section, after the
traits.

The Ethos:

```
Library
[]                                                       ; imports
[ Sink.{ String Integer } ]                              ; types
[ Summarizable.[ summarize.[ String ] ]                  ; traits
  Fillable.[ create:[ Self ] ] ]
[ Sink.[ Summarizable Fillable ] ]                       ; associations
```

The Rust generated from it:

```rust
// Compile-time assertion: Sink bears Summarizable and Fillable.
const _: () = {
    fn assert_sink_summarizable<T: Summarizable>() {}
    let _ = assert_sink_summarizable::<Sink>;
    fn assert_sink_fillable<T: Fillable>() {}
    let _ = assert_sink_fillable::<Sink>;
};
```

Interactions — the term for trait implementations — use the type
itself in all cases.

No tuple in the code we design; if some parts require it (standard
traits, dependencies), then it is allowed at that contact point only.

## Spacing

Space the delimiters and the inner content. Ethos follows the
canonical protos print: a space inside every bracket and brace
at both ends when non-empty.

Ethos expands vertically: a structure with more than one element opens on its line and its elements hang beneath the first, aligned; the closing delimiter ends the last element's line. Nothing that has a next layer sits on one line.

Ethos carries a comment on every section and on every line that has a next layer, saying in plain words what the machine reads there; a comment runs from ; to the end of the line.

## Zero

Ethos Zero was first named Ethos Monolith; the two are the same thing.
Zero as in version 0: no daemon yet, no Nexus. The ethos repository is
for the ethos nexus that follows.

## Generation

By request to ethos-zero, which is not a daemon, hence its name; committed, held fresh by a test.

```
ethos-zero 'Generate.{ /abs/orchestrate.ethos /abs/out }'
```
