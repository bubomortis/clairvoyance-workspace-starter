# The Clairvoyance Workspace Standard

**Version:** 1.7 · **Status:** Free to copy, adapt, and share.
**Audience: human.** This document exists to be understood, argued with, and updated as the subject
matures. It is deliberately heavy on evidence, counter-evidence and rationale — the parts a person
needs to decide whether to adopt a rule, and the parts an agent does not benefit from (C1).

**If you want Staff to *implement* this rather than read it**, do not point them here. Point them at
[Implementation Runbook](IMPLEMENTATION.md), which has them derive a compact working copy tuned
to your instance. You should not have to study this document to benefit from it.

**Upgrading from v1.4, v1.5 or v1.6?** No artifact you created changes name or location. But two
releases **tighten conformance**, so re-check any audit you are still relying on:

- **v1.5** — an audit that passed with an unblocker reading *"when we have time"* does not pass
  now, and `?` rows acquire an owner, an age, and a decay to `no`.
- **v1.7** — **re-score every C14 exception and every `accepted` from a v1.6 audit.** An exception
  now passes only with all four conditions; the Engineer persona shipped in v1.6 taught two of
  them, so anything built from it is a violation rather than an exception — check specifically for
  the missing *do not copy this pattern* marking and the missing *fails loudly and by name*.
  An `accepted` now needs a re-raise condition a third party could notice without asking you —
  *"revisit if circumstances change"* no longer passes — **and the owner has to confirm it.**
  Separately, C16 stops exempting a half-measure on the strength of an intention to finish it, and
  a Base Workspace that was told C14 applied absolutely can now discharge its exception.

Full history in [CHANGELOG.md](CHANGELOG.md).

A practical standard for setting up and operating Clairvoyance Workspaces where AI Staff do
sustained work. It exists because most Workspace problems are not intelligence problems — they
are *memory, orientation and verification* problems, and those are fixable with structure.

**Three parts:**

1. **The Charter** — 16 principles, for judgment no procedure covers.
2. **The SOPs** — 7 procedures for the repeatable work.
3. **The Rubric** — 34 checkable criteria in six scoreable layers, plus 5 external-tool criteria.

> **How to read this.** Internalise the Charter. Follow the SOPs. Score against the Rubric.
> If an SOP conflicts with the Charter, the Charter wins and the SOP is wrong.

> **This is a floor, not a ceiling.** Every rule here has a cost. A two-file Workspace you
> actually use beats a fully compliant one you abandon. §14 covers when to deliberately ignore
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
| **Base** | Your app's own user-data root, with a Workspace registered on top. | Charter + SOPs 3–5, **plus any SOP section a Charter criterion in scope depends on** — currently SOP-7 §5, wherever a C14 exception exists |

**Why the Base class exists.** In a Base workspace the folder layout is app-generated, durable
content is interleaved with runtime state, files are rewritten at runtime, and it is usually not
a version-controlled repository. You cannot tidy that tree — deleting an "unused" folder can break
the app. **Waive** structure, naming and hygiene criteria there. **Do not waive** decision records,
review gates, or honest health signals.

⚠️ **A class scope cannot be narrower than the Charter it admits.** If a Charter criterion in
scope discharges through an artifact defined in an SOP, that SOP section is in scope too — read
the "plus" clause above as the general rule, not as a special case for SOP-7. Scope the class
narrower than the criterion's dependencies and the criterion does not become lighter; it becomes
**absolute**, because the only thing that could satisfy it has been ruled out of scope. That is
how a rule with a deliberate exception silently loses it, and it is the failure mode to check for
whenever a new Charter criterion is added: **does every class bound by it have access to what
discharges it?**

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

### C13 — Tools are resolved, not vendored

**A Workspace should not carry a copy of a tool the machine already has. It should resolve the
tool by name and let the environment answer.**

This sounds obvious and is violated constantly, because vendoring is locally rational: a copy
inside the Workspace is guaranteed present, guaranteed the right version, and needs no
coordination. The costs land elsewhere and later.

**The evidence.** On the audited machine, two independent Workspaces vendored tools that were
already installed and already on `PATH`. Verified by full SHA-256 rather than by name and version:

| Tool | Vendored | On PATH | Match |
|---|---|---|---|
| `ffmpeg.exe` | `ad8f211bc894755e…` | `ad8f211bc894755e…` | identical |
| `ffprobe.exe` | `9df3b0b5275e8309…` | `9df3b0b5275e8309…` | identical |
| `rclone.exe` | `3ac0dba3a883555f…` | `3ac0dba3a883555f…` | identical |
| `pandoc.exe` | `098af4570d89423c…` | `098af4570d89423c…` | identical |

Creation dates settle the direction: the `PATH` copies predate the vendored ones by three to
twenty-four days. **~795 MB of byte-identical duplication** — measured across the four vendored tools in a single
Workspace — **created after a discoverable copy already existed.** *(Not to be confused with the
~6 GB figure in SOP-7 §6, which is a different scope: total retained archive volume across the
backup's full retention set, not on-disk duplication.)*

**Why this is a Charter principle and not an SOP step:** the second-order costs are what hurt.
A vendored copy is invisible to every other Workspace, so the *next* project duplicates it too.
It drifts from the system copy silently. And it invites the anti-pattern in C14.

---

### C14 — Never resolve a binary through another Workspace's private directory

**If a tool is not discoverable, the correct response is to fail loudly and say so — not to reach
sideways into a neighbour.**

Observed on the audited machine:

```bash
RCLONE_BIN="${RCLONE_BIN:-D:/…/Workspaces/<OtherWorkspace>/bin/rclone.exe}"
```

One Workspace's publish flow defaulted to a binary inside a *different* Workspace's private `bin`.
The tool it needed **was on `PATH`, byte-identical**; the author had been handed a path by
precedent and never searched.

**Footprint, stated by composition — the headline count misleads in both directions:**
**one live script** (2 occurrences), plus three frozen version snapshots, six documents, and **six
permission-allowlist entries** — **20 references across 11 files.** A reader told "eight references
across four files" pictures four live consumers; there is one. **The allowlist entries earn their
mention: they are how a hardcode survives review, because each one silently ratifies the path.**

**Why it matters:** the dependency is invisible from both ends. The owner of the borrowed directory
does not know they have a consumer — in the audit, they reported the file as having "zero
references" because they measured from inside their own tree. And it breaks the moment the
neighbouring Workspace is renamed, archived, cleaned, or relocated, at run time, in a scheduled
job, quietly.

**The rule to write down:** never a sibling-Workspace path at any tier of a resolver. Failing with
*"install X or set X_BIN"* is strictly better than silently succeeding against a neighbour's copy.

### ⚠️ The routing-index form is worse than the code form — it *manufactures* the failure

A **documentation** route saying *"use `<tool>` at `E:\…\<OtherWorkspace>\bin\<tool>.exe`, invoke by
full path"* is not a record of Mode A. **It is a Mode A generator.**

It produces the failure on a schedule, for every future author, **through the one file staff are
told to read *before* they go looking** — converting a one-time lapse into a standing instruction to
repeat it. A hardcode in one script is an author's mistake; the same path in a routing index is
**institutional**. Audit indexes for these, not just code.

### The narrow, self-closing exception — because a rule with no legitimate path gets ignored

C14 stated absolutely would have made **the most compliant Workspace in the audit its first
violation**: that Workspace routes to a neighbour's `yt-dlp` because the tool is genuinely on no
`PATH` and no alternative exists today. A rule that brands a correct, unavoidable choice as a
violation teaches readers the rule is aspirational.

⚠️ **Read that case prospectively, not as a certificate.** It is the kind of dependency that must
remain permissible — *the need is legitimate* — but the artifact as it stands **does not satisfy the
conditions below**, and saying otherwise would hand adopters a worked example that fails the rule it
illustrates. Measured against the four: unreachability holds in substance (`where.exe` confirms it);
it **is** registered in the manifest as a labelled coupling, never as a resolvable path — **condition
3 is met** — while the reference itself carries none of the proof, the do-not-copy warning or the
recovery instruction that conditions 1, 2 and 4 require *beside it*, and is in fact headed
*"Retrieval recipe"*, framed for reuse.

**One of four — and the three failures all have the same single cause: the borrower's reference was
never amended.** That is worth stating plainly rather than as a score, because it tells an adopter
the outstanding work is one edit to one file, not four separate obligations. The exception exists
because the *need* is legitimate, not because the current artifact is compliant — and the gap
between those two is the work the conditions name.

⚠️ **Note what the lender/borrower split looks like here, because it is the C14 harm in miniature:**
the *lending* side is fully discharged and the *borrowing* side is untouched. That is the same
"invisible from both ends" asymmetry the prohibition opens with — the owner of the borrowed
directory has done the visible thing, and the consumer who actually depends on it has not.

This matters more than it looks, because the permitted case and the condemned one are near-verbatim.
The routing-index anti-pattern above condemns a doc route reading *"use `<tool>` at
`E:\…\<OtherWorkspace>\bin\<tool>.exe`, invoke by full path"* as **institutional Mode A**. The live
artifact here reads *"the pipeline uses a bundled `yt-dlp.exe` (not on global PATH — invoke by full
path)."* **Nothing in the wording distinguishes them.** What separates a Mode A generator from a
legitimate exception is not how the sentence reads — it is whether the four conditions are carried
alongside it. A reader who cannot tell which rule governs is looking at an artifact that has not yet
been amended.

**So a sibling-Workspace reference is permitted only when ALL of the following hold.** Note that
they are discharged in **two different places**: condition 3 is satisfied in the tools manifest,
the rest must be satisfied **at the reference itself**. A scorer checking one artifact will find
half a compliant exception and conclude it is compliant.

1. the tool is **provably not otherwise reachable, and that proof is written down beside the
   reference as the test that cancels the exception — stating what a reader must do when it flips.** Proven by a `PATH` query and a **direct
   listing of the shared tools directory** — *not* by absence from the manifest, which SOP-7 §5
   shows can omit exactly the undiscoverable tools this test is about.

   > 🔑 **The proof and the expiry are the same command.** `where.exe <tool>` returning nothing is
   > what justifies the exception; the same query returning a hit is what voids it. Writing it down
   > once does both jobs — and a recorded, runnable test is what SOP-7 §1 requires instead of a
   > date, because *"provisional pending X"* rots into permanence when nobody can tell whether X
   > has happened. An unrecorded proof decays exactly the same way: it was performed once, by
   > someone, at a time nobody wrote down.

2. it carries **"do not treat this as a pattern to copy"**, so it does not propagate; and
3. it is **registered in the tools manifest as a known coupling** — in a coupling/exception field,
   **never as the tool's resolvable canonical `path`**, and labelled so that no reader and no
   generator can treat it as a route (per SOP-7 §5: record the `PATH` resolution as canonical and
   list anything else separately, labelled). This makes the dependency visible from the lender's
   side too — the side that otherwise measures "zero references" and concludes nothing depends on
   it — without turning the discovery artifact into the thing that propagates the coupling; and
4. **its absence fails loudly and by name** — no fallback, no degradation to a default, and the
   failure identifies the exception and the recovery rather than just the missing file. State this
   as a *property*, because the two artifact classes satisfy it differently:
   - a **resolver** — anything with a default, fallback, or env-overridable path such as
     `RCLONE_BIN="${RCLONE_BIN:-…}"` — must implement it explicitly: *"yt-dlp resolved via
     `<Workspace>\bin` per the C14 exception; that path no longer exists — install yt-dlp on `PATH`
     or set `YTDLP_BIN`"*;
   - a **literal non-resolving invocation** — an absolute path in a documented recipe or a direct
     call — already fails loudly when absent, because the shell does it. What it lacks is the
     *naming*: `"The system cannot find the path specified"` tells the reader nothing about the
     exception or the recovery. So the recipe must **carry the recovery instruction beside the
     command.**

   ⚠️ **Do not write this condition as "fails at run time."** A routing index or a documented recipe
   has no run time — and those are exactly the artifacts C14 and T2 govern. A condition phrased for
   resolvers gives the routing-index case no passing state at all, which is a rule that cannot be
   followed rather than a rule that is strict.

That makes the exception **visible and self-closing** rather than silent, which is the whole thesis.
It also stops the exception being the thing that quietly voids the rule: *there will always be a tool
that has not moved yet*, and a rule with no legitimate path for it gets ignored rather than followed.

⚠️ **Note what this clause is:** the permissive half of a rule, added late — precisely the shape this
document warns about twice elsewhere.

**This clause was four conditions, became five under adversarial review, and is four again — and
the round trip is worth more than the text.** The original four were all documentation and
registration controls. C14's "Why it matters" names *two* harms — invisibility to the lender, and
quiet breakage when the neighbour is renamed or moved. Mapping each condition to a harm showed that
every one of them addressed the first, and **nothing addressed the second**: the exception made the
coupling legible to readers and self-closing over time while leaving the failure exactly as the
prohibition describes it. C14's own headline had already stated the missing condition — *fail
loudly* — and the conjunction did not carry it. That became the loud-failure condition, and a second
review then found that the registration condition, as first written, instructed the very act SOP-7
SOP-7 §5 catches as a Mode A generator.

**Then the count came back down.** Two of the five turned out to be one: the `PATH` query that
proves unreachability *is* the runnable test that cancels the exception. Merging them removed no
coverage, because **the harm map did not change** — and by the rule stated below, a condition that
maps to no additional harm is decoration, however diligent it looks. *Adding conditions is how a
clause is strengthened; noticing two of them are the same artifact is how it is finished.*

> 🔑 **Do not ask whether an exception is strict enough; that question is answerable with confidence
> in either direction. Enumerate the harms the prohibition names, map each condition to a harm, and
> look for a harm with no condition mapped to it — that is the gap. A condition mapping to no harm
> is decoration.** A conjunction feels rigorous because it is long, and four conditions against a
> two-part harm can still be four answers to the same half. **Counting conditions measures effort;
> mapping them measures coverage.**

---

### C15 — Anything running elevated resolves binaries by absolute path, never by PATH

**A privileged process must not let a writable directory decide which executable it runs.**

This is the finding that most justifies the whole exercise, and it was latent for weeks.

A nightly backup running as SYSTEM contained:

```powershell
try { $rr = ((& rclone listremotes 2>$null) -join ', ') } catch { $rr = '(n/a)' }
try { $ol = ((& ollama list 2>$null) -join ', ') }        catch { $ol = '(n/a)' }
```

Bare names, full `PATH` resolution, under SYSTEM. The directory proposed for shared tools sat under
a root carrying `Authenticated Users: Modify` inherited from the volume root. **Machine `PATH` +
that ACL + those two lines = any authenticated user plants an executable and the 03:00 job runs it
as SYSTEM.**

**The subtle part, and the transferable lesson:** the defect was *dormant*, and dormant for the
exact reason this Standard section exists to remove. The tools lived only in the user's `PATH`, and
SYSTEM cannot see user `PATH`, so both calls failed into their `catch`. **Improving discoverability
at machine scope would not have added a vulnerability — it would have armed one.**

The recovery document those lines produce had read `(n/a)` in **every archive sampled** — and the
code path that produced it was **unconditional**, so there is no run in which it could have
differed. A second defect, invisible until someone opened an archive.

*(Note the form of that claim. "Every archive ever generated" would be an extrapolation dressed as a
measurement — two archives were actually opened. **A verified sample plus a structural argument is
both honest and stronger than an unverifiable universal**, because the structural half is what
actually establishes the universal.)*

⇒ Two rules.

**1. Elevated code resolves by absolute path — into a directory where write is granted ONLY to
SYSTEM and Administrators, ownership is held by SYSTEM or Administrators, verified against the
EFFECTIVE DACL including inherited ACEs, with no parent in the path granting Full Control to a
wider principal.**

That is deliberately long. Each clause is a way the short version fails:

- **State it positively, not as "unprivileged users cannot write."** That is a **denylist** — a
  negative over an open set of principals. To check it you must enumerate everyone and confirm none
  has write, and **any ACE added later silently violates it with no signal.** The positive form is
  checkable against a fixed list in one read. *(This Standard argues elsewhere that allowlists beat
  denylists; it should apply that reasoning to itself.)*
- **Ownership is decisive and is the clause most often missed.** An owner holds implicit
  `WRITE_DAC` and can re-grant themselves anything, so **a perfect DACL owned by an unprivileged
  account is not a control at all.** Verified on the audited machine: the hardened tools directory
  was owned by `BUILTIN\Administrators`; its sibling holding the tool manifest was owned by a normal
  user *and* carried an inherited `Authenticated Users: Modify` — failing on **two** counts, not one.
- **Inheritance is how the original defect arrived.** The `Authenticated Users: Modify` ACE was
  **inherited from the volume root** — nobody granted it on that directory, and it looks
  unremarkable in isolation. So check the *effective* DACL, and **break inheritance when hardening.**
- **The parent chain matters, though less than it first appears.** A parent granting only Modify does
  **not** permit renaming or replacing a hardened child: Modify excludes `FILE_DELETE_CHILD`, and
  deleting the child requires `DELETE` on the child itself, which Read+Execute does not grant. But a
  parent granting **Full Control** to a wider principal *would* allow exactly that swap.

⚠️ **"Absolute path" alone is necessary and NOT sufficient, and the incomplete version of this rule
is the more dangerous one, because it reads as satisfied.** An absolute path pointing into a
user-writable directory passes the rule as usually stated while remaining **fully exploitable** —
the attacker no longer has to win a `PATH` race, they simply overwrite the file at the path you
carefully specified. The `PATH` lookup was never the vulnerability. **Writability of the resolved
target is.**

So the check has two halves, and the second is the one that gets forgotten:

- Is the path absolute? *(the easy half)*
- **Can any unprivileged process write to that file, or to any directory on the way to it?**
  *(the half that decides whether the rule did anything)*

Harden the target directory — break inheritance, remove write for ordinary users — **at creation**,
and treat an unhardened tool directory as equivalent to a `PATH` lookup. On the audited machine
the shared tools directory qualifies *because it was explicitly hardened*; its sibling `bin\`, which
inherited `Authenticated Users: Modify` from the volume root, would **not** — and `bin\` is where
the tool manifest lives.

### The same rule on POSIX — and one clause is *stricter* there, not weaker

The rule above is stated in Windows vocabulary because that is where it was measured. The property
is platform-independent; the mechanism is not, and translating it word-for-word gets one clause
backwards.

**The equivalent check:** resolve by absolute path, then require that the target file **and every
directory on the path to it** are owned by `root` (or the dedicated admin account that owns tooling)
with **no group-write and no other-write bit anywhere on the chain**. `0755 root:root` passes;
`0775 root:staff` does not, and neither does a correct binary under a `0777` parent.

Clause by clause, against the Windows form:

- **Ownership is decisive for the identical reason.** An owner can `chmod` at will, so a perfect mode
  on a file owned by an unprivileged account is not a control — the same substance as `WRITE_DAC`.
- **Inheritance HAS a POSIX analogue and you must check it.** Mode bits are not the whole permission
  set. Linux **default ACLs** (`setfacl -d -m …`) are inherited by every entry created beneath a
  directory — the same mechanism as Windows inheritance with different syntax — and macOS ACLs carry
  explicit `file_inherit` / `directory_inherit` flags, deliberately modelled on the NFSv4 scheme.
  **A `+` at the end of the mode string in `ls -l` means an ACL is present and the mode bits are not
  the answer.** Enumerate with `getfacl <path>` on Linux or `ls -le <path>` on macOS, **on every
  component of the chain**.
- 🔑 **The parent chain is STRICTER on POSIX, and this is the clause that inverts.** The Windows
  analysis concludes a parent granting only Modify cannot replace a hardened child, because Modify
  excludes `FILE_DELETE_CHILD`. **POSIX has no such protection: write *and search* permission on a
  directory authorises `unlink` and `rename` of any entry it contains, and the entry's own mode and
  owner are never consulted.** A perfectly hardened `root:root 0755` binary sitting in a
  group-writable directory can be deleted and replaced by anyone in that group. The sticky bit
  (`chmod +t`) narrows removal to **the entry's owner, the directory's owner, or a privileged
  process** — note the middle one: a shared tools directory is often owned by an admin-ish
  non-`root` account, and that account can still replace `root`'s binary. Worth setting; **a
  mitigation, not a substitute for correct ownership up the chain.**
- **Resolve symlinks before you judge the path.** A symlink inside a writable directory silently
  redirects the absolute path you specified — the `PATH`-race attack, reintroduced through a path you
  believed was pinned. Check the target as `realpath` returns it, not as written.

**On Linux, one command answers most of the chain:** `namei -l /path/to/tool` prints owner and mode
for every component and follows symlinks to the target. Two limits worth stating, because a check
believed complete is worse than one known partial: **`namei` is `util-linux` and is not present on
macOS by default** — there, walk the chain with `ls -lde` per component — and **it does not surface
ACLs**, so it never answers the inheritance question above on its own.

⚠️ **Elevated contexts carry their own `PATH` regardless.** `cron` runs with a minimal `PATH`,
`systemd` units with whatever `Environment=` supplies, and `sudo` substitutes `secure_path` from
`sudoers` **where that option is configured** — which is a hardening default, **not** a reason to
resolve by bare name. `secure_path` constrains *which* directories are searched; it does not
validate that they are safe, so a writable entry in it leaves bare-name resolution exploitable — and
it applies to `sudo` only, not to setuid binaries, `cron`, or `systemd` units. The rule is unchanged:
absolute path, verified target, on every platform.

**2. When you make something discoverable, audit what becomes reachable that was not reachable
before.**

---

---

### C16 — A control you will not maintain is worse than one you declined

**Adopting a control is a commitment to keep it true. Where you will not make that commitment,
decline deliberately and say so.**

A half-implemented control reads as coverage to everyone who comes after, including you. The
mechanism is C7's, one level up: a status signal from a process that does not actually check is
worse than no signal **because it suppresses investigation** — and a control *believed* to be in
place suppresses investigation of that exposure in exactly the same way. Declining leaves your
picture of your own exposure accurate, which is worth more than a control you will not maintain.

Recording the decline is what prevents this, not what causes it.

⚠️ **And if the half-measure is already installed, recording the decline is not enough — remove
it.** Paperwork does not un-mislead an artifact. A control left half-configured in the tree goes
on reading as coverage to whoever finds it next, whatever the decision log says; the decline is
only honest once the thing it declines is gone.

⚠️ **This is a comparison against the half-measure, not against doing it properly.** If full
implementation is genuinely on the table, that is the option to price first. But *on the table*
means **owned, scheduled and dated by a named person** — the same bar as a `blocked` unblocker,
and for the same reason: a condition shaped like an intention (*"when we have time"*) is exactly
the one that never fires. **Until it lands, this criterion still applies and the half-measure
still comes out.** A scheduled fix does not stop an installed half-control reading as coverage in
the meantime, and the fix is the thing most likely to slip. Intent is not coverage. And the
question is never **only** *"is this a real risk?"* — almost
everything a rubric surfaces is, and that answer alone settles nothing in either direction. It is
*"what does this cost, what does it buy, and what would change the answer?"*

*Claim status, following the provenance-note pattern C8 applies to itself: the failure mode is
argued from C7's mechanism and from one recorded instance, not from a survey. Adopt it because
the reasoning holds.*


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

   *A dated, non-normative list of which tools load which filename is in §16. It is a snapshot of a
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
Revisit if: <the condition that reopens this>
Evidence:   <how it was verified, or "asserted, unverified">
Decided by: <name> — human | agent
Agent had:  <what context the agent was working from, if an agent decided>
```

**Rejected alternatives are mandatory.** Without them, a future reader re-opens a settled question
or re-tries a known failure.

**`Revisit if:` is mandatory on a decline** — it is what the `accepted` verdict is checked
against. A re-raise condition must name an event a third party could notice without asking you.
If checking whether it has fired requires your judgement, it is not a trigger: *"revisit if
circumstances change"* is not a re-raise condition.

> **Provenance note, stated because this Standard demands it of others.** Both halves of that
> paragraph are **local extensions**. The established practice (NIST SP 800-53 RA-7) requires a
> risk acceptance to carry a justification **and nothing further** — no revisit condition, no
> review date, no trigger. Requiring `Revisit if:` at all is ours. So is the
> **third-party-observable test**: the nearest source (NIST SP 800-137) supports continuous
> monitoring of accepted risk but says nothing about who must be able to notice the trigger.
> Both are argued from the *designed-around risk* failure mode (§12), not cited. **Do not present
> either as established practice** — adopt them because the reasoning holds. The same test is
> reused for `blocked`'s unblocker and for `?`'s evidence statement in §11, and inherits this
> label wherever it appears.

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

## 10. SOP-7 — Standing up shared external tools

### 1. Establish the convention *before* the directory

The directory is the mechanism; the convention is what makes anyone use it. In the audit, **every
measured duplication happened despite the tool being discoverable.** A shared location without a
stated norm reproduces the same failure against a new path.

Put this where staff read before writing scripts — the Workspace charter or its routed library, not
a README nobody opens.

**What makes such an index worth opening**, from the one written for the audited machine:

> Nearly every route in it is **a rule someone could plausibly *simplify* into a defect** — pin this
> binary to System32, enforce the allowlist on both paths not one, don't "just add a module", don't
> "correct" that `%APPDATA%` reference.
>
> **A library that only says where things are is a directory listing. One that says which apparent
> tidy-ups are actually regressions is worth reading first.**

Two practical constraints learned writing it:

- **Route, never reproduce.** A summary of the convention inside the index will drift from the
  convention. Link, so the two cannot disagree.
- 🔴 **State the CURRENT state, not only the target state — or the convention authorises breakage.**
  In a Workspace that has not yet migrated, a route saying *"resolve by bare name via `PATH`"* tells
  a newcomer that `PATH` is authoritative **while the scripts still call vendored copies through a
  local resolver.** Someone helpfully "tidying" a resolver call into a bare name would have broken
  a dozen call sites. The index must say plainly: *the migration is planned, not done; do not
  convert these on your own initiative.* Revise when it lands.
  **This is the permissive-half failure wearing new clothes** — an aspirational rule, stated without
  its current exception, read as an instruction.
- 🔑 **Give a provisional route an expiry TEST, not an expiry date.** *"Provisional pending X"* rots
  into permanence the moment nobody remembers whether X happened. Instead, hand the reader a
  one-command check they can run **now**:

  > ⚠ **PROVISIONAL** — this cross-workspace absolute path is correct *only while* the tool is off
  > `PATH`. **If you are reading this and `where.exe <tool>` returns a hit, this clause has expired
  > — fix the route.**

  **The reader cancels it, rather than it silently ageing out.** Cross-reference the rule that should
  replace it, so someone who trips the expiry lands on the convention instead of inventing a fix.
- ⚠️ **A hub or Home workspace may legitimately differ — do not standardise it by reflex.** In the
  audit the project Workspaces consolidated to one canonical location while the **Home workspace was
  deliberately excluded**: it serves a different function, and its index routes material arriving
  from outside rather than describing a project tree. **Record the exemption in the exempt file
  itself, with its reason** — otherwise the next person tidying for consistency finds it, assumes it
  was missed, and "fixes" it. A stated exception survives; an unexplained one gets normalised away.
- ⚠️ **Advertise the convention centrally, or the merge will simply re-diverge.** On the audited
  machine, three of four Workspaces kept their index in the non-canonical location — **not because
  anyone overrode a known rule, but because the rule lived in one Workspace's charter and nowhere
  else.** Under-advertised, not ignored. Consolidating the files without publishing the convention
  fixes the symptom and leaves the cause: *a convention nobody can discover gets re-derived wrong by
  the next person, and documentation that cannot be checked becomes a fossil.*
- ⚠️ **Check that your links resolve from where they are written.** A workspace-local index whose
  WikiLinks resolve against a *local* documents folder will render a link to a Home-level document
  as **a dead link that looks live** — and the reader concludes the *document* is missing rather than
  that the *link* is wrong. Use an absolute path across such a boundary. This was caught in review
  after the broken form had already been issued to three workspaces.
- 🔑 **Declare the resolution base in the file; do not leave it implicit.** The subtler defect found
  during consolidation was not a broken link — it was **relative paths whose base was never stated
  and merely happened to be correct.** While the index sat beside the tree it described, `docs/…`
  resolved by coincidence. Moving the index one directory down turned an unstated base into an
  actively misleading one: a reader could reasonably resolve it against the index's own directory
  and find nothing.

  **Prefer a stated base to a computed one.** One header line —
  *"paths below are relative to the workspace root `<path>`, not to this file's directory; anything
  outside the workspace is given as a full absolute path"* — beats rewriting every route with `../`
  prefixes, which is brittle and breaks again on the next move.

  ⚠️ **This is structural wherever the canonical index lives below the tree it describes**, so put
  the base declaration in the **scaffolding template**, not in each workspace's copy. Otherwise every
  workspace rediscovers it independently, and the ones that don't ship a latent defect that activates
  the next time anything moves.

  🔴 **But verify the template's declaration before trusting it — in the audit it was FALSE.** The
  scaffolding declared that WikiLinks resolve under a local `Docs/` directory. In **two of the
  workspaces checked that directory existed and was completely empty**, every routed document living
  elsewhere. So a WikiLink in those files had **never been able to resolve — before or after any
  consolidation.**

  Worse, and the detail worth carrying: **the canonical file's own pre-existing route was already
  broken by its own declared base**, in a file others were being told to merge *into*. **The
  destination of a consolidation is not automatically the correct one.** Audit it with the same
  suspicion as the thing you are merging in — an index that has never been exercised looks identical
  to one that works.

> **Unprivileged code:** resolve external tools **by bare name via `PATH`**.
> **Elevated code: never `PATH`.** Resolve by **absolute path into a directory unprivileged users
> cannot write** (see C15 — this is one rule, not two).
> **Never** hardcode a path into another Workspace. If a tool is not on `PATH`, say so rather than
> reaching sideways.

⚠️ **The elevated carve-out is inside the box deliberately.** This box is the passage most likely to
be copied into someone's charter, stripped of the surrounding document. An earlier draft said only
*"resolve external tools by bare name via `PATH`"* — which **contradicted C15** and would have
instructed adopters to build the exact privilege-escalation this Standard exists to prevent. A
quotable rule must carry its own exceptions, because **quotation is how rules travel and context is
what gets lost in transit.**

### 2. Classify the failure you are actually fixing

Discoverability is three distinct problems. Naming them prevents building the wrong fix:

| Mode | Failure | Fixed by |
|---|---|---|
| **A** | Precedent handed the author a path; they never searched | **Convention** |
| **B** | The author searched, and the tool genuinely was not discoverable | **Shared directory on PATH** |
| **C** | The author never knew the tool existed, so never searched | **Manifest** |

> **Provenance note, stated because this Standard demands it of others.** The Mode C row — *that
> a manifest improves discovery* — is a **local extension**. A deliberate search found no source
> establishing that a tool inventory reduces re-solving, and the structural argument below is
> what carries it, not evidence. The three-mode split itself is a classification of three
> observed incidents on one machine; it is offered because it makes the *fix* fall out, not
> because the population is large enough to generalise from. Adopt it because the reasoning
> holds.

**The claim that matters here is structural, not statistical — take this rather than the counts:**

> A shared directory on `PATH` only ever helps an author **who is already searching for a tool**.
> **Mode A never enters the search path** — precedent supplied an answer before the question formed.
> **Mode C never enters it either** — you cannot search for a name you have never heard.
> **Both bypass the mechanism by construction. Only Mode B is downstream of it.**

That explains *why* the observed counts fall as they do instead of asking you to trust them:
**copying is cheaper than searching, so authors copy.** Mode A is what happens **instead of**
searching, not a failure of searching. A directory that serves only searchers will always miss the
modes that skip searching.

**The practical upshot for an adopter — and it is prospective, not a post-mortem of someone else's
machine:** build the directory for Mode B, **expect your observed incidents to be A and C, and do
not read that as the directory failing.** It is serving the one mode that requires someone to have
already gone looking.

*(Audit figures, for provenance only — the argument above does not depend on them. **Three
classified incidents: two Mode A, one Mode C, zero Mode B.** The unit is an incident, not a tool or
a file. **Classification requires knowing whether the author searched, which is recoverable only by
self-report** — vendorings whose rationale could not be recovered are excluded from these counts, so
this is not the full population of duplications. Zero Mode B means **no search failed**, not that
nobody searches: the one search actually run succeeded.)*

Mode C is not the cheapest to ignore. The audited instance was a tool sitting unnoticed in the host
application's own `bin`. Not knowing it existed, the author reached for a general-purpose
alternative — **which does not execute JavaScript, so the source's JS-toggled tables were dropped
entirely.** Not degraded: absent. Caught only because extraction completeness was independently
verified against the raw source.

*(Supporting figures, deliberately not stated as a percentage of the document: the correct
extraction recovered **35.8 KB of text**; the general-purpose tool produced **3 KB**. Quoting
"94% of a 55 KB document" would compare **markup bytes to text bytes** — and stripping markup is
what the tool is supposed to do, so that framing conflates correct behaviour with data loss and
hands a hostile reader a free rebuttal. **The qualitative claim is the defensible one.**)*

⚠️ **State the counterfactual honestly, because the tempting version is not supported:** it is
**unknown** whether the unnoticed tool would have handled that particular source — the content was
JS-toggled and might have defeated it too. **The cost of Mode C is not that the better tool was
passed over. It is that the author never got to evaluate it.** That claim needs no counterfactual
and cannot be rebutted by pointing out the alternative might also have failed. **Mode C cost data,
not disk.**

### 3. Site the directory outside the backup, structurally

Prefer a location that was **never** a backup source over one carrying an exclusion. An exclusion
is a config line that can be reverted, lost in a migration, or silently stop matching. A location
outside every source needs no config at all and cannot be tidied away.

Do not site it inside a Python virtual environment or couple it to one Workspace's runtime; venvs
get rebuilt, and a machine-wide tool surface should not inherit a single project's lifetime.

### 4. Register on user PATH, not machine PATH — and harden the ACL at creation

Per C15. Machine `PATH` plus a user-writable directory is an escalation chain. If machine scope is
ever genuinely required, both of these are prerequisites, not alternatives: break ACL inheritance
and remove `Authenticated Users: Modify`, **and** eliminate every bare-name invocation from
elevated code.

Harden at creation. Retrofitting permissions to a directory already in use is a migration.

### 5. Back up the manifest, not the binaries

Third-party tools are large, usually re-downloadable, and contain **no irreplaceable user data**.
They are the worst possible archive payload. But excluding them opens a rebuild hole, and the answer
is not to archive them anyway:

> **The tools directory holds bytes you can *usually* re-fetch. The archived manifest holds the
> record of *what* to re-fetch — and, via the SHA-256, the means to *verify* you got the same
> thing.**

A manifest of name, version, version-query command, package ID, install path, SHA-256, size,
`pinned: true|false` **with the reason and its owner**, and a **`coupling` field for any C14
exception** is kilobytes.

⚠️ **That last field is not optional decoration — without it C14's exception cannot be complied
with.** C14 requires a sibling-Workspace reference be registered *as a labelled coupling and never
as the tool's canonical `path`*, and a schema whose only location slot is `path` leaves nowhere else
to put it. On the audited machine the evidence was already visible: the manifest carried a coupling
record for a *different* tool by smuggling it into free-text notes — *"<publish script>:63 HARDCODES
this absolute path. Moving this binary breaks that script."* **A record forced into prose because no
field existed is the schema telling you what it is missing.** Site it somewhere already
archived. It costs no runtime.

⚠️ **Do not read "re-downloadable" as a property of the tool.** It is an assumption about a third
party that the manifest neither controls nor measures. A manifest makes a binary *identifiable* and
a re-fetch *verifiable*; it does not make the binary *obtainable*. This bites hardest exactly where
SOP-7 §9 says the build is load-bearing: distributors routinely retain only recent releases, so **the
pinned tool is simultaneously the one most worth archiving and the one this section argues hardest
to exclude.** Where a pin is genuinely load-bearing the manifest is *not* sufficient — archive that
one binary, or record a retrieval source you control. **Copy that binary into a location already
inside a backup source — alongside the archived manifest — rather than adding an inclusion rule that
reaches back into the tools directory.** SOP-7 §3's structural property survives only if the tools
directory itself stays unreferenced by backup config; an inclusion rule reaching into it is the
config line SOP-7 §3 argues against. The exclusion recommendation stands for the unpinned majority, which
is where it is actually true.

**The manifest must cover the host application's own bundled tools**, not only the shared
directory. That is where Mode C lives.

⚠️ **And the manifest must not itself teach the anti-pattern — this was found live.**

The audited generator resolved each tool to **first-found** and recorded that as the canonical
`path`. For four tools it therefore recorded **a private workspace copy** as the answer, while
simultaneously flagging `onUserPath = true`:

```
ffmpeg   onUserPath=True  pinned=True  path=E:\...\<Workspace>\bin\ffmpeg.exe
rclone   onUserPath=True  pinned=True  path=E:\...\<Workspace>\bin\rclone.exe
```

So a reader consulting the manifest to *"find the existing tool before installing another copy"* —
the exact behaviour the manifest exists to produce — **is pointed into another Workspace's private
`bin\`**, which is the move C14 forbids and precisely how the audited hardcode came about. *The
discoverability artifact was reproducing the failure it was built to prevent.*

⇒ **When a tool is on `PATH`, record the `PATH` resolution as the canonical path, and list any
vendored duplicate separately, labelled as a duplicate.** First-found is the wrong rule.

⇒ **Audit the manifest for omissions against the tools that cannot be discovered any other way.**
The same generator omitted one of only two genuinely *undiscoverable* tools on the machine — the
highest-value entry it could have carried. (**Undiscoverable is narrower than off-`PATH`**: the
sweep found three tools off `PATH`, but one of them installs to a conventional location a reader
would think to check. Off-`PATH` is a fact about resolution; undiscoverable is a fact about whether
anyone can find it, and only the second is what the manifest exists to fix.)

### 6. Measure the cost against the schedule, not the disk

In the audit, disk was never the constraint — 15 TB free against roughly 6 GB of retained
duplication. **The binding constraint was the nightly job's abort window**, because the mirror is a
delta but the archive is rebuilt in full every run.

⚠️ **Measured vs projected, kept distinct — this section's headline numbers are PROJECTIONS.**

| Quantity | Basis |
|---|---|
| Compression of `ffmpeg`, `rclone`, `yt-dlp` | **measured** at the tool's real setting |
| Compression of `ffprobe`, `pandoc` | **extrapolated** at the measured `ffmpeg` ratio |
| **~200 MB added per archive**, **~16 min added compression**, ~6 GB retained | **derived from that extrapolation — projected, not measured** |
| ~26-minute margin (18 min 24 s run against a 03:45 abort) | **measured**, from the previous night's run |

The trade is decided by the *measured* margin against a *projected* cost, and that asymmetry is the
honest way to state it. **Re-measure before relying on the projection** if the decision is close.

That job's failure mode is *total* — an abort produces no archive at all. Halving the margin of an
unattended job to store mostly re-fetchable tools is a bad trade regardless of free space. (Subject
to the SOP-7 §5 caveat: a load-bearing pinned build is the exception that earns its archive slot.)

Also **measured**, and counter-intuitive: **do not assume binaries compress.** Ratios ranged from
4.21:1 down to **1.02:1** for a packed PyInstaller bundle — which is why extrapolating one tool's
ratio onto another is exactly the move that needs flagging.

### 7. Sequence the migration so rollback stays cheap

1. **A complete cross-workspace reference sweep, with termination verified.** In the audit
   **three** separate sweeps timed out and returned partial results, and a partial result was
   briefly mistaken for evidence of no coupling. Scope to executable file types; check the exit
   code; never trust a quiet search.
2. **Repoint borrowed references first** — deleting a binary that a neighbour still resolves is
   the one irreversible step.
3. **Switch scripts to bare-name resolution and verify green.**
4. **Only then delete the vendored copies.** Deleting first turns rollback from a revert into a
   re-download.
5. **Restart long-lived processes.** A running process holds the `PATH` it started with; scheduled
   workers will not see a new entry until they restart.

### 8. Do not oversell consolidation where formats differ

A shared directory dedupes *bytes*, not *capability*. In the audit, two Workspaces held ~2.4 GB of
speech-to-text assets that looked like duplication and were not: one CTranslate2, one ggml,
**mutually unloadable**. Near-zero recoverable overlap.

The honest pitch there is **discoverability for the next Workspace** — which today would find
nothing and download a third copy — not savings on the current two. Claiming otherwise sets up a
disappointment that discredits the rest.

### 9. Pinned versions survive consolidation, or the pin was a lie

If a Workspace's DR document records `ffmpeg 8.1.2` as a reproducible fact, a shared copy that
shadows it with a different build **silently makes that document false**. Either the shared copy
carries the pinned version, or the DR document is rewritten to point at the shared location with
its own verification step.

Watch resolution order specifically. A *missing* tool fails loudly; a **different** tool fails
quietly. One audited pipeline degraded silently to a fallback known to be wrong by up to 2.6× if
the primary produced no parseable output — an empty result, not an error.

**And assert behaviour, not version strings.** Exact-version equality turns routine upgrades into
mid-run hard stops. Minimum-version passes everything *newer* — precisely the direction a silent
semantic change arrives from. Neither proves a destructive subcommand still means what it meant.
Prefer bounding the blast radius: re-verify after the first destructive operation rather than
applying an unverified assumption N times in a loop.

### 10. Upgrading a shared tool is a consent protocol, not a maintenance task

The moment a tool is shared, upgrading it stops being a unilateral act. A version bump that is
routine for one consumer can be breaking for another, and the consumer who breaks usually finds out
at run time, in a scheduled job, after the person who upgraded has moved on.

**Announce through the manifest, then require an explicit answer from each consumer.**

1. A new version becomes available → **announced in the manifest.**
2. Each consuming Workspace **evaluates impact against its own processes**.
3. Each records **acceptance, or a documented issue.**
4. **Unanimous acceptance** among consumers → the tool is updated.
5. **Any issue raised** → escalate to the human owner for a decision.
6. **Timeout with missing responses** → escalate to the human owner.

**Silence is not consent.** A timeout must escalate, never auto-approve. This is the load-bearing
property: the failure mode being prevented is an upgrade that nobody objected to *because nobody
looked*.

Suggested windows, scaled to the cost of waiting rather than the cost of reviewing:

| Severity | Window | Meaning |
|---|---|---|
| **Critical** | 6 h | Active security fix, or a live issue |
| **Urgent** | 24 h | Fixes a breaking bug or a real risk |
| **Non-elevated** | 48 h | Everything else |

**Seven things that decide whether this works in practice:**

- **The clock cannot start before detection.** A 6-hour window against a weekly version check burns
  a week before the six hours begin — and still reports "6 h". **Detection cadence must be at least
  as tight as the tightest window**, or the number is decoration. If you cannot detect a critical
  release within the critical window, publish the cadence you can actually sustain.
- **Prefer pull over push.** A consent window that depends on a notification reaching an idle agent
  inherits every delivery failure of the messaging layer. Have each consumer's own scheduled task
  read the manifest and react on its own cadence; push may supplement, never carry it.
- **"All consumers" must be computable.** Unanimity is undefined without a maintained per-tool
  consumer registry — and only consumers should count. A Workspace that never touches the tool must
  not be able to block it by silence.
- **A pin is a standing objection.** Where a Workspace pins a version as a reproducibility fact, a
  new release should auto-register an issue that only the pin-holder can clear. Requiring a hand
  response to every routine bump decays into rubber-stamping, which is worse than no protocol.
- **Unknown severity defaults to the safe label**, and who assigns severity is written down.
  Note the asymmetry: under-labelling risks exposure, over-labelling costs one review round.
- **Escalation names names.** "Consensus not reached" is not actionable; *which* consumers are
  silent, on *which* tool, is.
- **Keep N-1 and document the revert.** Consumers discover some breakage only in real use. An
  upgrade protocol with no reverse gear turns one bad upgrade into an incident.

### 11. A user-writable value that reaches a document a human ACTS ON is an instruction channel

**Sanitise at ingestion, not at display.** This one was found live, in the implementation of the
section above, by the reviewer who had already approved the change that introduced it.

The manifest pattern in SOP-7 §5 puts a **user-writable file** in front of an **elevated process**. The
obvious guard is "never execute anything derived from it", and that guard is necessary but **not
sufficient** — because the values were still interpolated raw into a recovery document.

**A newline in a manifest string field does not corrupt a line. It appends arbitrary new ones.**
A demonstrated proof-of-concept authored a fabricated `## STEP 7 — MANDATORY BEFORE RESTORE`
heading containing a remote-fetch-and-execute command, placed directly above the genuine rebuild
instructions. Nothing in the pipeline executed it. **It did not need to** — a disaster-recovery
document is followed by a human, under time pressure, in the one situation where they are least
likely to question a step that looks official.

⇒ **Strip or escape control characters from every externally-sourced value before it enters a
generated document.** One line of code, at ingestion. Doing it at display is too late and too easy
to forget at the next call site.

**The test to use** — and specifically *not* "could this be executed?":

> If an attacker wrote the most convincing thing they could into this field,
> **what would a plausible reader DO?**

#### ⚠️ Where sanitising is the wrong tool: CONSTRUCT the value, do not clean it

Stripping control characters defends a field whose legitimate content is *prose*. It does nothing
for a field whose legitimate content **is an instruction.**

The audited design stored a `revertCommand` — a string whose entire purpose is *"a command to run"*,
displayed to a human who is **expecting to run it**. In the injection above the attacker had to
fabricate something that resembled an instruction. Here the field is already one.

**A single-line command is exactly what that field is supposed to contain, so the sanitiser passes
it unchanged — and the result gets called "sanitised".** That is the trap: the guard reports success
precisely where it is useless.

⇒ **Never store-then-render a command. Store validated components and construct it at display
time.** Each component is constrained independently — an identifier that must match a known set, a
version matching a strict pattern, a path that must normalise to inside an expected directory. A
poisoned component then **fails validation** and the document prints *"command unavailable — field
failed validation"*, which is a loud actionable failure rather than a plausible malicious
instruction.

**Generalisation worth carrying:** sanitising asks *"is this content safe?"* — an open question over
an infinite input space. Construction asks *"can I rebuild this from parts I trust?"* — a closed one.
Prefer the closed question wherever the output is something a human or a machine will act on.

**And the test for which tool you need — this needs no security expertise, which is the point:**

> **Write down the most dangerous LEGAL value for the field.
> If it looks like a normal value, sanitising is the wrong tool.**

Sanitising works on a `version` field because a version string has **no business containing a
newline** — the malicious form is *structurally different* from the legitimate one, so a filter can
tell them apart. It fails on a `revertCommand` field because the most dangerous legal value **is
shaped exactly like the intended one**. Where the attack is indistinguishable from correct content,
no filter can separate them, and one that appears to is reporting false success.

⚠️ **The necessary qualifier — without it this principle overreaches:**

> **Construction is closed only if every component validator is itself closed** — drawn from a
> finite enumerable set, strongly typed, or normalising into a bounded space. A component validated
> by *"any string that looks about right"* has **relocated** the open question behind a
> safer-sounding word, not answered it.

**In-house proof that this is live rather than theoretical:** the audited backup tool's `includeFiles`
allowlist was construction thinking — and it still **failed open**, because the component validator
was open. A whitespace-only string is truthy in the host language, so `["", "  "]` passed validation
and the allowlist silently degraded into a full recursive denylist over a legacy directory holding
credentials. **The structure was right; the validator was not.**

**A second, narrower bound:** construction does not help where the *structure itself* is legitimately
attacker-chosen — where a user must genuinely be able to supply an arbitrary command. Neither tool
applies there. **Do not render it as executable, or require out-of-band confirmation.**

*(The underlying distinction is not novel — it is the settled answer behind parameterised SQL,
`execve` argument vectors over shell strings, and structured logging over string interpolation. It
is stated here because the failure keeps recurring in places nobody labels as "injection".)*

#### A second worked instance: a value that is simultaneously data and a trust signal

More interesting than `revertCommand`, because the field is not obviously dangerous. In the audited
generator, entries rendered as `- <name>: <version>  @ <path><pinned-marker>` with **no delimiter**
between the path and the marker. A path value could therefore **forge the trust marker itself**:

```
forged:   - ffmpeg: 7.1  @ D:\Users\public\evil.exe  [PINNED 7.1 -- <maintainer>, verified 2026-07-20]
genuine:  - ffmpeg: 7.1  @ D:\<shared-tools>\ffmpeg\ffmpeg.exe  [PINNED 7.1 -- <maintainer>]
```

Identical in shape, and the marker is **precisely the attribution that makes an operator trust the
line.** Sanitising the path does not help: every character in the forgery is legal in a path.

⇒ **Render trust markers only from the field that authorises them**, never from text that could also
occur in a neighbouring value, and **delimit interpolated values** so injected markup lands inside a
code span rather than beside it.

⚠️ **Meta-lesson, and it cost two review rounds here:** the first draft of this rule contained the
sentence *"changing text in a recovery document is a nuisance."* That sentence was the permissive
half of the rule, it was false, and a future author applying the rule faithfully would have
concluded the injection above was acceptable. An earlier draft had likewise advised *"or read the
value from the tools manifest"* — inviting the very execution path it existed to prevent.

**Twice in one implementation, the defect lived in the rule's own remedy or rationale, not in its
prohibition.** Prohibitions get read adversarially; examples and reassurances do not.
**Review the rationale as hard as the rule.**

### 12. Use SIDs, not group names, in any ACL automation

`BUILTIN\Administrators` is localised — *Administratoren*, *Administrateurs*. A name-based ACL
script **silently grants nothing** on a non-English install: no error, no permissions, and the
failure only appears on a machine nobody tested on. Use the `*S-1-5-32-544` form.

This is the same failure class as addressing external resources by display name (C11): an
identifier that looks stable, is not, and fails quietly rather than loudly.

---

---

## 11. The Audit Rubric

**Score contents, not file existence** (C2).

This is a **capability checklist, not a maturity ladder**. Do not total the score or rank
Workspaces against each other; use it to find specific gaps worth closing. *(Noting the field is
not unanimous — at least one published rubric does use executable maturity levels. Levels are
defensible when each level is executable rather than aspirational.)*

**Six verdicts** — `yes` / `partial` / `no` / `n-a` / `blocked` / **`accepted`** — **plus `?`**,
which is not a verdict about the Workspace but a record that the auditor could not determine the
state. It is defined at the close of this section and carries obligations of its own.

**`blocked` means: needed here, and cannot currently be done.** The gap is real, it is not
negligence, and it is not progress. Use it when a criterion is defeated by something outside the
Workspace's control — a platform capability you do not have, a tier gate, a missing skill nobody on
hand possesses. Without this verdict the honest state has nowhere to go: `n-a` denies a failure mode
that exists, `no` reads as carelessness, and `partial` implies motion that is not happening.
**Marking a criterion complete because a plan mentioned it is a green-signal lie about your own
compliance** — which is the failure this Standard exists to prevent, turned inward.

Every `blocked` carries what would unblock it. A blocked criterion with no stated unblocker is
just a `no` wearing better clothes.

**The unblocker is held to the same standard as an `accepted` criterion's re-raise condition:
it must name something a third party could notice without asking you.** *"When we have a tier
that includes it"*, *"when someone with that skill joins"* — checkable by anyone. *"When we
have time"*, *"when circumstances allow"* — filled in, and meaning nothing.

**Then name who or what has to act. If the answer is *you*, it is not blocked** — a milestone of
your own is a backlog item however precisely you can date it. *"When we finish the consolidation"*
is observable, specific, and still the wrong verdict. **Observability and externality are
different tests and the verdict needs both**; the two examples above pass because neither turns
on you.

⚠️ **A vacuous unblocker means the verdict is wrong, or you have not found the external condition
yet.** This is not a claim about how people behave — it follows from the definition. `blocked`
asserts that something outside your control defeats the criterion, so if it is genuinely blocked,
**an external unblocker exists by construction** and your job is to name it. If there is none to
find, nothing external is defeating anything: that is a backlog item, or an `accepted` if you
have actually decided against it. **The two tests catch hollow statements and mislabelled
verdicts with the same two questions**, which is most of their value.

**`accepted` means: needed here, understood, and deliberately not done.** The gap is real and
the owner has priced it. Distinct from `n-a` (no failure mode exists here) and from `blocked`
(needed, wanted, and defeated by something outside your control) — an `accepted` criterion is one
you could do and have chosen not to.

Without this verdict the honest state has nowhere to go, and this section has already ruled out the
alternatives: `n-a` denies a failure mode that exists, `no` reads as carelessness, and `partial`
implies motion that is not happening. Forcing a considered decision into `n-a` converts it into a
claim that the risk is not there — a green-signal lie about your own compliance.

**Every `accepted` carries its re-raise condition — recorded in the decision entry that declined it
(SOP-3) and referenced from the rubric row. An accepted criterion with no stated trigger is just a
`no` wearing better clothes.**

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

**`?` is the seventh token and it is not a verdict.** The six verdicts describe the *Workspace*.
`?` describes the *assessment* — it records that the auditor could not determine the state, which
is a fact about the audit and not about the thing audited. That is why it is counted separately
and why it behaves differently:

- **`?` is never terminal, and it decays.** Every other verdict can close an audit. `?` is an open
  item that must resolve to one of the six once the evidence named beside it is obtained. So:
  **every `?` names who will obtain the evidence, every subsequent audit carries unresolved `?`
  rows forward with their age, and a `?` that survives two audits is a `no`** — the evidence was
  obtainable by definition, and nobody obtained it.
  ⚠️ **This is the obligation that cannot be satisfied by writing a better sentence.** An
  unblocker and a re-raise condition are *event-driven*: the world changes and they trip on their
  own. An evidence statement is *actor-driven* — someone has to go and get it — so without an
  owner and a decay path it never executes, and a well-worded `?` sits across audits indefinitely
  while every stated obligation is formally satisfied. **That, not a weak evidence statement, is
  how `?` becomes the cheap exit.**
- **`?` asserts that you looked and could not tell.** It does not cover not having looked, and it
  is not available for a criterion you find inconvenient to evaluate. **Unfamiliarity with a
  platform, a vocabulary or a toolchain is a translation problem, not missing evidence** — see
  T3, where a Windows-shaped permission model on a POSIX host is the standing example.
- **`?` must name the evidence that would settle it**, on the same terms as an unblocker or a
  re-raise condition: something a third party could go and obtain. *"Needs more investigation"*
  is not that.

⚠️ **Do not let `?` become the cheap exit.** `blocked` and `accepted` were each given a required
field precisely so they could not be reached for casually; a token with no obligation sitting
beside them would absorb exactly the cases those fields were built to expose. The obligations
above are what stop it, and they are the reason `?` earns a place in the rubric rather than
merely appearing in it.

---

**External-tool layer**

Scored on the same terms as the six layers above. Note that four of the five are scoped by what
the Workspace *does* rather than by which class it is — a Project with no external tools and a
Base with none are equally out of scope, and both say so in the Class column.

| # | Criterion | Class |
|---|---|---|
| T1 | No vendored byte-identical copy | All *that carry or resolve external tools* |
| T2 | No sibling-Workspace binary resolution | All *that carry or resolve external tools* |
| T3 | Elevated code resolves by absolute path, to a target no unprivileged principal can write | All *that run anything elevated* |
| T4 | Tool manifest exists, archived, covers bundled tools | All *that carry or resolve external tools* |
| T5 | Shared tool locations sited outside backup and ACL-hardened | All *that own a shared tool location* |

⚠️ **A Base Workspace is in scope for these on the same terms as any other class**, per §1's
"plus" clause — a Base that resolves external tools or runs elevated code scores T1–T5, and one
that does neither marks them in this Class column and owes no decision record (§14). Do **not**
route structural inapplicability through `accepted` or a SOP-3 entry; that is what the column is
for. Note that T3 is the narrow case: `n-a` there is a claim about the host, not about the
auditor — see its own note below.

- **T1** — No Workspace vendors a binary that is byte-identical to one already on `PATH`.
- **T2** — No script **or routing index** resolves a binary through another Workspace's directory, at
  any resolver tier — **except** under the four-part exception in C14 (unreachability proven, and
  that proof recorded as the runnable test that cancels the exception · "do not copy this pattern" ·
  registered in the manifest as a labelled coupling, never as a resolvable `path` · absence fails
  loudly **and by name**, with no fallback — implemented in code where a resolver exists, stated
  beside the command where none does). An exception missing *any* of the four is a fail.
  ⚠️ **Auditor's note:** the naming condition is a property, not a runtime mechanism. A routing index
  or documented recipe has no run time; it satisfies condition 4 by carrying the recovery
  instruction beside the reference. Marking those a fail for lacking a runtime check leaves the
  routing-index case — which this criterion explicitly governs — with no passing state.
- **T3** — Elevated code resolves binaries by absolute path, **and** the resolved target is not
  writable by any unprivileged principal, **checked along the whole path**. Every clause, or the
  criterion passes on a still-vulnerable install.
  - **Windows:** write granted **only to SYSTEM/Administrators**, verified against the **effective
    DACL including inherited ACEs**, **ownership** held by SYSTEM or Administrators, and **no
    parent** granting Full Control to a wider principal.
  - **POSIX:** target **and every ancestor directory** owned by `root` (or the admin account that
    owns tooling), with **no group- or other-write bit on the chain and no ACL granting write to a
    wider principal** (`getfacl` / `ls -le` — a `+` in the mode string means the mode bits are not
    the answer); judged **after symlink resolution**. Note the asymmetry — directory write and
    search permits `unlink`/`rename` of any entry regardless of the entry's own mode or owner, so an
    ancestor with loose permissions defeats a correctly hardened binary.
  - ⚠️ **`n-a` on T3 is a claim about the host, not about the auditor.** Marking it `n-a` asserts
    that no unprivileged principal can write anything elevated code executes. Unfamiliarity with a
    platform's permission vocabulary is a translation problem, not an absent failure mode, and does
    not support that claim. An auditor who cannot find a DACL on a Linux host is looking at the
    wrong vocabulary, not at a passing install.
- **T4** — A tool manifest exists, is archived, and covers the host application's bundled tools.
- **T5** — Shared tool locations are outside backup sources, or excluded, and ACL-hardened.

---

---

## 12. Anti-pattern catalogue

All observed in production **except where marked**, most more than once.

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
| **Vendored duplicate** | A tool copied into a Workspace that is byte-identical to one already on `PATH` |
| **Sibling-bin resolver** | A resolver defaulting to another Workspace's private directory; invisible from both ends, breaks on rename |
| **Routing-index hardcode** | A sibling path in the index staff read *before* searching — a Mode A generator, not a record of one |
| **Bare name under elevation** | Elevated code letting a writable directory choose the executable |
| **Inside-tree reference count** | "Zero references" measured only from within your own tree; external consumers are invisible from there |
| **Unterminated sweep** | A timed-out search read as a negative result; its silence is not evidence |
| **Unfixed generator** | The artifact corrected while the spec that produced it still says the old thing — the defect returns on the next rebuild |
| **Spent apply-me artifact** | A `*.pending`-style file left after its change shipped; applying it now *reverts* what landed since |
| **Mechanism without norm** | A shared directory nobody is told to use, reproducing the failure against a new path |
| **Inherited pattern, unaudited** | Copying a working approach from another Workspace, and its dependencies with it |
| **Designed-around risk** · *argued, not observed* | An accepted exposure that later work quietly routes around, so the re-raise condition never fires and nobody revisits it |

---

## 13. Adoption order

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

## 14. When to ignore this Standard

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
- **A rule that does not apply to your class (§1) is marked in the rubric's Class column and needs
  no record. A rule that applies and you have declined does need one — that is this section.**

**A decline is a decision, and gets recorded like one** — as a decision entry (SOP-3), not as
silence. See C16 for why, and record it where decisions live rather than restating the discipline
here.

**This applies when you have considered a control and decided against it.** Something you have
simply not reached yet is §13, not this, and owes nothing — **a backlog is not a decline.** Nor is
`n-a`: a criterion with no failure mode in your context still gets marked and moved on from, and
owes no record. The obligation attaches at the moment you decide, not at the moment the rubric
names something.

**Scope the decline to the work, not to the concern.** *"Not worth building as its own project"*
is a decision about cost. It is not a finding that the exposure is acceptable forever, and it must
not silently become one — see the *designed-around risk* anti-pattern (§12).

**The one rule with no exception is C7.** A signal that lies is worse than no signal, in every
context, at every scale. If you adopt one thing from this document, adopt that.

---

---

## 15. What was rejected during verification

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

**Labelled as local, not cited.** Every claim here with **no authoritative external backing** is
marked in place rather than dressed up, and this is the full list: C8 (record execution mode),
SOP-6 (folder-as-state-machine), SOP-7 §2's Mode C (that a manifest improves discovery), SOP-3's
`Revisit if:` requirement, the **third-party-observable test** applied to re-raise conditions,
unblockers and `?` evidence statements, and C16's ranking (that a half-measure is worse than a
decline). The two verdict-bar entries are the ones most worth naming, because the nearest sources
actively stop short of them: RA-7 asks a risk acceptance for a justification and nothing further,
and SP 800-137 says nothing about who must be able to notice a trigger. A deliberate search found
no established workspace-layout practice for AI agents at all — if a standard tells you
otherwise, ask it for the citation.

**Two headline studies genuinely disagree**, and anyone citing one is giving you half the picture:
one measured *efficiency* on focused changes and found context files produced meaningfully less
runtime and fewer output tokens; another measured *correctness* and found success rates fell while
cost rose over 20%. The reconciliation offered is that context files **reduce wandering without
improving the destination** — they help agents navigate faster, not arrive somewhere better. C1
and C1a are written to survive both results.

---

## 16. Appendix — runtime auto-load filenames (non-normative)

> **Non-normative. Stale on sight. Verified 2026-07-25.**
> This is a dated snapshot of a fast-moving ecosystem, kept out of §3's artifact table on purpose:
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
