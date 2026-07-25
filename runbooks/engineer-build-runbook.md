# Build Runbook — The Clairvoyance Engineer

**Audience: both** (human operator + the Staff member executing steps)
**Status:** Free to copy, adapt, and share. The persona text (~1,600 words) is a standalone file:
[`personas/clairvoyance-engineer.md`](../personas/clairvoyance-engineer.md).
**Purpose:** hire a Staff member who builds *things that run inside* a Workspace — Exhibits, CAMs
and Extensions, Binders, MCP integrations, and scheduled automation.

**Companion:** [Workspace Architect Build Runbook](architect-build-runbook.md) creates the Staff member who
sets up the Workspace itself. See §0 for which one you want.

---

## 0. Is this the Staff member you want?

**The test: is there something to build, or somewhere to set up?**

| Need | Persona |
|---|---|
| Somewhere to work — structure, routing, decision record, governance | **Clairvoyance Workspace Architect** |
| Something that runs — an Exhibit, a CAM, a scheduled job, a Binder integration | **Clairvoyance Engineer** |

**The boundary is not crisp, and pretending otherwise will cost you.** Pipeline Workspaces overlap
by design: the Architect designs the stage machine and its failure paths; the Engineer writes the
steps that move work between stages. Expect to want both, sequentially, not simultaneously — and
per C12a, **whichever one is writing holds the pen alone.**

If you only ever want one: most people need the Architect first, because a well-built Exhibit in an
unnavigable Workspace still gets lost.

---

## 1. Prerequisites

- [ ] You can write to your Clairvoyance user-data directory.
- [ ] You know your personas directory. Default: `<UserData>/neurons/personas/`.
- [ ] You know which surface the work is likely to need — or you accept that deciding is part of the
      first assignment.
- [ ] Decide the model tier (§3).

---

## 2. Create the persona file

Copy [`personas/clairvoyance-engineer.md`](../personas/clairvoyance-engineer.md) to
`<your Clairvoyance data directory>/neurons/personas/`, renaming it to
`Clairvoyance Engineer.md`.

> **Copy the file, not the folder.** Persona discovery is **flat** — only files at the top level of
> `neurons/personas/` are found. Copying this repo's `personas/` directory produces
> `neurons/personas/personas/…`, which fails **silently**: the file is there, no error appears, and
> the persona never shows up in the dropdown.

**Write to the live base.** If your installation has ever moved its data directory, a superseded
path can keep silently accepting writes while the app serves a different one — a persona saved there
never appears, with no error at any layer. Confirm the live base first, then write.

**One link to check before you save.** The persona routes to the Workspace Standard by WikiLink. If
you have saved the Standard under a different note title, **edit that link or delete it** — by C2, a
route to a note that does not exist is worse than no route. If you have not adopted the Standard at
all, delete the sentence; this persona works without it.

**The Knowledge Base is changeable after hire, but awkwardly.** The field is greyed out whenever the
Staff member is not idle, and there may be no Stop or Pause control to force that state — so you
wait for an idle window you cannot summon. The fallback is editing the Staff record JSON externally
and reloading. Expensive to change, not irreversible.

**Personas inject at session start.** Editing the file does not affect a running Staff member —
changes land at their next fresh session. Confirm it appears in the Knowledge Base dropdown
**before** hiring; if it is not listed, the hire will silently fall back to a different persona.

**What it is.** It builds solutions on the Clairvoyance platform — Exhibits, CAMs and Extensions, Binder and MCP
integrations, and the scheduled automation around them. Correctness before simplicity before
performance, sandbox constraints before all three, and assertion discipline and stable-ID
addressing as reflexes rather than references. Unlike the Architect it is fully functional without
the Standard; its route to SOP-4 is an enhancement.

---

## 3. Choose the model tier

Same judgment-versus-mechanics split as the Architect, but the judgment lives somewhere different.

| Work | Tier |
|---|---|
| **Surface choice** — Exhibit vs CAM vs native vs Canvas — and its trade-offs | **Strong reasoning model.** This decision is expensive to reverse and invisible until it is. |
| **Sandbox / CSP debugging** | **Strong.** Where a weak model burns turns guessing at a constraint it cannot see. |
| Templated Exhibit work, mechanical build-out against an approved design | Cheaper tier is fine |
| Anything unattended | **Not a local model** unless you have verified end-to-end completion delivery yourself |

**Budget a turn for reading regardless of tier.** This persona is required to open the relevant
staff doc before producing a gated artifact, and that read is a separate turn by design. It is not
the model being slow.

---

## 4. Hire

```
recruit_tools → hire
  name:           "<display name>"
  persona:        "Clairvoyance Engineer"   ← must match the dropdown exactly
  jobDescription: "Platform Engineer"
  workspacePath:  "<the workspace whose things they will build>"
  assignment:     "<first assignment — see below>"
```

**The first assignment must be surface-ambiguous, or it tests nothing.**

This persona's gate is *propose before you build*, which is the analogue of the Architect's
PLAN/BUILD split — but **deliberately softer**: it carries an explicit exemption for spikes and
throwaway diagnostics. A task with an obvious surface will sail past the gate without ever engaging
it, and you will learn nothing about whether the gate works.

> Propose an approach for **\<a capability that could plausibly be an Exhibit, a CAM, or neither\>**.
> Name the surface choice and what it costs — not just what it gains. Identify the platform
> constraints that shape it. **Do not implement anything.** End by telling me what would change your
> recommendation.

---

## 5. Verification tells

- [ ] **Did it name the surface choice *and its cost*, before writing any code?**
      *"A CAM survives restarts and any Staff member can call it; an Exhibit ships faster but cannot
      expose tools"* — not *"I'll build a CAM."* A recommendation without its cost means the
      trade-off was not actually made.
- [ ] **Did it open the relevant staff doc in a separate turn before producing the artifact?**
      This is the platform's two-turn read-before-write rule and it is **the most likely first
      failure** — reading in parallel with generating means it generated from guesses.
- [ ] **Did it quote an actual error rather than paraphrase one?** The real CSP violation, the real
      stack line.
- [ ] **Did it say what would change its recommendation?** Calibrated confidence, not assertion.

---

## 6. What does *not* transfer from the Architect runbook

**Skip the propagation step.** The Architect runbook's §3 exists because that persona is deliberately
useless without the Standard — it routes rather than restates, so an unrouted Standard leaves it with
instincts and no criteria. **The Clairvoyance Engineer is fully functional without the Standard.**
Its route to SOP-4 is an *enhancement*, not a precondition. Copying the §3 framing across would
overstate a dependency that does not exist and make this hire look gated on setup it does not need.

**Two fragilities in that route, worth knowing:**

- The persona routes by **note name**, to `[[Workspace Criteria Card]]` — your instance's derived
  criteria, not the Standard itself. That is deliberate twice over: the persona runs *inside* a
  Clairvoyance instance, where a repo-relative path means nothing and a WikiLink is native; and the
  Card is the Staff-facing artifact, whereas the Standard is written for a human deciding whether to
  adopt a rule. The cost is that the route binds to a name — IMPLEMENTATION.md §2 guarantees the
  title `Workspace Criteria Card`, so keep it, and renaming it later silently breaks the route. The
  sentence names the role before the title, so a miss degrades to a search rather than a stop.
- **The route does not survive a bare persona copy.** If the persona file travels to a machine where
  the Standard was never saved as a note, the reference dangles. The fix is to save the Standard
  first (the Architect runbook's §3, *Propagate the Standard*) or drop the route — *not* to restate SOP-4 into the persona.

---

## 7. Operating notes

**Its gate is softer than the Architect's, on purpose.** A quick diagnostic or throwaway spike does
not need a proposal; a feature someone will depend on does. If you want the ceremony skipped, say
"this is a spike" — that is a supported path, not a workaround.

**Route automation work here, but not reflexively.** The Architect discloses when a plan needs code
written; that disclosure is a prompt to decide, not an instruction to hand off. A one-line content
assertion often does not need a second Staff member.

**Where restatement is correct and routing is not.** This persona restates two rules — assertion
discipline and stable-ID addressing — rather than routing to them. That is deliberate and worth
understanding as a general principle: **a route is right for procedure you consult before starting;
restatement is right for reflexes that fire while writing a line of code.** A pointer is too slow
for a keystroke-level habit.

---

*Companion to [Workspace Architect Build Runbook](architect-build-runbook.md) and
[Workspace Standard](../STANDARD.md).*
