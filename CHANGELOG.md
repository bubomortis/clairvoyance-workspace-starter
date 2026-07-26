# Changelog

**Audience: human.** Release history for the Clairvoyance Workspace Standard.
**Status:** Free to copy, adapt, and share.

Companion to [STANDARD.md](STANDARD.md) (the canon) and [CITATIONS.md](CITATIONS.md) (the evidence).

Versions are tagged in this repository. Anything marked **breaking for adopters** changes a file you
were previously instructed to create — those are the entries to read if you have already adopted a
version.

---

## [v1.3] — 2026-07-25

### Breaking for adopters

- **The charter file is now `AGENTS.md`, not `CLAUDE.md`.** A Workspace charter should not be named
  after one model vendor, and `AGENTS.md` is a published open format with broad multi-vendor
  adoption. **If you adopted v1.2 you created `CLAUDE.md`; that file is now `AGENTS.md`.** This is
  the only change in this release that touches files you already made.

### Added

- **SOP-1 step 4 — the runtime auto-load rule.** Most agent runtimes load a file of their own
  choosing into context at session start, and they do not all choose the same name. If yours does
  not read `AGENTS.md`, your charter is silently not loaded and nothing reports it. The rule:
  `AGENTS.md` is canonical; add a vendor-named pointer file **only if** your runtime auto-loads a
  different name; that pointer **may add, never restate**. Two charter files is two sources of truth.
- **§15 — runtime auto-load filenames.** Which runtimes load which file, with a confidence mark per
  entry. Deliberately **non-normative and outside the artifact table**: by C1b a named file is a file
  agents will create, so a vendor roster in normative text would produce Workspaces holding six
  charter files for one runtime — this document committing the failure it documents. It is safe in
  §15 because `STANDARD.md` is `Audience: human` and agents do not read it, which is also why it
  must not be migrated into an agent-facing derive doc or a Criteria Card.
- **`CITATIONS.md`** — every source behind the Standard, with a confidence mark per entry, the claims
  that have **no** external citation, and the places the Standard overreaches what its sources
  actually measured. Routed from `STANDARD.md` and `README.md`, and deliberately **not** from
  `IMPLEMENTATION.md`: evidence does not belong in an agent-facing file (C1).

### Changed

- **"Charter" disambiguated.** Capital-C **Charter** is reserved for the 12 principles in §2.
  The `AGENTS.md` artifact is now consistently the **charter file**. Without this, a reader who
  internalised *"if an SOP conflicts with the Charter, the Charter wins"* would meet *"your charter
  is silently not loaded"* meaning something else entirely — in the most operationally important new
  passage in the document.
- **R3** now reads *"Charter FILE exists"*, resolving the same ambiguity for anyone scoring the
  rubric, without hard-coding a filename into a criterion.

### Known, unfixed

- **C1a and R5 overreach their sources.** Both are phrased around *authorship* — "hand-authored, not
  generated" — but the cited studies measure **tuning vs. no tuning** and contain no hand-authored
  arm. The conclusions still hold on the tuning framing; the wording does not. Recorded in
  `CITATIONS.md` rather than quietly corrected. **When arguing from C1a or R5, argue tuning.**

---

## [v1.2] — 2026-07-25

First public release. 12 principles, 6 procedures, and a 34-criterion rubric scored per layer rather
than as a total — a capability checklist, not a maturity ladder.

### Fixed

- **C7b's success-signal example chained to an exit code**, reproducing the exact failure C7 forbids.
  Now three terms: **work → assert → signal**. With a portable-shell note, because `&&` is a parse
  error in Windows PowerShell 5.1.
- **R25 restated shell-agnostically.** It named an operator the default Windows shell cannot parse,
  so a correct Windows Workspace failed the criterion *by construction*. Found in review and
  independently reproduced before the ruling.
- The PowerShell replacement then **went wrong twice more before it was right** — `$LASTEXITCODE`
  reads stale after a function, and `-ErrorAction Stop` is discarded by simple functions. Both were
  caught by measurement, and both are left documented in C7b rather than tidied away.

*At this version the charter file is `CLAUDE.md`. Renamed in v1.3.*

---

## v1.1 — unpublished

Second research pass folded in. Added instruction-file provenance and over-application (C1a/C1b), the
factory/product split (C6), heartbeat and absence-of-signal monitoring (C7a/C7b), single-threaded
writes (C12a/C12b), superseded-not-edited decision records, the rebuild drill, and a rubric regrouped
into six scoreable layers. Two claims were **rejected during verification** — see §14 of the Standard.

## v1.0 — unpublished

**No record survives of what v1.0 contained.**

This is stated rather than reconstructed. v1.0 and v1.1 predate publication, have no tag and no
commit, and nobody outside ever held them. Writing a plausible v1.0 entry would be invented history
in a document whose credibility rests on marked, verifiable provenance — so the gap stands, labelled.

The public lineage begins at **v1.2**. Version numbers were carried forward rather than restarted at
1.0 because a reader was already citing v1.2 by rule number when the question arose, and renumbering
a released artifact underneath someone reading it trades a cosmetic tidy for real confusion.

---

[v1.3]: https://github.com/bubomortis/clairvoyance-workspace-starter/releases/tag/v1.3
[v1.2]: https://github.com/bubomortis/clairvoyance-workspace-starter/releases/tag/v1.2
