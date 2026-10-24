---
description: A book for the living is written, checked, built or published.
dependencies: [vision-book]
---

## The two tools

A book source is a Markdown file that `tools/book-check.clj` and `tools/book-build.clj`, in Primary, both accept; these two tools are the whole check. A book is sent for publication only with the clean output of `tools/book-check.clj` on that exact source, run by the sender; the publisher refuses a book sent without it. The author runs the check until it reports no error, then the build; the publisher runs both again and publishes only what passes both. A refusal returns the source to its author with the tool's words. `tools/book-check.clj` refuses a removed line that is not a whole line of the module at origin main, and a change that cuts a hard-wrapped paragraph.

```sh
bb tools/book-check.clj /absolute/path/to/book.md        # {"checked":true,...} when clean; else {"errors":[...]} by line
bb tools/book-build.clj /absolute/path/to/book.md out.html --figures /absolute/path/to/figures
```

## What a source holds

Outside a proposal a source holds only: one `Presentation.{ «title» }` line, one `# title`, unlabelled diagram fences, and modules shown as they stand, each under a level-two heading `## repo › path`. A module shown as it stands is its text at origin main, byte for byte, front matter left out.

A proposal opens with `### Proposal N: title · repo › path`, numbered from 1; a new module ends the heading with `, a new file`, a deleted one with `, a deleted file`. A line moved between modules is one proposal headed `### Proposal N: title · repoA › pathA, and repoB › pathB`, with a level-four heading for each path, the line in red under the first and green under the second. No other level-three heading exists.

## Red and green

Colour comes only from signed lines. In a change every line opens with `- ` (red, removed), `+ ` (green, added) or two spaces (unchanged, shown for place). A removed line is a whole line of the module at origin main; an added line is not. HTML, inline styles and words like "added" make no colour.

A module line is shown whole. A change to a hard-wrapped paragraph shows every physical line of that paragraph, so no sentence is cut at a wrap. A replaced paragraph is diffed as one paragraph: its removal and its addition together, with only the changed words marked.

```text
### Proposal 1: A message names its sender · psyche-context › vision/messaging.md

**Comment** The sender is resolved from the calling process.

  ## A message is a datom, and it arrives as one
  
- The message body is a datom.
+ The message body is a datom; Flow names its sender.
```

## Marks inside a proposal

Inside a proposal a source holds only its change lines, one Comment, its Alternatives, its Destroy or Archive mark, path headings at level four, and code that the proposed lines themselves land. Inside a proposal every path heading is level four, `#### repo › path`, as the moved-line form has it.

Every fence inside a proposal is signed line by line: red, green, or two spaces for a line kept in place, code-file proposals included, because code shown in a proposal is either what stands at origin main or what is proposed. An unsigned fence inside a proposal is refused.

One `**Comment**` paragraph at most, before every change: the machine's word, in its own colour. `**Alternative 1**`, `**Alternative 2**` and on, two or more, in order, each alone on its line and followed by the exact lines it lands. `**Destroy**` or `**Archive**` opening a paragraph marks a deleted module or record. Prose never sits inside a change; it is a separate paragraph, a blank line apart.

## Fences

An unlabelled fence holds a box-and-arrow sketch and nothing else; each one needs its figure, `fig-N.svg` in the figures directory, drawn by the illustrator from the sketch with every box, label and arrow kept. Every other fence carries its language: `ethos`, `datom`, `rust`, `edn`, `sh`, `yaml`, `text`. An `ethos` fence passes ethos-zero's Check. A figure is at most 52 columns wide. A module written in Markdown is shown as rendered text, never in a fence. No quote block.

Every figure in a book is headed by the module it lives in and one of three states: as it stands, proposed added in green, or proposed removed in red; a figure with no module and no state is refused by the checker.

## Code in a proposal

Code the proposed lines land is shown in labelled fences, the Datom it reads or writes and the Ethos that types it, checked against the source before it is sent.

## Commented books

A book the living has commented on is never changed and never republished. Its redo is a new book at a new link, and the commented one stays as he left it.
