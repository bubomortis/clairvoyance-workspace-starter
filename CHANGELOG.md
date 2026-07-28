# Changelog

**Audience: human.** Release history for the Clairvoyance Workspace Standard.
**Status:** Free to copy, adapt, and share.

Companion to [STANDARD.md](STANDARD.md) (the canon) and [CITATIONS.md](CITATIONS.md) (the evidence).

Versions are tagged in this repository. Anything marked **breaking for adopters** changes a file you
were previously instructed to create — those are the entries to read if you have already adopted a
version.

---

## [v1.9] — 2026-07-28

### Tightens conformance — two new Charter criteria, C17 and C18

No artifact changes name or location. A v1.8 audit is **incomplete** against v1.9 rather than
invalidated by it: there are two more criteria to score, and both are the kind that tend to come
back `no` the first time they are asked.

### Added — C17, run at the lowest privilege that achieves the goal

- **The Charter hardened elevated processes (C15) without ever asking whether they needed to be
  elevated.** C17 supplies the prior question. Removing an elevation deletes a class of exposure;
  hardening narrows one path through it. C15 now points here before it applies.
- **The transferable failure is not "least privilege" — it is that a privilege outlives its
  justification and nothing re-checks it.** The recorded instance ran `RunLevel=Highest` for one
  day's worth of reason and kept it for fifteen, because the change that ended the reason had no
  idea the elevation existed. So the rule's obligation is to **record what each elevation is for,
  next to the elevation**, and to grep for what a superseded reason was used to *justify*.
- **New trap: reducing privilege can strip your ability to reverse what you did while you held
  it.** The same incident's `icacls /restore` failed after de-elevation, and the
  detached-scheduled-task workaround failed with it, because registering an elevated task also
  needs elevation.
- Externally grounded rather than argued from one instance: Saltzer & Schroeder 1975 for the
  principle, NIST SP 800-53r5 **AC-6** for its application to processes. See CITATIONS.md.

### Added — C18, alternatives are priced together, before either is applied

- **The first criterion in this Standard that governs how Staff propose a control, rather than what
  the Workspace contains** — scored, as always, on the artifact it leaves behind (R35, a decision
  record). Where two controls each close the same exposure they are alternatives, and the choice
  belongs to the owner, which requires both to be priced *before* either is applied.
- **The tell it names:** *"now that X is in place, Y is unnecessary"*, when you would have said the
  reverse had the order gone the other way. Whichever change lands first retroactively becomes the
  argument against the other, so the ratchet turns only toward more change.
- **A mitigation may not be presented as a prerequisite for a fix the owner already chose** unless
  the technical dependency can be stated. *Necessary* converts a preference into a mandate, and
  nobody audits a prerequisite — so an owner who agrees to an optional change believing it was
  mandatory has complied rather than chosen. The criterion is aimed at the **unsubstantiated** claim
  of necessity; where a change genuinely is required, saying so plainly is what the rule wants.
- **Owner resistance is reclassified as a cost signal, not an obstacle.** Herley 2009 (rejection of
  security advice is *"entirely rational"* when its indirect costs exceed the harm prevented) and
  Beautement et al. 2008 (compliance is *"a finite resource"*) are what move this from etiquette to
  economics. On negative affect the obligation is to **stop advocating**, enumerate the root cause
  and every way of addressing it, and hand the decision back — most of all in security exchanges,
  where anxiety collapses *"here is an option"* into *"you must"*.
- **C18 says explicitly that the owner can be wrong, and gives that case a procedure** rather than
  leaving it to be inferred: **one full round** — the situation stated completely, the consequences
  of the choice, what you recommend instead, and what would change your own assessment — then the
  decision is the owner's, recorded with your dissent, and you proceed. **The obligations are
  explicitly ordered** — the round comes first and carries your recommendation; *stop advocating* and
  *assume a reason you cannot see* govern conduct only after it has been delivered and answered, so
  an owner who is both irritated and mistaken is owed the round rather than spared it.
  **The round must be received and answered to count**: aviation and healthcare's two-challenge rule
  triggers its first stage *"if your initial assertion is ignored"*, and pressing for an answer you
  never got is not a campaign. Re-opening a decision the owner actually made is.
  **The bound stops at one round because of where authority sits, not because persistence is
  improper** — both AHRQ's second stage (*"move up the chain of command"*) and the ACM Code's
  whistleblowing clause prescribe escalation, and both presume a chain above the person who decided.
  A Workspace has none: NIST's RMF holds that the authorizing official *"is the only person who can
  accept risk"*, and here that is the owner. Where such a chain does exist, those sources apply and
  this bound does not. The rule also instructs you to **assume a reason you cannot see** — a choice that
  is wrong in general can be correct for the situation actually in hand, and recorded dissent is
  what lets you defer without needing the owner to justify themselves. **One boundary:** where the
  consequence lands on someone who cannot consent for themselves, it is not solely the owner's risk
  to accept.
- Both rules discharge through SOP-3 decision records, which every class bound by the Charter
  already has in scope — so §1's class-scope check produced no widening. Recorded per §1's standing
  instruction to run that check whenever a Charter criterion is added.

### Added — two rubric criteria, so the new rules are scoreable rather than decorative

- **T6 (tooling layer)** — every elevation **records what it is for**, next to the elevation, and
  the stated reason is still live. Class: *All that run anything elevated*. Expect this to score
  `no` on first pass almost everywhere; almost nothing records why it is elevated.
- **R35 (decision & rationale layer)** — where alternatives each closed the same problem, the entry
  shows they were **priced together before any was applied**, records the owner's choice, and where
  Staff disagreed carries the **dissent alongside the decision**. Class: *All*.
  ⚠️ **R35 scores the proposal, not the outcome.** A decision that landed on the right control still
  fails if the alternatives were surfaced one at a time. Appended as R35 rather than inserted beside
  R9 where it thematically belongs — **renumbering would invalidate every existing audit record.**

### Added — three anti-patterns

**Stale privilege** (C17), **Alternatives ratcheted** (C18), **Unearned prerequisite** (C18).

### Fixed during pre-tag review — two citations were used against their own sources

Recorded rather than quietly corrected, because this file's premise is checkability.

- **The ACM Code no longer supports the one-round bound, and an earlier draft said it supplied
  "both halves" of it.** It does not. The sentence *preceding* the "capricious or misguided" line
  licenses whistleblowing when leaders decline to act, and the sentence *following* it prescribes
  careful assessment — so the Code's limit is on the **groundedness** of a report, not its
  **frequency**. Quoting it for a count argued from a passage measuring quality of basis: the same
  error as the C1a/R5 authorship-from-tuning overread this project already carries. The gloss
  *"repetition is not diligence"* is **gone**; the underlying norm — that repetition converts a
  concern into pressure — is kept, restated in the Standard's own voice and **explicitly marked as
  this Standard's claim rather than the ACM's**, with a note not to cite the Code for a count.
- **AHRQ's two-challenge rule governs C18's case after all.** Its second stage triggers on the
  **outcome** — *"if the outcome is still not acceptable… move up the chain of command"* — which is
  *heard and overruled*, exactly C18's situation, and it prescribes escalation. An earlier draft
  claimed *"C18 governs the second; this rule governs the first"*, and its scope note told readers to
  rely on that trigger distinction and to **avoid** the domain argument. That was backwards: the
  domain argument is the one that survives, because it travels with the chain-of-command apparatus
  the rule presumes and a Workspace lacks.
- **§1's standing check gains a second half — ranges and counts.** Four consecutive releases have
  shipped a stale enumeration; this one shipped `T1–T5` in the clause that scopes Base Workspaces
  into the tooling layer, which would have let a Base with an elevated task cite it to skip T6. A
  stale range is normative, not cosmetic.

---

## [v1.8] — 2026-07-28

### Tightens conformance — re-check every standing `?`

No artifact you created changes name or location, and the headline change **removes** a failing
score. But this is still a minor release and not a patch, for the reason the standing rule names:
**the obligation that replaces the decay can fail a Workspace that passed under v1.7.** Anyone who
has been quietly letting a `?` ride now owes a tracked, dated, owned item for it. Relief in the
scoring, a new bar in the obligation — and the bar is the part that decides the release number.

### Fixed — `?` escalates; it does not decay to `no`

- **A `?` that survives two audits now escalates to the owner.** v1.5's decay rule contradicted
  unchanged v1.2 text sitting three lines above it in §11 — *"scoring it `no` for lack of evidence
  manufactures a gap that is not there"* — and then did exactly that. It also converted an
  assessment fact into a Workspace fact, which the same v1.5 passage insists `?` categorically is
  not: *"a fact about the audit and not about the thing audited."* **Two audits failing to obtain
  evidence establishes that the audit is not getting done. It establishes nothing about the
  Workspace**, and a decayed `no` sends remediation after a gap that may not exist. What failed is
  the process, so the escalation is aimed at the process.
- **The pressure the decay applied is preserved, and given a bar.** This was the risk in the
  change: drop the decay without teeth and `?` becomes a permanent parking space again, which is
  worse than the defect because it looks resolved. So the escalation is held to the same kind of
  bar v1.5 gave `blocked` and `accepted`, and owes **three** things — a **tracked, dated item with
  a named owner** that the rubric row references (a third party can open the tracker and check it
  without asking the auditor, which is the observability test met by an artifact rather than by a
  sentence); a statement of **what will be different this time**, because the same person and the
  same approach is what already failed twice; and **the owner's sight of it**, since the remaining
  remedies — funding, access, changing who audits — are nobody else's to authorise.
  ⚠️ **An escalation is an obligation, not an adjective.** *"Escalated"* in a cell with nothing
  owed reads as though someone is handling it, and suppresses the investigation the word exists to
  trigger. That is C7's mechanism one level up, and it is the way this fix would have failed.
- **And escalation terminates.** It resolves to one of the six when the evidence arrives, or — if
  the owner concludes the evidence cannot be obtained here, which is itself a finding — to
  `blocked` or `accepted` with their own bars. It must never sit as `?` with a new adjective.

### Added — the audit record, so the rule is checkable

- **`docs/AUDITS.md` joins §3's artifact table**, on §3's own trigger logic rather than
  unconditionally: *a second audit is going to happen*. Written at the close of the **first** one,
  because the second cannot carry `?` rows forward from a record that does not exist; a Workspace
  audited once and never again does not need it. It may live in your tracker instead — what
  matters is that audits are **dated and kept**, not where.
- **A `?`'s age counts from the first audit that recorded it.** An audit nobody wrote down does
  not start the clock, and backdating one is a green-signal lie about your own compliance (C7).
  *"Survives two audits"* was not checkable from the Workspace before this — §3 had no row for an
  audit record and nothing required audits be dated or retained — which was the same class of
  defect as the rule it replaces.

**Both halves of this were carried as *known, unfixed* in v1.7** and are now closed. The v1.7
entry below is left as it stood; it was accurate when it shipped.

**Deliberately not added: a rubric criterion for the audit record.** R8 covers the decision record
and R17 the work ledger, so the symmetry is tempting — but adding one would change the criterion
count and the scoring surface in a release scoped to a single defect. Recorded here so it reads as
a decision rather than an oversight.

### Known, unfixed

Unchanged from v1.7 except where closed above: the v1.3 banner path, the Engineer persona's
two routes, the T-block's citation of §1's *"plus"* clause, C13's headline against T1, the
Engineer's hash-before-install check, `blocked`'s domain in a solo Workspace, C1a/R5's
authorship-vs-tuning overreach, and the cosmetic set.

- **New:** T1 scores byte-identity, which is a *proxy* for "this duplicate is redundant" and
  fails in **both** directions — a **stale** duplicate is more dangerous than an identical one,
  because if anything resolves it you get a silent version split rather than a no-op. Demonstrated
  live: upgrading `rclone` moved the `PATH` copy to 1.74.4 while a vendored 1.74.3 remained, and
  **T1 flipped from fail to pass with nothing fixed.** The proposed replacement tests whether the
  copy is *referenced* (in code and docs) and whether an equivalent is reachable on `PATH`, with
  byte-identity demoted to a confirmation that deleting is safe — never a gate saying it is not.
  Not in this release: it changes what T1 measures and earns its own adversarial read.

---

## [v1.7] — 2026-07-28

### Tightens conformance — re-score C14 exceptions and `accepted` verdicts

No artifact you created changes name or location. **But an audit that passed under v1.6 may not
pass now**, which is why this is a minor release and not a patch: **four** things that passed
before now fail — a C14 exception built from the v1.6 Engineer persona, an `accepted` with a
judgement-shaped trigger, an `accepted` the owner never confirmed, and a half-measure previously
exempted by C16 on the strength of a planned fix. A patch number would tell adopters the opposite
of the truth.

**This release is a remediation.** v1.4–v1.6 were written and tagged in one evening; an
independent adversarial review of that delta found four blocking defects and returned *not safe to
adopt as-is*. All four are fixed here, along with the two non-blocking findings that share their
root cause. **Every one of the four sat in a rule's remedy, exception or propagated copy — none in
a prohibition.** That is the permissive-half shape this Standard names twice (SOP-7 §11, C14), and
the release process reproduced it three times in one evening on its own newest text. Recorded here
rather than quietly fixed, because the pattern is the finding.

### Fixed — the exception that swallowed its own criterion

- **C16's escape clause no longer exempts anyone on the strength of an intention.** It read: *if
  full implementation is genuinely on the table, this criterion does not apply to you.* C16's
  target population is people who installed half a control — a population that almost universally
  believes full implementation is on the table, because that belief is why they stopped halfway
  rather than declining. The clause handed them an exemption keyed on intent, with no test, one
  release after v1.5 established at length that intent-shaped conditions are exactly the ones that
  mean nothing. It also nullified the operative remedy directly above it (*if the half-measure is
  already installed, remove it*).
  **Now:** *on the table* means owned, scheduled and dated by a named person — the same bar as a
  `blocked` unblocker — **and the criterion still applies until the fix lands.** The exemption
  became a priority instruction, which is what it was always trying to be: price the full
  implementation first, and take the half-measure out in the meantime.

### Fixed — `accepted` lost its bar on the way into the derived documents

- **`accepted`'s re-raise condition now carries the third-party-observable test everywhere.**
  `STANDARD.md` §11 declares the `accepted` and `blocked` bars *identical*. Both derived documents
  carried `blocked`'s verbatim — including v1.5's who-must-act half — and dropped `accepted`'s
  entirely. The weaker copy landed on the **self-exemption** verdict, the one that lets a Workspace
  decline a criterion outright, so Staff working from either document would accept *"revisit if
  circumstances change"* — which the Standard itself names as the *designed-around risk*
  anti-pattern. Fixed in `IMPLEMENTATION.md` §3 and, structurally, in both personas (below).
- **`IMPLEMENTATION.md` §1 gains a fourth human decision: confirm anything marked `accepted`.**
  The human's job listed a `blocked` counterpart and no `accepted` one, so a Staff member could
  self-issue a decline that never surfaced to the owner — while the Standard says of `accepted`
  that *the owner has priced it*. If nobody showed the owner the price, it was not priced.

### Fixed — a Base Workspace could not satisfy C14's exception

- **§1's class table no longer scopes a class narrower than the Charter it admits.** The Base row
  read *Charter + SOPs 3–5 only*. The Charter is now C1–C16, so a Base Workspace is bound by C14 —
  but C14's exception condition 3 discharges in the tools manifest, defined in SOP-7, which is §10.
  The artifact that satisfies the condition was out of scope for the class the criterion binds, so
  **C14 was absolute for every Base Workspace** — precisely the state its exception exists to
  prevent, and the state C14's own text says teaches readers a rule is aspirational.
  **Now:** the row reads *plus any SOP section a Charter criterion in scope depends on*, stated as
  a general rule rather than a patch for SOP-7, with the recurrence check written down: when you
  add a Charter criterion, ask whether every class bound by it has access to what discharges it.
- **T1–T5 gain the Class column every other rubric criterion has.** They shipped in v1.4 as a
  headerless bullet list between two rules, while §14 routes class-inapplicability *through* that
  column — so a Workspace with no external tools had nowhere to record that and was sent to write
  decision entries for criteria that do not apply to it. The new table also states that a Base
  Workspace is in scope on the same terms as any other class, and that structural inapplicability
  goes in the column, never through `accepted`.
  **T4 is `All`, and deliberately so** — caught by the re-review of this release, in the fix
  itself. Scoping the manifest criterion by whether the Workspace carries external tools gates it
  on the self-assessment Mode C is *defined* by getting wrong: a Workspace whose author believes
  it uses none marks `n-a`, and the criterion that would have surfaced the tool never runs. The
  host application's bundled tools are also present in every Workspace, so T4's population is
  never empty. **Correctly removing manufactured noise for tool-free Workspaces manufactured a
  blind spot on the one criterion that must not be scoped by what the author already knows** —
  a different failure from the permissive halves above, and worth recording as its own shape.

### Fixed — two personas from the same release disagreed on the rule the release existed to propagate

- **The Engineer persona taught a two-of-four C14 exception.** Its new *External tools* section
  described conditions 1 and 3 and omitted 2 (*do not treat this as a pattern to copy* — the
  condition that stops the exception propagating) and 4 (*its absence fails loudly and by name*).
  T2 is unambiguous that an exception missing **any** of the four is a fail, so an Engineer
  following the persona faithfully built an exception the Architect auditing the same Workspace
  would fail. Not a drift risk: wrong on the day it shipped.
  **Now:** the bullet routes to C14 for the enumeration, states that all four must hold, and keeps
  only the two that are genuinely the code author's — the proof recorded as the runnable test that
  cancels the exception, and absence failing loudly and by name. Those two fire on opposite events
  and the previous text conflated them.

### Fixed — the root cause of both propagation defects

- **The verdict set now has an authored home in the agent-facing chain.** `IMPLEMENTATION.md` §2's
  Card shape had no verdicts section at all, so when v1.5 and v1.6 needed to propagate the verdict
  semantics they had nowhere to route and copied instead — into a persona whose own second line
  says *read it; do not restate it*. C5 predicts the rest: any rule stated twice will diverge, and
  the only question is when. The answer here was *at ship* — two of the four blockers above are
  that divergence, present in the tag.
  **Now:** `## Verdicts and their obligations` is a required Card section, carrying all seven
  tokens and, for the four with an obligation, the obligation *and its quality bar*. Both persona
  blocks are reduced to a route plus what is genuinely persona-specific: for the Architect, that
  filling the field does not discharge the obligation and that `accepted` is not theirs to issue
  alone; for the Engineer, the two conditions that are implemented in code. **This removes the
  divergence class rather than patching its two instances** — which is why it shipped with the
  blockers rather than after them.

### Fixed — three unmarked local extensions

- **SOP-3's `Revisit if:` and SOP-7 §2's manifest claim now carry provenance notes**, and §15's
  list is extended from two claims to five. The Standard's headline virtue is that it marks the
  claims it cannot source; these were the two it did not, and they are load-bearing — v1.5 built
  its entire conformance tightening on the third-party-observable test and v1.6 propagated it into
  two personas, all on an unlabelled extension. `CITATIONS.md` §1a is blunt about both: SP 800-137
  *does not* support the third-party-observable test, and RA-7 requires a justification **and
  nothing further** — no revisit condition, no review date, no trigger.
  This also makes v1.4's *Evidence* sentence true. It claimed three local extensions were *marked
  as such*; only C16's was.

### Known, unfixed

Carried deliberately, to keep this diff small enough to review exactly. Each is real:

- **`?`'s decay to `no` contradicts unchanged §11 text three lines above it** — which says scoring
  `no` for lack of evidence *manufactures a gap that is not there* — and converts an assessment
  fact into a Workspace fact, which the same passage insists `?` categorically is not. It is also
  not checkable from the Workspace: *"survives two audits"* and *"carry it forward with its age"*
  need an audit-history artifact, and §3's table has no row for one. **This needs a decision about
  what `?` decays *to*, not an edit.**
- **The upgrade banner still has no v1.3 path.** v1.3 is the last version published and adopted
  before v1.4–v1.6 landed together, so the most likely upgrader is the one it does not address.
  v1.4's entry also never tells a reader to re-check an audit, despite adding nine new things to
  score. **The banner was rewritten in this release, which was the free moment to add it** — the
  cost of fixing it goes up from here.
- **The Engineer persona routes to two different places**, and the Card — the sanctioned target —
  can legitimately omit C14's four conditions, because they were not given the do-not-compress
  protection the verdicts section just got. It fails loudly rather than silently (the bullet
  states the count, so an Engineer who cannot find the other two knows to ask), which is why it
  is not blocking. The fix is one more line in `IMPLEMENTATION.md` §2.
- **The T-block cites §1's "plus" clause for something that clause does not say.** The plus clause
  admits *SOP sections a Charter criterion depends on*; T1–T5 are rubric criteria, so what
  actually puts a Base in scope is the new Class column itself. The fix touches §1's scope
  strings, and a structural edit there earns its own adversarial read rather than riding along.
- **C13's headline is broader than T1.** C13 says *a tool the machine already has*; T1 says
  *byte-identical to one already on `PATH`*. A deliberately pinned build — SOP-7 §9's own worked
  example of a legitimate pin — violates the first and passes the second.
- **The Engineer's *resolve, do not vendor* check cannot be executed as written.** It says check
  by hash, not by name and version; you cannot hash a copy you have not obtained yet.
- **v1.5's externality test narrows `blocked`'s domain in a solo Workspace** — where the actor is
  you by default — and is disclosed as a wording bar rather than as a narrowing.
- **C1a/R5's authorship-vs-tuning overreach**, open since v1.3 and now four releases old.
- Cosmetic: the three newest CHANGELOG headings are undefined reference links, `STANDARD.md` has a
  doubled *SOP-7 SOP-7 §5* token and four doubled horizontal rules, and `CITATIONS.md`'s scope line
  still says *SOP-1 through SOP-6*.

---

## [v1.6] — 2026-07-27

### Propagation only — no normative text changed

**`STANDARD.md`'s rules are identical to v1.5.** The version number moves so that the document and
the tag agree; if you have already read v1.5, there is nothing new in the Standard itself.

What changed is the two personas, which had not kept up:

- **Workspace Architect** taught the verdict set as it stood before v1.5 — `?` with no owner, no age
  and no decay, and no mention of `accepted` or the unblocker bar at all. It now carries all three
  verdicts with their obligations, and the warning that `?` is not available for a criterion you
  find inconvenient to evaluate.
- **Clairvoyance Engineer** was last revised at v1.2 and said nothing about external tools, despite
  C13–C15 and SOP-7 being squarely engineering remit. It gains a section: resolve rather than vendor,
  never reach into a neighbouring project's private directory, and the rule that matters most —
  **elevated code resolves by absolute path, and an absolute path into a writable directory is
  equally exploitable**, including the POSIX case where the parent chain is stricter rather than
  weaker.

**Why a release for this.** A verdict nobody is taught to use does not exist, and a persona that
teaches the previous rule set actively contradicts the current one. Shipping rules without the
documents that propagate them is *mechanism without norm* — an anti-pattern this Standard lists.
v1.5 fixed that for `IMPLEMENTATION.md` and the Architect runbook and missed the personas.

---

## [v1.5] — 2026-07-27

### Tightens conformance — re-check existing audits

No artifact you created changes name or location. **But an audit that passed under v1.4 may not pass
now**, which is why this is a minor release and not a patch.

- **`blocked`'s unblocker now has a quality bar.** It already had to be stated; it now has to be
  *checkable*. Name something a third party could notice without asking you — and **name who or what
  has to act. If the actor is you, the criterion is not blocked**, however precisely you can date the
  milestone. *"When we have time"* and *"when we finish the consolidation"* both fail, for different
  reasons: the first is vacuous, the second is internal.
  A vacuous unblocker means the verdict is wrong or the external condition has not been found yet —
  and that follows from the definition rather than from any claim about behaviour. `blocked` asserts
  something outside your control defeats the criterion, so if it genuinely does, an external
  unblocker exists by construction.
- **`?` is defined.** It has appeared in the rubric since v1.0, uncounted and undefined. It is **not
  a verdict about the Workspace** — it records that the *auditor* could not determine the state, which
  is a fact about the audit. It now carries three obligations: it names **who will obtain** the
  evidence, unresolved rows are **carried forward with their age**, and **a `?` surviving two audits
  becomes a `no`** — the evidence was obtainable by definition and nobody obtained it.
  The decay path is the load-bearing part. An unblocker and a re-raise condition are *event-driven*
  and trip on their own; an evidence statement is *actor-driven* and never executes without an owner.
  Without decay, a well-worded `?` sits across audits indefinitely with every obligation formally
  satisfied — which is how it would have become the cheapest exit in the rubric.

### Derived documents ship with it

- **`IMPLEMENTATION.md`** taught the derivation with `?` and `blocked` and **did not know `accepted`
  existed.** Shipping a verdict without the instruction that propagates it is *mechanism without
  norm*, which this Standard lists as an anti-pattern. It now teaches all three, with their bars.
- **The Architect build runbook's flex check** counted `n-a` only. It now counts `accepted` too, and
  notes that `accepted` is the stronger signal of the two: `n-a` says a criterion did not apply,
  `accepted` says someone priced one and declined it.

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
