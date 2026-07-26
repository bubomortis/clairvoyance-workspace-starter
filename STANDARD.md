# The Clairvoyance Workspace Standard

**Version:** 1.3 · **Status:** Free to copy, adapt, and share.
**Audience: human.** This document exists to be understood, argued with, and updated as the subject
matures. It is deliberately heavy on evidence, counter-evidence and rationale — the parts a person
needs to decide whether to adopt a rule, and the parts an agent does not benefit from (C1).

**If you want Staff to *implement* this rather than read it**, do not point them here. Point them at
[Implementation Runbook](IMPLEMENTATION.md), which has them derive a compact working copy tuned
to your instance. You should not have to study this document to benefit from it.

*v1.3 — **the charter file is now `AGENTS.md`, not `CLAUDE.md`.** A Workspace charter file should not be
named after one model vendor, and `AGENTS.md` is a published open format with broad multi-vendor
adoption. **This renames an artifact named throughout v1.2 — if you adopted v1.2, this is the one
change that touches files you already created.** SOP-1 step 4 gains the runtime auto-load rule:
`AGENTS.md` is canonical, add a vendor-named pointer file only if your runtime auto-loads a
different name, and that pointer may add but never restate. New §15 records which runtimes load
which filename, deliberately **non-normative and outside the artifact table** — a roster of vendor
filenames in normative text would produce Workspaces holding six charter files for one runtime, which is
C1b's over-application failure committed by this document about itself. Also new: `CITATIONS.md`,
the source list behind the Standard, with per-entry confidence and the claims that have no external
citation.*

*v1.2 — C7b corrected: the success-signal example chained to an exit code, reproducing the failure
C7 forbids. Now three terms (work → assert → signal), with a portable-shell note: `&&` is a parse
error in Windows PowerShell 5.1. R25 restated shell-agnostically — it named an operator the default
Windows shell cannot parse, so a correct Windows Workspace failed the criterion by construction.
Found in review and independently reproduced before the ruling. The PowerShell replacement then
went wrong twice more before it was right — `$LASTEXITCODE` reads stale after a function, and
`-ErrorAction Stop` is discarded by simple functions — both caught by measurement, both left
documented in C7b rather than tidied away.*

*v1.1 — second research pass folded in. Added: instruction-file provenance and over-application
(C1a/C1b), the factory/product split (C6), heartbeat and absence-of-signal monitoring (C7a/C7b),
single-threaded writes (C12a/C12b), superseded-not-edited decision records, the rebuild drill, and
a rubric regrouped into six scoreable layers. Two claims were **rejected during verification** —
see §14.*

A practical standard for setting up and operating Clairvoyance Workspaces where AI Staff do
sustained work. It exists because most Workspace problems are not intelligence problems — they
are *memory, orientation and verification* problems, and those are fixable with structure.

**Three parts:**

1. **The Charter** — 12 principles, for judgment no procedure covers.
2. **The SOPs** — 6 procedures for the repeatable work.
3. **The Rubric** — 34 checkable criteria, in six scoreable layers.

> **How to read this.** Internalise the Charter. Follow the SOPs. Score against the Rubric.
> If an SOP conflicts with the Charter, the Charter wins and the SOP is wrong.

> **This is a floor, not a ceiling.** Every rule here has a cost. A two-file Workspace you
> actually use beats a fully compliant one you abandon. §13 covers when to deliberately ignore
> this document.

---

## 0. Evidence and its limits

This Standard is built on two legs.

**Practice.** Structured surveys of five production Workspaces running AI Staff across creative,
engineering, pipeline and operations work — describing actual state, with gaps marked. Where a
rule below is marked *"multiple independent confirmations,"* that means several teams hit the same
wall separately. That is the strongest evidence in this document.

**Research.** Published work, content-verified: every load-bearing citation was fetched and read,
not merely confirmed to exist. That process **refuted part of the first draft** (see C1) and
sharpened four other principles.

**Limits, stated plainly:**

- Research findings on agentic AI are young and some cited sources are proposals rather than
  validated results. Those are labelled inline.
- Surveys are self-reported by one operator per Workspace.
- Numbers quoted as *community-tier* come from issue reports and practitioner research, not
  controlled studies. Directionally useful; do not treat as authoritative.

---

## 1. Classify your Workspace first

Not every rule applies everywhere. Scoring a Workspace against criteria it structurally cannot
meet produces noise and teaches people to ignore the rubric.

| Class | Definition | Applies |
|---|---|---|
| **Project** | A human-designed directory for a body of work. | Full Standard |
| **Pipeline** | A Project that also runs recurring automated throughput. | Full Standard + SOP-6 |
| **Base** | Your app's own user-data root, with a Workspace registered on top. | Charter + SOPs 3–5 only |

**Why the Base class exists.** In a Base workspace the folder layout is app-generated, durable
content is interleaved with runtime state, files are rewritten at runtime, and it is usually not
a version-controlled repository. You cannot tidy that tree — deleting an "unused" folder can break
the app. **Waive** structure, naming and hygiene criteria there. **Do not waive** decision records,
review gates, or honest health signals.

---

## 2. The Charter

### C1 — The entry point must be *directive*, not *descriptive*

A Staff member arriving cold should orient from one known file — and that file should tell them
**what to do and where to go**, not describe the project at them.

This is narrower than the usual advice, deliberately. A study of repository-level context files
for coding agents found they **did not generally improve task success rates and increased
inference cost by over 20%**, across different models and agents, for both AI-generated and
human-written files. But the breakdown is the useful part: **instructions were well followed,
while repository overviews — popular and widely recommended — were not helpful.**

So:

- **Write instructions, routes and constraints.** These get followed and earn their tokens.
- **Do not write project overviews for agents.** Keep the descriptive tour in a human-facing
  README, off the agent's path.
- **Every line in an agent-facing file should be actionable**, or it costs more than it returns.

**Two corollaries, both load-bearing:**

**C1a — Do not auto-generate your instruction file.** Generated context files measured *worse than
no file at all*. A follow-up study makes the mechanism explicit: **how the guidance is produced is
the decisive variable.** Guidance iteratively tuned against observed failures reached a **33.0%**
resolve rate, versus **28.3%** for a static generated knowledge base and **25.5%** unguided
(p<0.001 for both contrasts). So the honest position is not "context files don't work" — it is
**untuned context files don't work.** Write yours by hand, then *refine it against failures you
actually observed*, not against what you imagine the agent needs.

**C1b — Anything you name will be over-applied.** The failure mode is **over-compliance, not
neglect.** Most people worry adherence is too low; the measured evidence points the other way.

From the primary source, verified in its full text: a tool merely *mentioned* in a context file was
used **1.6 times per instance on average, versus fewer than 0.01 times when unmentioned** — a
roughly **160-fold** increase. Repository-specific tools showed **2.5 versus fewer than 0.05**.
Naming a thing does not inform the agent that it exists; it instructs the agent to use it.

**Practical consequence: do not mention a tool, path, or procedure you do not want reached for by
default.** "Documenting it for completeness" is not a neutral act — it is a strong default. If you
want something available but not preferred, say so explicitly, or leave it out and let the agent
discover it when it actually needs it.

### C2 — An empty scaffold is worse than none

A router file that says *"No routes yet"* consumes the step meant to help, then fails silently.
Staff instructed to read it first get nothing, and fall back to ad-hoc search anyway — having paid
for the detour.

Research calls this the **container fallacy**: equating the *presence* of an evidence container
with *sufficiency*. **Score contents, never the existence of a file.** Fill it or delete it.

### C3 — Route, don't recite

Keep the entry point short; point to depth with links. A router of IF-lines —
`- IF <situation> → read [[document]]`, *follow exactly one match and skip the rest* — makes
relevance decidable **without opening files**. Tag non-negotiables explicitly so they cannot be
skimmed past. *(Independently nominated as best practice by two surveyed teams.)*

### C4 — Attention is a budget, and instructions compete

Duplicated policy does not reinforce; it dilutes, then contradicts. One surveyed team re-authored
policy across five to seven living documents until two openly contradicted each other; unwinding
it took a dedicated project.

*Community-tier measurement:* a frontier model's system prompt may already carry ~50 instructions,
with reliable adherence to roughly **150–200 total** — beyond which adherence reportedly degrades
**uniformly, not selectively**. You do not lose your least important rule; you lose reliability
everywhere. And instruction files re-injected on every tool call cost far more than their size
suggests — one report measured 11 rule files (~6,200 tokens) consuming **~93,000 tokens, 46% of a
200K context window**, across 30 tool calls. **Splitting instructions across more files does not
buy more instruction slots.**

### C5 — One authored home per rule

Link, don't copy. A ruling should be a one-file edit. Any rule stated twice will diverge; the only
question is when.

### C6 — Durable and scratch must be separable at a glance

If an agent cannot tell where output belongs, output lands anywhere. One surveyed Workspace root
accumulated a dozen temp files plus three whose *filenames were unexpanded paths* — redirects
where a path variable was empty at expansion. It recurred because **nobody owned root hygiene**.
Name the scratch directory unambiguously, and give hygiene an owner.

**Split on three axes, not two.** The most transferable version of this is the *factory vs.
product* distinction: separate **reference material that is stable across runs** from **working
artifacts unique to each run**, and both from **durable output you intend to keep**. Reference is
read-mostly and safe to cache; working state is disposable and must be safe to delete blindly;
output is the thing you would be upset to lose. Three directories, three lifetimes, no ambiguity
about which is which.

### C7 — Green is a claim, not a fact

**Assert on output content; never on exit code alone.** A status signal from a process that does
not actually check is worse than no signal, because it suppresses investigation.

*Four independent instances, in one survey round:* a backup script that never exited non-zero, so
the scheduler logged success on a run that failed its own assertion; a path error that produced
exit 0 and an empty output file that looked like success; a dry-run overwriting a live result with
`ok: true`; and — during this Standard's own research — an automated citation check returning 34
"dead link" verdicts of which **31 were live**, because it never fetched anything.

**C7a — The absence of the expected signal is the alert.** Asserting on content is necessary but
not sufficient, because **a job that never runs produces no failing assertion at all.** Logs and
exit codes are *internal* signals: they fail together with the system that should emit them. Invert
the dependency with a heartbeat — if the job runs, it pings; if it does not, the ping never
arrives, and the silence is the alert. This covers what exit-code alerting structurally cannot:
the scheduler never fired, the daemon died, the schedule was deleted, the host rebooted, the
container wedged, the disk filled.

The canonical case remains the 2017 GitLab data-loss incident, where four of five backup methods
had been failing silently for months. The monitoring was correctly configured **to alert on the
presence of errors — which is exactly why it detected nothing.** Green dashboards, exit code 0, no
backups.

**C7b — The success signal must be downstream of the assertion.** A ping emitted unconditionally,
or at the top of a script, is decoration. Put it last, and make it conditional on **both** the work
completing **and** its output assertion passing:

```
do_the_work  →  assert_the_output  →  signal_success
```

**Three terms, not two.** Chaining a signal to the work's *exit status* alone reproduces the exact
failure C7 just described — an exit code is a claim about completion, not evidence about output.
The assertion is the term that makes the signal mean anything.

**Shell note, because the obvious idiom is not portable.** In POSIX `sh`, `cmd.exe` and
PowerShell 7+, this is written directly:

```sh
do_the_work && assert_the_output && signal_success
```

**`&&` does not exist in Windows PowerShell 5.1** — the Windows default shell, and what many
scheduled tasks run under. It is a **parse** error, not a runtime one, so a script using it does
not run at all. There, express the same three terms explicitly:

```powershell
$ErrorActionPreference = 'Stop'   # script scope; promotes non-terminating errors
try   { Invoke-Work }
catch { exit 1 }
if (Assert-Output) { Signal-Success }
```

**Two traps in that snippet, both of which fail by signalling success on failed work.**

*Set the preference at script scope; do not rely on `-ErrorAction Stop` at the call site.*
`-ErrorAction` is a common parameter, so a **simple** function — one without `[CmdletBinding()]` —
accepts it and silently discards it. `Write-Error` stays non-terminating, `catch` never fires, and
execution falls straight through to the signal. That is the shape most people write, and it is
wrong only in the case nobody tests.

*Do not gate on `$LASTEXITCODE` unless the work is a native executable.* It is not updated by
PowerShell functions or cmdlets, so it silently retains a value from some earlier, unrelated
command — a status check reporting on the wrong thing.

Both traps are the same failure this section exists to prevent, reproduced inside the fix for it.
They are recorded rather than quietly corrected because **that is the evidence for C7**: the
mechanism is not carelessness, it is that a check which resembles a check passes review.

### C8 — A status artifact must record the mode that produced it

Dry-run and live results are not interchangeable and must not be able to overwrite each other
indistinguishably. A dry-run reporting `count=0` is otherwise indistinguishable from a live run
that failed.

> **Provenance note, stated because this Standard demands it of others.** A deliberate search
> found **no authoritative source** recommending that execution mode be recorded in status
> artifacts. This principle is a **local extension**, not established practice — it follows from
> the structured-payload assertion pattern (C7), but nobody in the surveyed literature says it.
> It earns its place here on internal incident evidence: a dry-run overwrote a live result with
> `ok: true` in a production Workspace. Adopt it because the reasoning holds, not because someone
> cited it.

### C9 — Decisions are the asset; artifacts are the residue

Prior decisions **and their rationale** must be recoverable by someone who was not there. Private
per-agent memory is not a decision record — it is invisible to every other Staff member.

*This was the strongest single finding of the survey: four of five Workspaces independently
reported having no shared decision record.* One operator summarised the result as institutional
memory living entirely in the owner's head — a single point of failure that is a person.

Research names the same problem: each commit captures a diff but discards "the constraints,
rejected alternatives, and forward-looking context that shaped the decision" — the **Decision
Shadow**. *(That specific protocol proposal is unvalidated; the concept is sound, the mechanism
unproven.)*

### C10 — Independent review beats self-review

This is the best-supported principle here — three independent results:

- Review conducted in a **fresh session with no access to the production conversation** caught
  meaningfully more injected errors than same-session self-review (F1 **28.6% vs 24.6%**,
  p=0.008). Critically, **reviewing twice in the same session did not beat reviewing once** —
  so the gain comes from **context separation itself**, not extra effort.
- Holding an erroneous claim byte-identical and changing only *whose voice carries it*, relabelling
  from the agent's own reasoning to an external source lifted correction rates by **23–93
  percentage points**. Failure to self-correct is largely a **role-label artifact**, not a
  capability deficit — which is exactly why an independent reviewer works.
- Models rate their own familiar output more highly, so a reviewer should not assess its own work.
  **The bias is really *familiarity*, not vanity** — judges over-reward low-perplexity text
  regardless of who wrote it. That matters more than it sounds: it means a review panel also
  **penalises correct-but-unusual answers**, not just rival models.

Industry practice has converged on the same shape independently: *"a clean-context reviewer catches
bugs the coder can't see."*

**The fix is a formatting change, not a smarter reviewer.** Re-present the artifact to the reviewer
as **external input** — extracted, without the production conversation attached. Prompting a model
to "be critical of your own work" does not reproduce the effect; the mechanism is *addressability*,
not effort or capability.

**If you use a review panel, check that it disagrees.** Multiple reviewers only pay off when their
errors **decorrelate**. Mixing providers is a *hypothesis* about decorrelation, not a guarantee —
shared latent confounders induce correlated errors even across vendors. **If your panel always
agrees, you paid three times for one verdict.** Treat disagreement as the signal that triggers
human review, not as noise to be averaged away.

**Honest caveat: absolute review performance is poor.** A best case near 29% F1 means even good
independent review catches under a third of errors. It beats self-review; it is not a guarantee.
**Never let a passed review substitute for testing.**

### C11 — Address external resources by stable ID, never display name

Name-based addressing fails silently and late. In one surveyed case a sync tool addressed remote
storage by path name, could not see an API-created folder, and **auto-created a duplicate tree
that quietly swallowed every backup** — while the correct folder ID sat defined-but-unused. Same
shape as an upsert without a match key: it duplicates instead of updating, and you find out days
later.

### C12 — More agents is not more capability

Add a seat when there is a distinct role and a defined handoff — not to increase throughput.

Single-agent systems match or outperform multi-agent systems on multi-hop reasoning **when
reasoning tokens are held constant**; reported multi-agent gains are often confounded by simply
spending more compute. **The nuance cuts both ways:** multi-agent becomes competitive precisely
when a single agent's **effective context utilisation degrades**. The honest rule: multi-agent is
justified when **context is the binding constraint**, not when throughput is the goal.

**C12a — Keep writes single-threaded; let extra agents contribute intelligence, not actions.**
This is the highest-value coordination rule available, and it is a *revised* industry position —
the widely-cited 2025 "don't build multi-agents" advice was superseded in April 2026 by a narrower
claim that has held up: *"multi-agent systems work best today when writes stay single-threaded and
the additional agents contribute intelligence rather than actions."* In practice most production
subagents end up **read-only** — search, review, analysis — resembling tool calls more than
collaborators.

*Independent internal confirmation:* one surveyed team arrived at the identical rule from painful
experience and states it as a hard constraint — **never let two Staff edit the same structured
record simultaneously**, because the store is last-writer-wins.

**C12b — Know where multi-agent is a poor fit, per its own strongest advocate.** The vendor
reporting the largest multi-agent gains also states the boundary explicitly: domains that require
**all agents to share the same context**, or that involve **many dependencies between agents**, are
a poor fit today — and names **coding** as exactly such a case. When the vendor limits its own
claim, believe the limit.

---

## 3. Artifacts, and when they earn their place

Names are conventions, not magic — consistency across your Workspaces is the point.

**Read this table as triggers, not as a checklist.** By C1b, naming an artifact makes it something
an agent will create; a column headed *"required"* would produce `REBUILD.md` files in Workspaces
that will never be rebuilt. **Each artifact has to be earned by a condition that already exists in
your Workspace.** If the trigger has not fired, not having the file is the correct state — score it
`n-a`, not `no`.

| Artifact | Purpose | Create it when… |
|---|---|---|
| `library.md` | IF-line router. Entry point. **Never a stub.** | …there is more than one place a Staff member might need to go. This is the first file and nearly always earned. |
| `AGENTS.md` | Charter: role, authority, policies, escalation. | …someone other than you will work here, or authority over decisions is not obvious. |
| `README.md` | Layout and conventions, for humans. | …the directory layout is not self-evident, or humans other than you open it. |
| `docs/REBUILD.md` | Rebuild-from-zero guide. | …there is a process someone would otherwise have to reconstruct by reading code. |
| `docs/DECISIONS.md` | Shared record incl. **rejected alternatives**. | …a decision has been made that would be expensive to revisit. In practice: immediately. |
| `docs/STATUS.md` | Work ledger: open items, owner, assignments. | …work outlives a session, or more than one Staff member takes assignments here. |
| `versions/v<n>_<date>/` | Config snapshot + narrative `VERSION.md`. | …configuration changes are consequential across runs and you would want to compare or roll back. |

*The two that are effectively always earned are the router and the decision record. The rest depend
on your Workspace, and creating them speculatively costs more than it returns.*

**On work tracking.** If your Clairvoyance tier includes Todos, use them — they are better than a
markdown file. If it does not, `docs/STATUS.md` is the fallback and it is normative in this
Standard, because a standard nobody can execute is decoration. Check your tier before designing
around either.

---

## 4. SOP-1 — Standing up a Workspace

> **Do only the steps whose trigger has fired.** §3 says which. This is a numbered list and numbered
> lists get executed in full — which would rebuild the seven-artifact scaffold §3 exists to prevent.
> **Steps 1, 2 and 5 are effectively always earned. The rest are conditional, and skipping them is a
> correct outcome, not an incomplete build.**

1. **Classify** (§1). State the class and why.
2. **Create the tree.** Separate what is stable, what is disposable, and what would hurt to lose —
   three lifetimes, three places. Name the scratch directory unambiguously; never write durable
   output there.
3. **Write `README.md`** — layout, one line per directory, plus any storage-residency rule.
   *Trigger: the layout is not self-evident, or humans other than you will open it.*
4. **Write `AGENTS.md`** — role and scope; who holds authority and over what; escalation path;
   the team and their lanes; hard constraints. Short enough to be read every session. **Directive,
   not descriptive** (C1). *Trigger: someone other than you works here, or authority is not obvious.*
   **On the name, and on runtime auto-loading.** `AGENTS.md` is deliberately vendor-neutral — a
   Workspace charter file should not be named after one model vendor, and the file outlives whichever
   tool you are using this year. It is also a published open format with broad multi-vendor
   adoption, not a local convention.

   But most agent runtimes **auto-load a file of their own choosing** into context at session
   start, and they do not all choose the same name. If yours does not read `AGENTS.md`, your
   charter file is silently not loaded — the worst failure mode available, because nothing reports it.
   The rule, in three parts:

   1. **`AGENTS.md` is canonical.** All substance lives there.
   2. **If — and only if — your runtime auto-loads a different filename**, add that file as a
      *pointer*: include or import `AGENTS.md` using whatever include mechanism the runtime
      provides, or a one-line "read `AGENTS.md` first" if it has none.
   3. **The pointer file may add, never restate.** Genuinely runtime-specific lines are fine —
      tool invocations, hook paths, review commands. The moment it repeats a policy that also
      lives in `AGENTS.md`, you have two charter files, and the copy will drift.

   **Do not create pointer files for runtimes you do not use.** By C1b, a named file is a file
   agents will create and reach for; a Workspace carrying five vendor charter files for one runtime is
   the over-application failure, not thoroughness. Add the one your runtime actually loads.

   *A dated, non-normative list of which tools load which filename is in §15. It is a snapshot of a
   fast-moving ecosystem — verify it against your runtime's current documentation rather than
   trusting it, and treat its absence of a tool as "not checked", not "does not exist".*
5. **Create `library.md` with at least one real route.** If nothing is worth routing, the Workspace
   is not ready for Staff. Never leave template text in place (C2).
6. **Create `docs/DECISIONS.md` and `docs/STATUS.md`.** *Trigger for DECISIONS: a choice has been
   made that would be expensive to revisit — in practice, immediately. Trigger for STATUS: work
   outlives a session, or more than one person takes assignments here.*
7. **Register naming conventions** in `README.md`: work-unit key, run key, version directory,
   backup suffix. *Trigger: a convention exists that someone could get wrong.* Do not invent
   conventions to register — unwritten conventions do not survive staff turnover, but invented ones
   become rituals (C1b).
8. **Declare the review gate** (SOP-3) and name who holds it. *Trigger: changes here can touch live
   data, published output, or shared configuration.*

**Definition of done:** a Staff member who has never seen this Workspace can read `library.md` and
`AGENTS.md` and correctly answer — what is this for, who decides, where does output go, what am I
not allowed to do.

---

## 5. SOP-2 — Documenting a process

1. **Write a rebuild guide, not a description.** Test: could someone reconstruct this from zero
   using only this document?
2. **Prefer an executable spec.** Where the document *is* the procedure the agent follows, drift
   surfaces as a failed run instead of silent rot.
3. **Mark the audience** in a header — `Audience: human` / `staff` / `both`. Unmarked audience is a
   live trip hazard: some runbooks assume a human at an elevated shell, others are agent-executable,
   and nothing distinguishes them.
4. **Add a navigation layer** past ~15 KB. One surveyed runbook is ~72 KB with five headings.
5. **Route it from `library.md` in the same change.** An unrouted document is invisible.
6. **Date regenerated snapshots** and mark them stale-on-sight. Two teams reported fixing silently
   drifted values in the same month.
7. **Keep runbooks inside the Workspace**, or route to them explicitly. Two surveyed Workspaces
   kept their best process docs in a sibling directory nothing indexed — "you can only find them
   if you already know."

---

## 6. SOP-3 — Decisions and review

**Record a decision** on any choice that is expensive to reverse, constrains future work, or was
non-obvious:

```
## <YYYY-MM-DD> — <short title>
Status:     Accepted | Superseded by <link> on <date>
Decision:   <what was decided>
Context:    <what forced the choice>
Rejected:   <alternatives and why not>   ← the part everyone skips and later needs
Evidence:   <how it was verified, or "asserted, unverified">
Decided by: <name> — human | agent
Agent had:  <what context the agent was working from, if an agent decided>
```

**Rejected alternatives are mandatory.** Without them, a future reader re-opens a settled question
or re-tries a known failure.

**Supersede; never edit in place.** When a decision changes, mark the old entry `Superseded by`
with a date and write a new one. Editing history destroys the reasoning trail you built the record
for — and the *sequence* of decisions is often more informative than any single entry.

**Record whether a human or an agent decided, and what context the agent had.** These are not the
same kind of decision and should not be weighed the same later. An agent decision made with partial
context is a candidate for revisiting; a human decision made with full context usually is not. If
you cannot reconstruct what the agent knew, that itself is worth writing down.

**The review gate.** For anything touching live data, published output, or shared configuration:

1. Author states the claim and the evidence.
2. An **independent** reviewer — ideally in a **fresh session without the production context**
   (C10) — **reproduces** the claim rather than reading it.
3. Verdict recorded: approve / approve-with-conditions / block-step.
4. Blocked steps do not proceed on the author's judgment alone.

**Write down what happens when the gate is skipped.** One surveyed team's gate was bypassed under
deadline pressure — a change went live unreviewed because a 03:00 deadline was nearer than the
reviewer. A gate with no defined bypass gets an undefined one.

---

## 7. SOP-4 — Automation and health signals

1. **Assert on content, not exit code** (C7). End every scheduled job with a check on the *shape*
   of its output — emit a structured payload (`{"rows_exported": 1523, "status": "ok"}`) and alert
   when the count falls below threshold. This is the difference between *"did it run"* and *"did it
   do the thing."*
2. **Add a heartbeat so silence pages you** (C7a). Content assertions cannot fire if the job never
   starts. Emit the ping only after the content assertion passes — never on completion alone (C7b).
   The obvious `&&` idiom is unavailable in Windows PowerShell 5.1; see C7b for the portable form.
3. **Set a grace period.** A job scheduled "every 24 hours" never runs at exactly 24-hour intervals.
   Configure expected-interval **plus** grace, or the monitor becomes noise and gets muted — at
   which point you have negative value.
4. **Treat duration anomaly as its own alert class**, distinct from missed-ping and from
   assertion-failure. A job that completes but takes four times as long is telling you something
   that neither of the other two signals will.
5. **Triage what deserves monitoring at all:** *if you would want to know within an hour that this
   job stopped running, monitor it.* Otherwise do not — an alert nobody acts on trains everyone to
   ignore alerts.
6. **Record the mode** in every status artifact (C8). Dry-run must not overwrite live.
7. **Reap completed one-shots.** Fire-once tasks left enabled accrete forever.
8. **Never store backups inside a live config directory.**
9. **Restart long-lived workers after a config cutover.** One worker held a stale path for an hour
   after the fix and wrote to the wrong tree. Resolver logic does not help; restarting does.
10. **Resolve paths through one resolver.** Absolute paths baked into *state files* at creation are
    resolver-independent and survive every environment fix — sweep state and config files, not just
    scripts.
11. **Keep local-model Staff off unattended paths** unless you have verified end-to-end completion
    delivery yourself. Two independent teams found local-model Staff completing inference but
    failing to deliver the completion handoff.
12. **Name scheduled tasks with their owning Workspace** if your scheduler uses one global pool.
13. **Assert that a write landed where the app actually reads from.** Nothing in a typical setup
    checks this. After any base-path or storage migration, a stale path can keep silently accepting
    writes and serving frozen content, with no error at any layer — files appear to save and simply
    never take effect. *(Observed in production during the writing of this Standard: eleven files
    written to a superseded path over two days, none of them visible to the running application.)*

---

## 8. SOP-5 — Staffing and handoff

1. **Name a lead**, or explicitly record that the human owner coordinates.
2. **Lanes, not hierarchy.** Peer co-leads meeting at a defined boundary works well — e.g. a
   content lead and a systems lead, explicitly peers.
3. **Maintain an assignment ledger** in `docs/STATUS.md`. *Duplicate delegation is a real and
   recurring cost: one surveyed team had the same item assigned to two Staff in parallel twice,
   detected only by racing on the same file.*
4. **Never put load-bearing content in a lightweight status channel.** Know exactly which fields
   your status mechanism preserves — one team lost three messages to a status call that silently
   kept only two fields, including a review request that never arrived, so a change went live
   unreviewed for a day. **Use the formal completion/report channel for anything that matters.**
5. **Formal handoffs go to the inbox; live messages are for questions, assignments and decisions.**
   Status, FYI and acknowledgements should never interrupt a working session.
6. **Concentrate sensitive access rather than distributing it.** Where some knowledge must be
   withheld, one holder beats redundant reviewers; have them log *that* something was withheld and
   why, never *what*.
7. **Know your roster's limits** before designing around it — whether hires are global or
   per-Workspace, whether a durable peer roster exists, and whether removal requires manual action.

---

## 9. SOP-6 — Pipeline Workspaces

> **Honesty label, because this Standard demands it elsewhere.** There is **no established
> workspace-layout practice for AI agents.** A deliberate search found no spec, no standard, and no
> controlled study for queue-folder or directory-as-state-machine patterns in agent workspaces.
> What follows is a **local convention** — validated in production by the teams surveyed here and
> supported by one published paper, not by an industry standard. Adopt it because it works, and
> deviate without guilt.

1. **Make the stage a folder.** Forward-only, one manifest per work unit. `ls | wc -l` becomes a
   status report; it is crash-safe, resumable, and needs no database. *One published method matches
   this closely: numbered folders as stages, with plain markdown carrying the role instructions,
   replacing framework-level orchestration for sequential human-reviewed workflows.*
2. **Make every step idempotent and re-runnable.** Retry, resumption, and partial-failure recovery
   all assume a step can be executed twice without damage. *A surveyed publish pipeline is
   idempotent and resumable by design and reported it as the property that made recovery routine
   rather than manual.* Anything expensive or irreversible needs an explicit guard, not an
   assumption that it runs once.
3. **Give failure its own terminal stages** — `failed/`, plus quarantine for units that are valid
   but out of policy.
4. **Gate cost explicitly.** Separate free/local stages from paid ones; let a gate decide promotion
   and record its decision.
5. **Make retry a first-class tool**, not a manual re-run.
6. **Self-flag dead inputs** after a defined failure window.
7. **Review cards over dashboards:** a failure becomes a durable note with options, and a human
   edits one line to steer the retry. Nothing to babysit.

---

## 10. The Audit Rubric

**Score contents, not file existence** (C2).

This is a **capability checklist, not a maturity ladder**. Do not total the score or rank
Workspaces against each other; use it to find specific gaps worth closing. *(Noting the field is
not unanimous — at least one published rubric does use executable maturity levels. Levels are
defensible when each level is executable rather than aspirational.)*

**Five verdicts, not four.** `yes` / `partial` / `no` / `n-a` / **`blocked`**.

**`blocked` means: needed here, and cannot currently be done.** The gap is real, it is not
negligence, and it is not progress. Use it when a criterion is defeated by something outside the
Workspace's control — a platform capability you do not have, a tier gate, a missing skill nobody on
hand possesses. Without this verdict the honest state has nowhere to go: `n-a` denies a failure mode
that exists, `no` reads as carelessness, and `partial` implies motion that is not happening.
**Marking a criterion complete because a plan mentioned it is a green-signal lie about your own
compliance** — which is the failure this Standard exists to prevent, turned inward.

Every `blocked` carries what would unblock it. A blocked criterion with no stated unblocker is
just a `no` wearing better clothes.

**Score per layer, not as a total.** Grouping matters: a Workspace can be strong on instructions
and weak on reliability, and a single blended number hides exactly that. **Pair each layer's score
with a direction of travel** (improving / static / degrading) — the trajectory is more actionable
than the level. **Do not publish cross-team level comparisons**; they drive gaming rather than
improvement.

**Instruction & context layer**

| # | Criterion | Class |
|---|---|---|
| R1 | Entry-point router exists **and contains real routes** | All |
| R2 | Router covers every process doc | All |
| R3 | Charter FILE exists (role, authority, escalation) | Project, Pipeline |
| R4 | No policy authored in more than one place | All |
| R5 | Agent-facing instruction files are **hand-authored, not generated** (C1a) | All |
| R6 | Instruction files contain **no rules the toolchain already enforces deterministically** | Project, Pipeline *with tooling* |
| R7 | Deep reference is behind an index and loaded on demand, not inlined | All |

**Decision & rationale layer**

| # | Criterion | Class |
|---|---|---|
| R8 | Shared decision record exists, Workspace-local | All |
| R9 | Decision entries capture rationale **and rejected alternatives** | All |
| R10 | Superseded decisions are **marked, not edited in place** | All |
| R11 | Each entry records **who decided — human or agent** — and the agent's context | All |

**Runbook & procedure layer**

| # | Criterion | Class |
|---|---|---|
| R12 | Rebuild-from-zero guide exists | Project, Pipeline |
| R13 | **The rebuild guide has actually been followed from zero**, with failures logged | Project, Pipeline |
| R14 | Process docs declare their audience | Project, Pipeline |
| R15 | Runbooks live in, or are routed from, the Workspace | All |
| R16 | An automated **freshness signal** surfaces stale docs before a human notices | Project, Pipeline |

**Orchestration & coordination layer**

| # | Criterion | Class |
|---|---|---|
| R17 | Shared work ledger exists (not private memory) | All |
| R18 | Assignment ledger prevents duplicate delegation | All |
| R19 | Every delegated task has an **explicit, checkable** definition of done | All |
| R20 | **Writes are single-threaded**; parallel Staff contribute analysis, not concurrent edits | All |
| R21 | A lead is named, or owner-as-coordinator is explicit | All |
| R22 | Independent review gate for consequential changes | All |
| R23 | The review procedure **specifies** re-presentation as external input, not inline review | All |

**Reliability & honesty layer**

| # | Criterion | Class |
|---|---|---|
| R24 | Automated jobs assert on output **content**, not exit code | All |
| R25 | Success signals fire **only after the work and its content assertion have both passed** — failure cannot signal success | All |
| R26 | A missing run alerts — **absence of signal is monitored** | All |
| R27 | Status artifacts record execution mode | All |
| R28 | Completed one-shot automation is reaped | All |
| R29 | No absolute base paths baked into state files | All |
| R30 | External resources addressed by stable ID | All |
| R31 | Local-model Staff are not on unattended paths | All |

**Structure layer**

| # | Criterion | Class |
|---|---|---|
| R32 | Reference / working / durable-output are separable at a glance | Project, Pipeline |
| R33 | Root is clean and hygiene has a named owner | Project, Pipeline |
| R34 | Config snapshots with narrative changelog | Project, Pipeline |

**R13 is the one people skip and the one that pays.** A rebuild guide nobody has executed is a
hypothesis. Running it once — and logging where it failed — converts it into a document you can
trust under pressure, which is the only time you will reach for it.

**Score criteria against evidence you can inspect today.** Several criteria describe procedures
rather than events, deliberately: an auditor arriving cold cannot verify how a past review was
conducted, and scoring it `no` for lack of evidence manufactures a gap that is not there. Where you
cannot evidence something, score `?` and say what would settle it.

---

## 11. Anti-pattern catalogue

All observed in production, most more than once.

| Anti-pattern | Signature |
|---|---|
| **Stub scaffold** | Router exists, says "No routes yet", consumes the orientation step |
| **Green-signal lie** | Exit 0 on failure; dry-run overwriting live; a check that never checked |
| **Baked state path** | Absolute path written into a state file at creation; immune to env fixes |
| **Stale worker** | Long-lived process holds pre-cutover config for its whole lifetime |
| **Path-sweep over-correction** | "Fixing" every environment variable on sight when only a subtree moved |
| **Name-addressed remote** | Display-name addressing silently creates a duplicate tree |
| **Silent duplicate record** | Upsert without a match key duplicates instead of updating |
| **Private decision record** | Rationale in per-agent memory, invisible to everyone else |
| **Title inflation** | A source labelled more authoritative than it is |
| **Unowned root** | Temp files accumulate because no one owns hygiene |
| **Overview-as-instructions** | Descriptive project prose in an agent-facing file (C1) |
| **Auto-generated instructions** | `/init`-style generated context file, never tuned against real failures (C1a) |
| **Over-application** | A tool or path mentioned "for completeness" becomes the default choice (C1b) |
| **Unconditional success ping** | Heartbeat emitted at the top of the script, so it fires even when the work fails (C7b) |
| **Untested rebuild guide** | Rebuild documentation nobody has ever executed (R13) |
| **Concurrent writers** | Two Staff editing the same record; last-writer-wins silently discards one (C12a) |
| **Agreeable panel** | Multi-reviewer setup whose members never disagree — three verdicts, one opinion (C10) |

---

## 12. Adoption order

Do not adopt this all at once. Ranked by benefit-to-effort from the audits that produced it:

1. **Fill or delete your router** (C2, R1). Minutes. Highest return.
2. **Start `docs/DECISIONS.md`.** The most-missed artifact in every Workspace surveyed.
3. **Add content assertions to your riskiest scheduled job** (C7). Start with backups.
4. **Name a lead and start an assignment ledger** (SOP-5).
5. **Write the rebuild guide** for your most complex Workspace (SOP-2).
6. **Everything else**, as it earns its place.
7. **If executing your plan requires code — assertions, heartbeats, pipeline scripts — recognise
   that as a different skill set from designing the Workspace.** Planning a monitoring criterion
   and implementing one are not the same job, and a plan whose top recommendation is "add an output
   assertion to your backup job" is not actionable to someone who cannot write one. Name the
   capability the work needs. Most Workspaces never reach this point; reaching for it before you do
   is cost without return.

---

## 13. When to ignore this Standard

Deliberately included, because a standard without an off-switch gets applied where it does not fit.

- **Short-lived or exploratory Workspaces.** Scratch work does not need a charter.
- **Solo, single-session work.** Most of this exists to move context *between* sessions and *between*
  Staff. Remove those and much of it is overhead.
- **When a criterion has no failure mode in your context.** A Workspace with no automation does not
  need SOP-4. Mark it `n-a` and move on.
- **When the platform blocks it.** If your tier lacks a feature, substitute or skip — do not
  simulate it badly.
- **When it would cost more than the failure it prevents.** The rubric finds gaps; it does not
  decide which are worth closing. That judgment stays with the owner.

**The one rule with no exception is C7.** A signal that lies is worse than no signal, in every
context, at every scale. If you adopt one thing from this document, adopt that.

---

---

## 14. What was rejected during verification

Recorded because a standard that only shows its wins is not showing you its method.

**Rejected — citation did not support the claim.** A widely-quoted breakdown of multi-agent failure
modes (step repetition ~15.7%, termination-condition blindness ~12.4%, together ~28% of failures)
was traced to a paper that is **about something else entirely** — graph-guided investigation of
operational data. The taxonomy it was attributed to is real and well-grounded; **that specific
distribution is not supported by the cited source** and does not appear in this Standard. The
underlying taxonomy's own authors note that category percentages are dataset-dependent, so treat
any precise split you see quoted with suspicion.

**Downgraded, then restored — number verified in full text.** The claim that merely naming a tool
drove ~160× more use of it was not confirmable from the source *abstract*, so C1b initially carried
it as unverified. Fetching the paper's full text resolved it: the underlying figures are **1.6 uses
per instance when mentioned vs. fewer than 0.01 when not**, which is where the 160× comes from. The
figure is a faithful derivation, and C1b now cites the underlying ratios instead of the headline.
*Method note: an abstract is not the paper. Two of the checks in this Standard changed outcome once
the full text was read.*

**Downgraded — dead source.** One frequently-cited article on silent cron failure returns a hard
404. The argument it supported is independently sourced and survives; the citation does not.

**Labelled as local, not cited.** C8 (record execution mode) and SOP-6 (folder-as-state-machine)
have **no authoritative external backing**. Both are marked in place rather than dressed up. A
deliberate search found no established workspace-layout practice for AI agents at all — if a
standard tells you otherwise, ask it for the citation.

**Two headline studies genuinely disagree**, and anyone citing one is giving you half the picture:
one measured *efficiency* on focused changes and found context files produced meaningfully less
runtime and fewer output tokens; another measured *correctness* and found success rates fell while
cost rose over 20%. The reconciliation offered is that context files **reduce wandering without
improving the destination** — they help agents navigate faster, not arrive somewhere better. C1
and C1a are written to survive both results.

---

## 15. Appendix — runtime auto-load filenames (non-normative)

> **Non-normative. Stale on sight. Verified 2026-07-25.**
> This is a dated snapshot of a fast-moving ecosystem, kept out of §6's artifact table on purpose:
> that table lists artifacts an agent should *create when a trigger fires*, and by **C1b** a named
> file is a file agents will create. A roster of six vendor filenames in the normative text would
> produce Workspaces holding six charter files for one runtime — the exact over-application this
> Standard documents.
>
> **The first line of defence is audience, not placement.** This document is `Audience: human`;
> agents never read it, they read the compact working copy derived via the Implementation Runbook.
> C1b's mechanism is *agents create what is named for them*, so a roster is safe **here** and
> dangerous **there**. ⚠️ **Do not migrate this table into the agent-facing derive doc, a Criteria
> Card, or an `AGENTS.md`** — that reintroduces exactly the failure this placement avoids.
>
> **What this table is for:** determining *which case you are in*, so SOP-1 step 4 is actionable.
> Without it, "add a pointer file only if your runtime auto-loads a different name" asks a reader
> to go research five vendors before they can act — and the realistic outcome is that they skip the
> step, which is the silent-charter-not-loaded failure. **It is a lookup, not a list of files to
> create.**

Most agent runtimes load a file into context automatically at session start. They do not agree on
the name. `AGENTS.md` is the open, multi-vendor format and is the canonical charter file under this
Standard; anything else is a pointer to it.

| Runtime | Auto-loaded file | Confidence |
|---|---|---|
| OpenAI Codex | `AGENTS.md` | High — the format originates here |
| Claude Code | `CLAUDE.md` (hierarchical: user → project → parent dirs → subdirectory on demand) | High |
| Gemini CLI | `GEMINI.md`, configurable | Medium-high |
| GitHub Copilot | `.github/copilot-instructions.md` | Medium-high |
| Cursor | `.cursor/rules/*.mdc` (legacy `.cursorrules`) | Medium |

**Confidence is marked because it is not uniform, and an unmarked list would imply verification
that did not happen.** Entries are marked from documentation and usage at the date above, not from
a test of each runtime.

**Deliberately absent:** xAI / Grok, and every runtime not listed. Absence here means **not
verified**, never "has no such file." Naming a filename we had not confirmed would be worse than
omitting it — a reader would create it, and by C1b, act on it.

**Example of the pointer pattern.** Claude Code supports importing another file from within its
charter, so the vendor file can stay one line of substance plus what is genuinely runtime-specific:

```markdown
# CLAUDE.md
@AGENTS.md

## Claude Code specifics
- Hooks live in .claude/settings.json; do not hand-edit settings.local.json.
```

*The `@path` import is a real, current Claude Code feature — but import syntax is a vendor detail
and is the most likely thing on this page to change, so confirm it against current documentation
before relying on it.* Where a runtime offers no include
mechanism, a one-line "read `AGENTS.md` first, it is the charter file" is sufficient; the point is one
source of truth, not the elegance of the include.

---

*Derived from surveys of five production Workspaces and content-verified published
research. Adapt freely.* **Every source behind that claim is listed in
[CITATIONS.md](CITATIONS.md)** — with a confidence mark per entry, the claims that have **no**
external citation, and the places this document overreaches what its sources actually measured.

Companion: [Workspace Architect Build Runbook](runbooks/architect-build-runbook.md) — creates a Staff member who can plan and
build Workspaces to this Standard.
