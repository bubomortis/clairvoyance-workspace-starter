# Changelog

**Audience: human.** Release history for the Clairvoyance Workspace Standard.
**Status:** Free to copy, adapt, and share.

Companion to [STANDARD.md](STANDARD.md) (the canon) and [CITATIONS.md](CITATIONS.md) (the evidence).

Versions are tagged in this repository. Anything marked **breaking for adopters** changes a file you
were previously instructed to create — those are the entries to read if you have already adopted a
version.

---

## [v1.4] — 2026-07-27

### Not breaking for adopters

**Nothing you already created needs renaming.** This release adds sections, four Charter criteria and
one rubric verdict. If you adopted v1.3, no file on disk changes name or location.

**But section numbers after SOP-6 shifted by one**, because SOP-7 is inserted as §10. If you quote
the Standard by section number anywhere, re-check: Rubric §10→§11, Anti-patterns §11→§12, Adoption
§12→§13, When to ignore §13→§14, What was rejected §14→§15, Appendix §15→§16.

### Added — external tools

- **C13 — Tools are resolved, not vendored.** A Workspace should not carry a copy of a tool the
  machine already has. Measured: two Workspaces vendored four tools that were byte-identical by
  SHA-256 to copies already on `PATH`, created *after* them.
- **C14 — Never resolve a binary through another Workspace's private directory**, with a four-part
  self-closing exception for the case where a tool is genuinely unreachable any other way. The
  exception exists because a rule with no legitimate path for the real case gets ignored rather than
  followed. **The routing-index form of this failure is worse than the code form** — a documentation
  route is a *generator*, producing the failure on a schedule for every future author.
- **C15 — Anything running elevated resolves binaries by absolute path, never by `PATH`** — and an
  absolute path is *necessary but not sufficient*, because a path into a user-writable directory is
  equally exploitable. **Stated for Windows and POSIX**, where one clause inverts rather than
  translating: POSIX directory write authorises `unlink`/`rename` of any entry regardless of that
  entry's own mode or owner, so a correctly hardened binary under a loose parent can still be
  replaced.
- **§10 — SOP-7, Standing up shared external tools.** Discovery failure modes, manifest design,
  backup siting, upgrade consent, and why a shared directory alone does not fix discovery.
- **T1–T5**, five external-tool audit criteria.

### Added — declining a rule

- **C16 — A control you will not maintain is worse than one you declined.** C7's mechanism one level
  up: a control *believed* to be in place suppresses investigation of that exposure exactly as a
  false green signal does.
- **A sixth rubric verdict, `accepted`** — needed here, understood, deliberately not done. Distinct
  from `n-a` (no failure mode exists) and `blocked` (defeated by something outside your control).
  Every `accepted` carries its re-raise condition.
- **SOP-3's decision template gains `Revisit if:`**, mandatory on a decline. A re-raise condition
  must name an event a third party could notice without asking you; if checking whether it fired
  requires your judgement, it is not a trigger.
- **§14 now says a decline is a decision and gets recorded like one** — scoped to controls you
  considered and rejected. A backlog is not a decline.
- **Eleven anti-patterns**, including *designed-around risk*: an accepted exposure that later work
  quietly routes around, so the trigger never fires. §12's header now reads *"All observed in
  production **except where marked**"* — that row is marked, because it is argued rather than
  observed.

### Evidence

First release where the new material was **checked against external sources after drafting** rather
than reconstructed afterwards. Every source in [CITATIONS.md](CITATIONS.md) §1a was opened and read.
Eleven citations survived; seven leads were rejected, including one dead link, one paywalled standard
cited at the wrong edition, and one citation that resolved but described an adjacent problem — that
last agreed on by both models consulted. **The rejections are recorded alongside the citations.**

Three claims are labelled as having **no external basis**: that a manifest improves discovery, that a
re-raise condition should be third-party observable, and the ranking in C16. They are local
extensions, marked as such.

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
- **§15 — runtime auto-load filenames** *(renumbered to §16 in v1.4)*. Which runtimes load which file, with a confidence mark per
  entry. Deliberately **non-normative and outside the artifact table**: by C1b a named file is a file
  agents will create, so a vendor roster in normative text would produce Workspaces holding six
  charter files for one runtime — this document committing the failure it documents. It is safe in
  that appendix because `STANDARD.md` is `Audience: human` and agents do not read it, which is also why it
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
into six scoreable layers. Two claims were **rejected during verification** — see §14 of the Standard *(§15 from v1.4 onward)*.

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
