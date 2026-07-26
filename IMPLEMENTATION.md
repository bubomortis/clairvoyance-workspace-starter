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

**Your job is three decisions**, none of which require reading the Standard:

- Approve, trim, or reject items on the plan — individually, not wholesale.
- Say when something they flagged as `blocked` is worth unblocking.
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
## Artifact triggers — create X when Y is already true
## Criteria, by layer — with anything excluded here marked and why
## When not to apply this
```

**Then route it.** Add a line to this Workspace's `library.md`:
`- IF designing, auditing or building a Workspace → read [[Workspace Criteria Card]]`
An unrouted card is invisible, and you will not find it next session.

**Then stop and show the human the card**, with a one-paragraph summary of what you dropped and
why. Do not begin changing Workspaces in the same turn.

### The honest caveat on this step

The Standard's own C1a says **generated guidance measured worse than hand-authored guidance**, and a
Criteria Card is derived rather than hand-written. That tension is real and you should not pretend
otherwise.

Three things make it defensible: you are **compressing a hand-authored source**, not inventing
guidance from scratch; the card is a **checklist and index**, not a persona or instruction file; and
C1a's own resolution is that *tuned* guidance beat both generated and unguided baselines. So the
card is only sound if you actually tune it — see §5. **A card derived once and never revised is the
exact artifact C1a warns about.**

---

## 3. Staff: first application

Pick one Workspace. Do **not** apply the card everywhere at once.

1. **Classify it.** Say which class and why. The class decides what is even in scope.
2. **Score it** against the card, by layer. Mark `?` for anything you cannot evidence, and say what
   would settle it. Mark `blocked` for anything needed but impossible here — with what would unblock it.
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
- **Do not auto-generate instruction files** (`AGENTS.md`, `library.md`) from a template. Hand-author
  them. This is the one place the research is unambiguous.
- **Do not report success you have not verified** by opening the file and reading it.
- **Do not apply this to a scratch or two-day Workspace.** Say it does not need it.

---

## 5. Staff: tune the card

**This is what makes the card legitimate rather than a compression artifact.**

When something goes wrong in a Workspace — a criterion you scored `yes` that turned out hollow, a
recommendation that wasted the user's time, a gap the card did not catch — **revise the card and
note what changed it.** Tuning against observed failure is the difference between the guidance that
measured best and the guidance that measured worse than nothing.

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
