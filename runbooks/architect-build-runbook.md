# Clairvoyance Workspace Architect - Build Runbook

**Audience: both** (human operator + the Staff member executing steps)
**Purpose:** create a persona, hire a Staff member on it, and propagate the
[Workspace Standard](../STANDARD.md) so they can **plan** Workspaces to the
Standard and **build** them once approved.

**Time:** ~20 minutes. **Reversible:** mostly — see §6 for the one part that is not.

---

## ⚠ Read first — two things that will bite you

**1. The Knowledge Base is changeable after hire — but awkwardly, so choose deliberately.**
It is **not** permanent, despite appearances. The field shows **greyed out** in an existing Staff
member's configuration whenever they are not idle, and there is **no Stop or Pause control** to put
them into that state on demand — so you are waiting for an idle window you cannot force. The
alternative is editing the Staff record JSON externally and reloading, which means closing the app
or working around a file it owns at runtime.

**Practical consequence:** treat the persona choice as *expensive to change*, not irreversible.
Getting it right at hire saves a fiddly recovery; getting it wrong is annoying, not fatal.

**2. A persona is injected at session start, not polled.**
Editing the persona file does **not** affect a running Staff member. The change takes effect on
their next fresh session. If you edit and "nothing happened," that is why — not a bug.

*(If your install also has a **Clairvoyance Engineer** persona, do not confuse the two. That one
builds software **on** the platform — Exhibits, CAMs, MCP integrations. This one designs and builds
**Workspaces**. Different role entirely, and they pair rather than overlap.)*

---

## 1. Prerequisites

- [ ] You can write to your Clairvoyance user-data directory.
- [ ] You have a **Criteria Card** saved as a note (derived per [IMPLEMENTATION.md](../IMPLEMENTATION.md) §2) —
      this is what the persona reads. The Standard saved alongside it is useful but not required.
- [ ] You know your personas directory. Default: `<UserData>/neurons/personas/`.
      *Verify by listing it — you should see the stock personas (Analyst, Engineer, Writer…).*
- [ ] Decide the model tier now (§4).

---

## 2. Create the persona file

Copy [`personas/clairvoyance-workspace-architect.md`](../personas/clairvoyance-workspace-architect.md)
to `<your Clairvoyance data directory>/neurons/personas/`, renaming it to
`Clairvoyance Workspace Architect.md`.

> **Copy the file, not the folder.** Persona discovery is **flat** — only files at the top level of
> `neurons/personas/` are found. Copying this repo's `personas/` directory produces
> `neurons/personas/personas/…`, which fails **silently**: the file is there, no error appears, and
> the persona never shows up in the dropdown.

**Verify you are writing to the base the app actually reads.** If your installation has ever moved
its data directory, a superseded path may still accept writes silently while the app serves the
other one — a persona saved there will simply never appear, with no error at any point. Confirm the
live base first (pointer file or app settings), then write.

**Do this with the app closed** if your build rewrites persona indexes at runtime; otherwise
create it and restart. Then confirm it appears in the Knowledge Base dropdown **before** hiring —
if it is not listed, the hire will silently fall back to a different persona.

The persona text is maintained as a single canonical file:
**[`personas/clairvoyance-workspace-architect.md`](../personas/clairvoyance-workspace-architect.md)**.

It is a planning-first Workspace designer: it classifies a Workspace, scores it against the
rubric, and produces a costed plan — and it is deliberately gated to PLAN mode until you approve.
**It then builds what you approved**; the gate defers construction, it does not replace it.
It **routes** to your instance's Criteria Card as its governing document rather than restating any
criteria — which is why §3 below is not optional: without the Card saved and routed, it has
instincts and no criteria.

Then confirm it appears in the **Knowledge Base** dropdown (refresh the field if it is not there
immediately) **before** hiring.

---

## 3. Propagate the criteria

The persona makes them *capable*. These steps make them *informed*. Do all three — the persona
carries neither the Card's contents nor the Standard's.

**3a. Put the criteria where they will find them.** Save the **Criteria Card** as a note — it is
the persona's governing document and the one thing it will stop without. Save the Standard as a
note too, for anyone deciding whether to adopt or change a criterion. Notes are readable across
Staff; per-agent private memory is not. **Save this runbook as a note too**, under the title
`Clairvoyance Workspace Architect - Build Runbook` — the route in 3b names it, and a route to a
note you never saved is exactly the C2 failure this step exists to prevent.

**3b. Route it from the Workspace `library.md`.** Add:

```markdown
- IF designing, auditing or building a Workspace → read [[Workspace Criteria Card]]
- IF deciding whether to adopt, challenge or extend a criterion → read [[Clairvoyance Workspace Standard]]
- IF creating Staff or personas → read [[Clairvoyance Workspace Architect - Build Runbook]]
```

*This step is the one people skip, and skipping it is what makes the criteria invisible. An
unrouted document does not exist. Note the three IF-conditions are deliberately disjoint — per C3 a
reader follows exactly one match and skips the rest, so overlapping conditions silently hide the
later line.*

**The Criteria Card line matters most.** The persona looks for the Card, not the Standard — it is
the compact, instance-tuned working copy derived in [IMPLEMENTATION.md](../IMPLEMENTATION.md) §2.
If you have not produced one yet, do that first: without it this persona will correctly stop on its
first turn and ask for it.

**3c. Give them the pointer in the first assignment** (§5). Do not assume they will find it.

---

## 4. Choose the model tier

Apply the Standard's own tiering logic — judgment versus mechanics.

| Work | Tier |
|---|---|
| Auditing, designing, trade-off reasoning, writing plans | **Strong reasoning model.** This is judgment work and it is where the value is. |
| Creating directories, writing templated files, verifying | Cheaper tier is fine |
| Anything unattended | **Not a local model** unless you have verified completion delivery yourself |

If you must pick one: **choose the stronger model.** A workspace architect that produces a
plausible-but-wrong structure costs far more than the token difference, and the error surfaces
weeks later.

---

## 5. Hire the Staff member

Hire with the persona attached at creation (remember: likely not editable later).

Using the MCP tooling:

```
recruit_tools → hire
  name:           "Warren"                             ← any display name you like
  persona:        "Clairvoyance Workspace Architect"  ← must match the dropdown exactly
  jobDescription: "Workspace Architect"
  workspacePath:  "<path to the workspace they'll work in>"
  assignment:     "<first assignment — see below>"
```

Or hire through the UI, selecting your new persona in the **Knowledge Base** dropdown.

**A first assignment that verifies the setup rather than assuming it:**

> Read `[[Workspace Criteria Card]]` — your governing document here. Then, in PLAN mode only, classify this
> Workspace and score it against the 34-criterion rubric, scored per layer rather than as a total.
> Report your findings with paired benefit and cost per recommendation. Mark anything you cannot
> evidence as `?` rather than guessing. Explicitly list criteria you judge not-applicable here and
> say why. **Do not build anything.** End by telling me which single change you would make first
> and what it would cost.

That assignment tests all of it: whether they can reach the Criteria Card, whether they respect PLAN
mode, whether they will admit uncertainty, and whether they will flex rather than demand
compliance.

---

## 6. Verify — and what is not reversible

- [ ] Persona appears in the Knowledge Base dropdown **before** hiring.
- [ ] New Staff member's configuration shows the correct Knowledge Base.
- [ ] They can open the **Criteria Card** note by name (and the Standard, if they need to argue a criterion).

> **What this checklist has and has not been used to verify.** The *audit* half of this persona
> has been exercised on a real Workspace — classification, per-layer scoring, costed plan, PLAN-mode
> gate, and the not-applicable discipline all behaved as documented. The *intake* half has **not**:
> the four-facts greenfield dialogue, its stopping conditions, and the ask-in-the-user's-language
> calibration are unobserved, because a delegated one-shot assignment has no conversational channel.
> If you are starting a greenfield Workspace, you are the first to exercise that path — treat the
> intake as unverified and tell us how it went.
- [ ] Their first report uses PLAN mode and did not create files.
- [ ] Their report contains at least one `n-a`, `accepted`, or "not recommended" — if everything
      scored as a gap to close, the flex instruction is not landing. **`accepted` is the stronger
      signal of the two**: `n-a` says a criterion did not apply, `accepted` says they priced one
      and declined it.
- [ ] **The first exchange asked fewer than five questions, and each one changed something.** A
      discovery interview means the intake has become a ritual — the number of questions should be
      emergent, and zero is a valid answer when the context is already evident.

**Not cleanly reversible:** on current builds, **permanent hires generally cannot be dismissed
through MCP tooling** — removal is a manual UI action, and a failed hire can sit on the global
roster indefinitely. Also note that in some builds hires register **globally** rather than
per-Workspace, so the Staff member's display name has to stay unambiguous across every Workspace,
not just this one. Get the name and persona right the first time.

---

## 7. Operating the Staff member

**Ask for a plan first, every time.** The two-mode split only works if you use it. If you ask for
a Workspace and get one built, the gate has already failed.

**On the two "only absolute" claims.** The persona says the PLAN/BUILD gate has no exceptions; the
Standard says the one rule with no exception is *a signal that lies is worse than no signal*. Both
are correct and they do not compete: the Standard's absolute governs **Workspaces you assess**, the
persona's governs **this Staff member's own conduct**. If a reader notices the apparent conflict,
that is the resolution.

**Approve item by item, not wholesale.** "Do 1, 3 and 4; skip 2 and let's discuss 5" is the
intended interaction. Blanket approval discards the benefit/cost analysis you asked them to
produce.

**Expect and reward pushback.** A workspace architect who never says "that criterion doesn't
apply here" is applying a checklist, not judgment — and a checklist you could have run yourself.

**Re-audit after material change**, not on a schedule. Audits on a timer produce ritual; audits
after change produce findings.

---

## Appendix — Adapting this runbook

- **Different platform layout?** Only §2's path is install-specific. Everything else holds.
- **Want a planner and a builder as separate Staff?** Reasonable for high-risk environments —
  it makes the approval gate structural rather than behavioural. Cost: two seats, and a handoff
  that must carry the plan intact. Do not split by default; more agents is not more capability
  unless context is the binding constraint.
- **Want them to audit multiple Workspaces?** Check whether your build scopes Staff tooling to
  their own Workspace. If it does, either give them a Workspace-agnostic path or hire one per
  Workspace.

---

*Companion to [Workspace Standard](../STANDARD.md). Free to copy and adapt.*
