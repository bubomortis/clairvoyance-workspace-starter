# Implementation Runbook — Putting the Workspace Standard to Work

**Audience: both.** §1 is for you. §2 onward is written to be executed by a Staff member.
**Status:** Free to copy, adapt, and share.

**You do not need to read the Standard to use it.** The Standard is a long, argued document meant
for someone deciding whether to adopt a rule. This runbook is the short path: hand it to a Staff
member, and they will read the Standard, derive a compact working copy tuned to *your* setup, and
apply it. You stay in the approval seat, not the study seat.

**Companions:** [Workspace Standard](STANDARD.md) (the canon, human-facing) ·
[Workspace Architect Build Runbook](runbooks/architect-build-runbook.md) (a Staff member built for this work) ·
[Clairvoyance Engineer Build Runbook](runbooks/engineer-build-runbook.md) (builds what runs inside a Workspace)

---

## 1. For the human — what you are about to get

Point any capable Staff member at this runbook. They will produce **two things**:

1. **A Criteria Card** — a compact, checkable working copy of the Standard, tuned to your instance
   and stripped of the argument. This is what your Staff will actually use going forward. Expect one
   to two pages, not thirty.
2. **A plan** — what they propose changing in a given Workspace, with the cost of each item, and an
   explicit list of what they are *not* recommending.

**Your job is four decisions**, none of which require reading the Standard:

- Approve, trim, or reject items on the plan — individually, not wholesale.
- Say when something they flagged as `blocked` is worth unblocking.
- **Confirm anything they marked `accepted`.** That verdict declines a criterion outright and
  leaves the gap open on purpose. It is a risk *you* are taking, not one they can take on your
  behalf — and the Standard's own wording for it is that *the owner has priced it*. If nobody
  showed you the price, it was not priced.
- Tell them when they are over-engineering. *"That feels like more than this needs"* is legitimate
  and sufficient feedback; the Standard explicitly agrees with you by default.

**The one thing worth knowing before you start.** The Standard's own strongest finding is that
**most Workspaces need a minority of its criteria.** If a Staff member comes back recommending
everything, they have misapplied it — that is the documented failure mode, not thoroughness. A good
plan tells you what it is skipping and why.

**Cost:** one Staff session to produce the Criteria Card, then it is reused. Re-derive only when the
Standard changes materially.

---

## 2. Staff: derive the Criteria Card

> Everything below is addressed to the Staff member executing this.

**First, find out what is already here. Do not skip this and do not assume the name.**

A Criteria Card is a *derived* artifact, and C1a's actual resolution is that **tuned** guidance beat
both generated *and* unguided baselines — tuning against observed failure is what separates guidance
that works from guidance that does not. **So workspace guidance genuinely in use here — followed,
and revised at least once because something went wrong — carries a tuning premium your fresh card
cannot have yet.** Replacing that silently is the precise substitution this Standard warns against,
performed in the name of adopting this Standard.

**This premium is earned, not automatic.** A stub, a template nobody followed, or a file last
touched the day it was created carries none of it — score the contents, never the existence, exactly
as you would in an audit. Establish which you are looking at *before* you weigh it.

Search for existing guidance under **any** name:

- a note or file serving as criteria, workspace standard, house rules, conventions, or an SOP
- an earlier, adapted, renamed or partially-edited copy of this Standard
- governance already encoded in `library.md`, `AGENTS.md`, or the equivalent entry-point file
- per-Workspace conventions living in a README, a decision record, or a pinned note

**If you find nothing:** say so explicitly, then derive the Card as below.

**If you find something — STOP. Do not merge, refine, update, or overwrite it.** Report to the
human in plain language:

- what you found, and where
- whether it appears to *descend* from this Standard (a version or a fork) or to be independent
- where the two **substantively disagree** — the real conflicts, not a diff
- what would be lost by replacing it, naming anything tuned to a failure this instance has had

Then give three options with their costs, and wait:

1. **Keep theirs.** Adopt nothing, or lift individual criteria into their existing artifact.
2. **Merge — additive only.** This Standard supplies what theirs *lacks*. Nothing already in
   theirs is changed, reworded, reordered or removed. **Where the two genuinely contradict, a merge
   cannot resolve it**: leave theirs standing, record the conflict, and put it to the human as its
   own decision. A contradiction is an owner's call, not a merge rule.
3. **Replace.** Only on an explicit instruction. Preserve the old artifact; do not delete it.

**Do not decide this yourself, and do not read enthusiasm for the new Standard as an answer to a
question nobody asked.** An instance with working guidance has already paid for the tuning that
makes guidance work; a stranger's document has not earned the right to overwrite it.

**Read the Standard in full, once.** Yes, all of it, including the sections on when to ignore it.
You are compressing it, and you cannot compress what you have not read. This is the only time the
full read is required.

**Then write a Criteria Card** — a single document, saved as a note in this instance, that is:

- **Checkable, not persuasive.** Every line is something you can score, apply, or check. The
  Standard's evidence, citations, counter-arguments and verification record do not go in. If a line
  does not change what you would *do*, cut it.
- **Scoped to this instance.** Drop criteria that cannot apply here. If there is no automation, the
  automation criteria are not in your card — note them as excluded rather than carrying them.
- **Explicit about the absolutes.** Three things survive compression no matter what: a signal that
  lies is worse than no signal; an empty scaffold is worse than none; score contents, never file
  existence.
- **Explicit about flex.** Carry the *when to ignore this* material. It is the counterweight that
  stops the card becoming a checklist, and a card without it will make you over-recommend.

**Suggested shape** — adapt freely:

```
# Workspace Criteria Card — <instance name>
Derived from: Workspace Standard <version> on <date>

## Absolutes (never relaxed)
## Classify: Project / Pipeline / Base — and what each excludes here
## Verdicts and their obligations
## Artifact triggers — create X when Y is already true
## Criteria, by layer — with anything excluded here marked and why
## When not to apply this
```

**`## Verdicts and their obligations` is not optional, and it is the one section to copy rather
than compress.** It carries all seven tokens — `yes` / `partial` / `no` / `n-a` / `blocked` /
`accepted`, plus `?` — and, for the three that carry an obligation, the obligation *and its
quality bar* — plus the caution on `n-a`, which owes no record but is still a claim you have to
be able to defend. In each case the bar is the whole control:

- **`blocked`** — what would unblock it: something a third party could notice, and **someone
  other than you who has to act**. If the actor is you, it is backlog, not `blocked`.
- **`accepted`** — the re-raise condition, on the same third-party-observable terms, recorded as
  a decision entry and **confirmed by the human**.
- **`?`** — what evidence would settle it, **who will obtain it**, and its age carried forward.
  After two audits it **escalates to the owner** — which is not a `no` and not a label: it owes a
  tracked dated item with a named owner, a statement of what will be different this time, and the
  owner's sight of it. Not available for a criterion you find inconvenient.
- **`n-a`** — a claim that the failure mode does not exist here, which is a claim about the
  Workspace and not about your familiarity with it.

**This section exists so that no other agent-facing document has to restate it.** C5: any rule
stated twice will diverge, and the verdicts are the most-copied rules in the set — the personas
route here rather than carrying their own copy. If you compress a bar out of the Card, you have
not simplified the Card; you have deleted the control from every document downstream of it.

**§3 restates these bars, on purpose, and that is the one exception.** Two reasons, and both are
narrow enough that they do not license a third copy. **C5's harm is divergence a reader cannot
adjudicate**, and §3 states its direction of authority — which converts a competing copy into a
derived one. The two are also **in the same file**: one reader, one pass, and any edit puts both
copies on screen together, so the drift window is near zero. C5's real target is two copies in
two files that no single change ever brings into view. And **they address different acts** — §2
says what to *write into* the Card, §3 says how to *score with it*; reducing §3 to a pointer
sends a reader back up the document mid-procedure, which is the friction that makes people work
from memory instead. **Neither reason survives being moved to two separate files.**

**Then route it.** Add a line to this Workspace's `library.md`:
`- IF designing, auditing or building a Workspace → read [[Workspace Criteria Card]]`
An unrouted card is invisible, and you will not find it next session.

**Then stop and show the human the card**, with a one-paragraph summary of what you dropped and
why. Do not begin changing Workspaces in the same turn.

### The honest caveat on this step

The Standard's own C1a warns against **guidance that has never been tuned against observed
failures**, and a Criteria Card starts life exactly there: derived in one pass, tested against
nothing. That tension is real and you should not pretend otherwise.

Two things make it defensible, and one obligation makes it sound. It is a **compression of a source
that has itself been tuned**, not guidance invented from scratch; and it is a **checklist and
index**, not a persona or instruction file. (Earlier versions listed a third defence — that C1a
resolves to tuning. It is not dropped; it is promoted below, because it is an obligation rather
than a defence.) Neither of the two earns it the 33.0% arm — only tuning does. So the card is only
sound if you actually tune it against what goes wrong here — see §5. **A card derived once and
never revised is the exact artifact C1a warns about.**

Note what does and does not carry weight here. C1a's strongest finding is about **tuning**, not
authorship: an untuned file does not significantly beat having no file at all, however it was
written. So being machine-derived is not by itself the defect — **staying untuned is.** The one
provenance rule C1a does keep is narrow and it applies to you: a card **committed exactly as
generated** is the artifact that measured worst. Derive it, then tune it — that sequence is the
best-performing condition measured, not a compromise.

---

## 3. Staff: first application

Pick one Workspace. Do **not** apply the card everywhere at once.

1. **Classify it.** Say which class and why. The class decides what is even in scope.
2. **Score it** against the card, by layer. The bars below are the Card's *Verdicts and their
   obligations* section applied — that section is where they are authored, and where to change
   them if the Standard moves. Restated here only because this is the step where they bite.
   **If these ever differ from §2, §2 governs — and one of them is wrong.**
   - Mark **`blocked`** for anything needed but impossible here, **with what would unblock it** —
     naming something a third party could notice, and someone other than you who has to act. If
     the unblocker is your own milestone, it is a backlog item, not `blocked`.
   - Mark **`accepted`** for anything needed, understood, and deliberately not done — **with the
     condition that would make you revisit it**, recorded as a decision entry, and **confirmed by
     the human** (§1). The condition is held to the same bar as an unblocker: something a third
     party could notice without asking you. *"When circumstances change"* is not one. An accepted
     criterion with no stated trigger is a `no` wearing better clothes.
   - Mark **`?`** for anything you cannot evidence, saying what would settle it **and who will
     obtain it**. `?` is not a verdict and not terminal: carry it forward with its age, and a `?`
     surviving two audits **escalates to the owner** — it does not become a `no`, because two
     audits failing to get evidence is a fact about the audit, not about the Workspace. Escalating
     owes a tracked dated item with a named owner and a statement of what will be different this
     time; *"escalated"* in a cell with nothing owed reads as though someone is handling it, and
     suppresses the investigation the word is meant to trigger. **Not available for a criterion
     you find inconvenient to evaluate** — unfamiliarity with a platform or a permission model is
     a translation problem, not missing evidence.
3. **Propose**, ranked by benefit-to-effort, each item with its cost.
4. **Name what you are not recommending, and why.** A plan without this section is incomplete.
5. **Stop.** Wait for item-by-item approval. Build only what was approved.

**Start with these three**, in order, unless the Workspace says otherwise:

1. Fill or delete the entry-point router. Minutes; highest return.
2. Start a decision record. The most-missed artifact in every Workspace surveyed.
3. Add a content assertion to the riskiest scheduled job — backups first.

---

## 4. Staff: what not to do

- **Do not create artifacts whose trigger has not fired.** Absence is the correct state, and the
  person least equipped to push back is the one most likely to accept a scaffold they will never use.
- **Do not leave instruction files** (`AGENTS.md`, `library.md`) **at their first draft** — whether
  you generated them from a template or typed them yourself. Tune them against failures you have
  actually seen here. Generating a starting point is not the defect; **committing it exactly as
  generated is**, and that is the one provenance result that reached significance.
- **Do not report success you have not verified** by opening the file and reading it.
- **Do not apply this to a scratch or two-day Workspace.** Say it does not need it.

---

## 5. Staff: tune the card

**This is what makes the card legitimate rather than a compression artifact.**

When something goes wrong in a Workspace — a criterion you scored `yes` that turned out hollow, a
recommendation that wasted the user's time, a gap the card did not catch — **revise the card and
note what changed it.** Tuning against observed failure is what separated the guidance that measured
best (33.0%) from the untuned baselines, which sat close together and untested against each other
(28.3% static, 25.5% no guidance at all).

Re-derive from the Standard only when the Standard itself changes. Otherwise, refine in place.

---

## 6. The prompt to paste

For a human who wants to start immediately. Point a Staff member at the repository or the notes,
then send this:

```text
Read the Workspace Standard in full, then produce a Criteria Card for this instance following
the Implementation Runbook §2 — compact, checkable, scoped to what applies here, keeping the
absolutes and the flex guidance. Save it as a note and route it from library.md.

Then stop. Show me the card and tell me in one paragraph what you dropped and why.

Do not change any Workspace yet. When I approve the card, I will pick a Workspace and you will
score it and propose — with the cost of each item, and an explicit list of what you are NOT
recommending. I will approve item by item.
```

**How to tell it worked:** the card is shorter than the Standard by a large factor, it names things
it deliberately excluded, and the first plan you get back contains at least one *"not applicable
here."* If everything scored as a gap to close, the flex guidance did not survive compression —
send it back.

---

*Free to copy and adapt. The Standard is the canon; this is the on-ramp.*
