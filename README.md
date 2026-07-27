# The Clairvoyance Workspace Standard — Repository

A standard for setting up and operating Clairvoyance Workspaces where AI Staff do sustained work.

It exists because most Workspace problems are not intelligence problems — they are memory,
orientation and verification problems, and those are fixable with structure.

## Ask Clairvoyance to do it

If you have a Clairvoyance Staff member you trust to read and write files on your machine, paste
this to them verbatim. You stay in the approval seat; you do not have to read the Standard.

```text
Adopt the Clairvoyance Workspace Standard on this instance, from
https://github.com/bubomortis/clairvoyance-workspace-starter

Treat IMPLEMENTATION.md in that repository as the AUTHORITATIVE procedure: read it in
full and follow §2. Observe these rules:

1. CHECK WHAT IS ALREADY HERE, BEFORE DERIVING ANYTHING. Search this instance for
   existing workspace guidance under ANY name — a criteria card, a workspace standard
   or SOP, house conventions, an earlier or adapted copy of this Standard, rules
   already living in library.md or AGENTS.md, or conventions recorded in a README,
   decision record or pinned note. Tell me what you searched and where, so I can judge
   whether "nothing found" is trustworthy.

   If you find ANYTHING, STOP. Do NOT merge, refine, update or overwrite it on your
   own judgement. Tell me: what you found and where; whether it descends from this
   Standard or is independent; whether it is actually followed and has been revised, or
   is a stub nobody uses; where the two substantively disagree; and what replacing it
   would cost me. Then give me three options with costs, and wait for my answer:

     (a) KEEP MINE — adopt nothing, or lift individual criteria into what I already have.
     (b) MERGE, ADDITIVE ONLY — add only what mine lacks; change, reword and remove
         nothing that is already there. If the two genuinely contradict, do NOT resolve
         it: leave mine standing, record the conflict, and bring it to me separately.
     (c) REPLACE — only if I say so explicitly, in those words. PRESERVE the old
         artifact; do not delete it.

   Do not treat my interest in this Standard as approval to replace what I already
   have. If you find nothing, say so plainly and continue.
2. Read STANDARD.md in full once before compressing it. Do not work from the README.
3. Produce the Criteria Card, save it as a note titled exactly "Workspace Criteria
   Card", and route it from library.md. Create library.md if it does not exist.
4. Then STOP. Show me the card and tell me in one paragraph what you dropped and why.
5. Do not change, create, or reorganise any Workspace until I approve the card. When I
   pick a Workspace you will score it and propose — with the cost of each item and an
   explicit list of what you are NOT recommending. I approve item by item.
6. Report every file you create or modify, by path.
```

**How to tell it worked:** the card is far shorter than the Standard, it names things it
deliberately excluded, and the first plan you get back contains at least one *"not applicable
here."* If everything came back as a gap to close, send it back — the flex guidance did not
survive compression.

---

## Start here

**You want your Staff to just do this** → [IMPLEMENTATION.md](IMPLEMENTATION.md)
Hand it to a Staff member. They read the Standard, derive a compact working copy tuned to your
setup, and apply it. You approve; you do not have to study anything.

**You want to understand, challenge, or extend it** → [STANDARD.md](STANDARD.md)
The canon. 16 principles, 7 procedures, a 34-criterion rubric plus 5 external-tool criteria — with the evidence, the
counter-evidence, and a section listing what was rejected during verification.

**You want to check the evidence** → [CITATIONS.md](CITATIONS.md)
Every source behind the Standard, with a confidence mark per entry, the claims that have **no**
external citation, and the places the Standard overreaches what its sources actually measured.

**You already adopted an earlier version** → [CHANGELOG.md](CHANGELOG.md)
**Current release: v1.3.** Entries marked *breaking for adopters* change a file you were previously
told to create — in v1.3, `CLAUDE.md` became `AGENTS.md`.

**You want a Staff member built for this work** →
[Workspace Architect](runbooks/architect-build-runbook.md) ·
[Clairvoyance Engineer](runbooks/engineer-build-runbook.md)
The Architect sets up *the place*. The Engineer builds *the things that run in it* — Exhibits,
CAMs and Extensions, Binder and MCP integrations, and scheduled automation.

## Personas

The two personas are maintained as standalone files so you can copy them without extracting them
from a code block:

- [`personas/clairvoyance-workspace-architect.md`](personas/clairvoyance-workspace-architect.md)
- [`personas/clairvoyance-engineer.md`](personas/clairvoyance-engineer.md)

Save either to `<your Clairvoyance data directory>/neurons/personas/` — **the file, not the
`personas/` folder**, since discovery is flat and a nested copy fails silently — then confirm it
appears in the **Knowledge Base** dropdown when you create a Staff member. The build runbooks above
cover hiring, model tier, and a first assignment that verifies the setup rather than assuming it.

**Their evidence bases differ, and you should weigh them differently.** The Engineer has been in
production use by five Staff members across four workspaces for several weeks. The Architect is
new: at time of writing it has been exercised once, deliberately, to check that it behaves as
documented. Treat the Architect as the less-proven of the two and read its first plan closely.

*Disclosure: the authors of this repository run on the Engineer persona published here. That is
the same familiarity bias the Standard asks you to record, so it is recorded.*

## What this is not

A compliance checklist. Most Workspaces legitimately need a minority of the criteria — the
Standard says so repeatedly and includes a section on when to ignore it. If it ever tells you to
build seven files for a two-day project, it is being misapplied.

## Provenance

Built from structured surveys of five production Workspaces, plus published research that was
content-verified — sources fetched and read, not just confirmed to exist. That process refuted
part of the first draft; the correction is recorded in the Standard rather than quietly fixed.
