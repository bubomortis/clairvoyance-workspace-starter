# Workspace Standard — Citation List

**Audience: human.** A reader checking the Standard's evidence, or extending it.
**Status:** Free to copy, adapt, and share.

Sources actually used in [STANDARD.md](STANDARD.md), including SOP-1 through SOP-6.
Compiled 2026-07-25.

## How this was built, and what to distrust

**The Standard contains zero URLs.** It is `Audience: human` and states its evidence in prose
without linking it. So this list is a **reconstruction**, not an extraction: each claim in the
Standard was matched back to the maintainer's local research corpus — not published — by its
distinctive figures and phrasing.

Confidence is marked per entry:

- **● high** — a unique number or verbatim phrase in the Standard matches exactly one source
  (e.g. "33.0% / 28.3% / 25.5%", "container fallacy", "Decision Shadow").
- **○ medium** — topical match only, no unique figure. The source is on-point and in the corpus,
  but another source could have supplied the same sentence.

**Liveness** is from `livecheck.tsv` (a real `curl` fetch with a browser User-Agent, run
2026-07-25): **99 of 107 corpus URLs return 200.** Do *not* use the DEAD verdicts in
`results-verify-CLAUDEs-citations.md` — that pass returned 39 dead-link verdicts, most of which
are live, and it is the same failure the Standard describes in §15 and C7. Its *content* verdicts
(real titles, authors, dates for arXiv IDs) did check out against the live fetch and are used here.

Corpus totals for scale: **107 unique URLs researched, ~30 actually used.** The gap is the point —
most of what was gathered did not survive verification.

---

## 1. The Charter (C1–C12)

### C1 — Entry point must be directive, not descriptive

1. ● **Gloaguen, T. et al. — "Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for
   Coding Agents?"** arXiv:2602.11988, 12 Feb 2026. `https://arxiv.org/abs/2602.11988`
   *Supplies:* the >20% inference-cost increase, no general improvement in task success, and the
   load-bearing breakdown — instructions followed, repository overviews not.
   🔑 **Design, recorded in full because omitting it caused two successive defects.** The paper runs
   **two** settings — SWE-bench tasks with **LLM-generated** context files, and **CTXBENCH**, a
   purpose-built benchmark of **138 instances across 12 repositories carrying developer-committed
   context files.** CTXBENCH is evaluated in **three** conditions on a **common corpus**: no context
   file, LLM-generated, developer-written. **It therefore contains a head-to-head on provenance.**

   | Contrast | Effect | Significance |
   |---|---|---|
   | Developer-written vs none | +2.4% | **not significant**, p = 0.21 |
   | LLM-generated vs none | marginal negative | **not significant** |
   | **Developer-written vs LLM-generated** | developer-written higher | **SIGNIFICANT, p = 0.038** |

   §6: *"LLM-generated context files have a marginal negative effect on task success rates, while
   developer-written ones provide a marginal performance gain, neither statistically significant."*
   §1 recommends *"omitting LLM-generated context files for the time being … Human-written context
   files should … be rigorously evaluated before adoption."*

   ⚠️ **Cite the §4 / Table 3 figures (2.4%, p = 0.038), not §1's "7% on average"** — the latter
   appears to be a relative framing of the same result, and quoting it unqualified is the next
   paraphrase trap in this file.

   ⚠️ **Boundary condition (appendix):** when **all documentation-related files are removed** from
   the codebase, LLM-generated context files improve performance by ~2.7% and **outperform
   developer-written ones**. The provenance advantage is **not unconditional** — in
   documentation-poor repositories the generated file is the better artifact.

   ❓ **Open methodological caveat, ours not the paper's.** The DEV arm is real files from live
   repositories, which have plausibly been revised over time; the LLM arm is first-draft output by
   construction. So the p = 0.038 contrast may **confound provenance with tuning**. We have not
   resolved this and do not rely on the contrast for more than the **Generated output shipped
   as-is** anti-pattern. It is deliberately not the basis of a scored criterion.

### C1a — Do not ship an instruction file you have never tuned

2. ● **Shepard, A. & Albrecht, J. — "Probe-and-Refine Tuning of Repository Guidance for Coding
   Agents."** arXiv:2606.20512, 18 Jun 2026. `https://arxiv.org/pdf/2606.20512`
   *Supplies:* 33.0% probe-and-refine tuned vs 28.3% static generated vs 25.5% unguided.
   ⚠️ **The p<0.001 is scoped to the two PROBE-AND-REFINE contrasts** (33.0 vs 28.3 and 33.0 vs
   25.5). The **28.3-vs-25.5 gap carries no p-value** and must not be argued in either direction.
   Those two words are the scope of the statistic — do not drop them when paraphrasing. An earlier
   paraphrase here read "p<0.001 both contrasts", and prose downstream then walked into the gap
   that opened.

   🔑 **The 33.0% arm is GENERATED-THEN-TUNED, not hand-written.** §3.1 describes the static
   condition as "tree-sitter-assisted parsing of the repository structure **and one-shot
   LLM-generated generic guidance**"; the abstract calls it "the static knowledge base **used to
   initialize** it"; contribution 1 says probe-and-refine "**refines a statically generated**
   repository knowledge base". **§4 decomposes the gain: 7.5pp total from no-context to
   probe-and-refine — 2.8pp from the generated layer, 4.7pp from the iterative refinement** (the
   structural layer ≈ 37% of the improvement). So this study does not merely permit
   generate-then-tune; it *is* generate-then-tune.

   ⚠️ **The authors disclaim the absolute numbers.** §3.1: a 16k-token context window is "**a hard
   truncation we impose** … These constraints result in **absolute resolve rates well below what
   larger-context configurations achieve. Thus the main contribution of our work in this space is
   the relative comparison across conditions, not the absolute numbers.**" Quote 33.0/28.3/25.5 as
   *between-condition* evidence only; they are not a benchmark to measure yourself against.

   ⚠️ **The advantage is budget-dependent.** §6/Fig. 7: "**At 25 steps, all conditions are
   equivalent.**" The unguided baseline is flat at 25% regardless of budget; probe-and-refine is
   the only condition still improving beyond 100 steps. Every headline number is at **200 steps**.
   §4 narrows it further: of 500 instances, 342 are a hard core where guidance does not help and 65
   an easy core — "**the middle 93 instances are where guidance matters**."

   🚨 **Guidance is not portable across models.** §1 contribution 4 / §7: "a capacity-constrained
   model cannot sustain the tuning loop, and **guidance calibrated for one model's behavioral
   profile actively destabilizes a different model's agent loop**." This is a live hazard for any
   Workspace pointing several models at one instruction file, which is the common case here.
3. ● arXiv:2602.11988 (above) — **re-scoped, not withdrawn.** Supplies C1a's two non-tuning facts:
   that an untuned file of **either** provenance fails to significantly beat having no file, and
   that **among files shipped untuned, developer-written beat LLM-generated (p = 0.038)** — the
   only provenance contrast in either source that reached significance. The **Generated output
   shipped as-is** anti-pattern rests on that contrast and on nothing wider. **R5 does not**: R5 is
   scored on tuning alone, because that contrast does not reach significance against the no-file
   baseline and cannot carry a scored row.

   🚧 **Scope note — where we knowingly stop short of the source.** §1 recommends omitting
   LLM-generated context files outright. We do **not** adopt that, and the reason is measured
   rather than asserted: the arm that failed here was generated-**and-shipped**, whereas
   generated-**and-tuned** is the best-performing condition in either source (2606.20512's 33.0%
   arm initialises from one-shot LLM-generated guidance; see its entry above). So the blanket form
   would forbid the winning path. **This is a deliberate narrowing of a source's recommendation to
   its tested scope, not an oversight** — do not "restore" the stronger form.
   📝 Benchmark naming: 2606.20512 refers to this benchmark as **AGENTBENCH**; the current version
   of 2602.11988 calls it **CTXBENCH**. We use the primary source's name.

   ⚠️ Two withdrawn framings, recorded so neither returns. **(a)** *"…as found in the wild, which
   are overwhelmingly first drafts"* — withdrawn: this paper measures no tuning and says nothing
   about file maturity. **(b)** *"hand-authoring was measured and did not separate"* — withdrawn
   as **false**: it separated at p = 0.038. Both were attempts to make this paper reach a
   conclusion it does not support; they failed in opposite directions.

> ✅ **Defect fixed in v1.10 (open v1.3–v1.9).** C1a and R5 were phrased around *authorship* —
> "write yours by hand", "hand-authored, not generated" — and cited **2606.20512** for it, which
> has no hand-authored arm and cannot carry an authorship claim. The **direction** turned out to be
> defensible; the **citation** was wrong, and the supporting claim that generated files measured
> *worse than no file at all* overstated a result that is **not statistically significant**.
>
> The corrected position, in order of confidence: **(1)** tuning is the only thing that
> significantly beats having no context file (p<0.001); **(2)** an untuned file of either
> provenance does **not** significantly beat having none; **(3)** among untuned files,
> developer-written beat LLM-generated (p = 0.038). **R5 is scored on (1) alone**; (3) is carried
> by an anti-pattern, not by a criterion, because it does not reach significance against the
> no-file baseline. **When arguing from C1a or R5, lead with tuning and treat provenance as the
> secondary, narrower claim it is.**
>
> **Rules bought by getting this fix wrong.** Four of them came from a wrong draft of this very
> entry; rule (3) came from watching one source paraphrase another. Rule first, incident as its
> evidence.
>
> **(1) Record a source's full design, including arms no criterion currently cites.** *Draft 2
> asserted that no study behind C1a had a hand-authored arm — four lines below re-listing the study
> whose developer-committed arm is exactly that. False, load-bearing, and it survived four sweeps.
> The cause was this file: entry 1's supply line recorded findings but never the two-setting
> design, so every later reader — including the ones auditing for overreach — inherited an evidence
> base with an arm missing.* A citation record that under-describes a source manufactures confident
> false claims downstream.
>
> **(2) For any claim a rule is scored against, read the section reporting the contrast — not the
> abstract, and not this file.** *Draft 3 fixed (1) by asserting authorship "was measured and did
> not separate" — false in the opposite direction. It came from the abstract, whose "holds for
> both" sentence is scoped to the comparison against no file; the head-to-head sits in §4 and
> reaches significance.* An abstract is a citation record too, and it omits arms exactly the way
> ours did.
>
> **(3) Do not inherit a secondary source's characterisation of a primary one.** *2606.20512
> describes 2602.11988 as finding generated files "reduce resolve rates by 3%" — a direction stated
> without the non-significance the primary source reports.* That is trusting an abstract, one
> citation removed.
>
> **(4) Under-claiming is the same defect as over-claiming.** *Draft 4 asserted "no arm tested
> generate-then-tune" — false, but this one cost a claim rather than inventing one:
> generate-then-tune is 2606.20512's winning arm, and the Standard was hedging a position the
> evidence actively supports.* Both directions are the record failing to match the source; only one
> of them feels like caution, which is why it survived a round longer than the rest.
>
> **(5) Retiring an untested claim does not license asserting its reverse.** *Draft 1 replaced the
> authorship claim with "the generated file still beat no file at all" — reversing an untested
> contrast instead of retiring it.* C1a now states that contrast is untested in **both** directions.
>
> **Deliberate wording, not drift:** C1a opens *"whether the guidance has been tuned is the decisive
> variable"* rather than the source's own *"how the guidance is produced…"* — an intentional
> narrowing, because the source's phrasing is broad enough to re-admit the authorship reading.
> **Do not restore the original wording.**
>
> Four drafts, four different wrong shapes, one root: **characterising a study from a summary of
> it.**

### C1b — Anything you name will be over-applied

4. ● **Galster, M. et al. — "Harness Engineering for Agentic AI Coding Tools: An Exploratory
   Study."** arXiv:2602.14690, 16 Feb 2026. `https://arxiv.org/pdf/2602.14690`
   *Supplies:* 1.6 uses per instance when mentioned vs <0.01 when not (the ~160× figure);
   2.5 vs <0.05 for repository-specific tools. Study covers 2,853 repos.
   *Note:* this figure was verified **in full text, not the abstract** — see §15 of the Standard.

### C2 — An empty scaffold is worse than none

5. ● **Solozobov, O. — "Decision Evidence Maturity Model for Agentic AI: A Property-Level Method
   Specification."** arXiv:2605.04093, 29 Apr 2026. `https://arxiv.org/pdf/2605.04093`
   *Supplies:* the **container fallacy** — equating presence of an evidence container with
   sufficiency. Source of "score contents, never existence."

### C3 — Route, don't recite

6. ○ **Sun, Y. et al. — "Don't Retrieve, Navigate: Distilling Enterprise Knowledge into Navigable
   Agent Skills for QA and RAG."** arXiv:2604.14572, 16 Apr 2026. `https://arxiv.org/pdf/2604.14572`
   *Supplies:* navigable hierarchical skill directories over retrieval.
   *Caveat:* C3's actual stated warrant is "independently nominated as best practice by two
   surveyed teams" — this citation supports the shape, but C3 is primarily **survey-derived**.

### C4 — Attention is a budget

7. ● **Chroma Research — "Context Rot: How Increasing Input Tokens Impacts LLM Performance."**
   Jul 2025. `https://research.trychroma.com/context-rot`
   Companion toolkit: `https://github.com/chroma-core/context-rot`
8. ○ **`abhishekray07/claude-md-templates` — `principles.md`.** Community repo (~194 stars).
   `https://github.com/abhishekray07/claude-md-templates/blob/main/principles.md`
   *Supplies:* the ~50 system-prompt instructions / ~150–200 reliable-adherence ceiling / degrades
   uniformly-not-selectively claim, and the 11 rule files (~6,200 tokens) → ~93,000 tokens = 46%
   of a 200K window across 30 tool calls (traced to `anthropics/claude-code` issue #32057).
   *Caveat:* the Standard correctly labels this **community-tier**. Attribution of the figure to
   this specific repo is inferred from the verification record, not confirmed line-by-line.
9. ○ **Anthropic — "Effective context engineering for AI agents."** 29 Sep 2025.
   `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents`

### C6 — Durable and scratch separable at a glance

10. ● **Van Clief, J. & McDermott, D. — "Interpretable Context Methodology: Folder Structure as
    Agent Architecture."** arXiv:2603.16021, 17 Mar 2026. `https://arxiv.org/html/2603.16021v1`
    *Supplies:* the **factory vs. product** split (Layer 3 reference stable across runs / Layer 4
    working artifacts unique to each run). The corpus called this "the single most directly
    reusable structure found."

### C9 — Decisions are the asset

11. ● **Stetsenko, I. — "Lore: Repurposing Git Commit Messages as a Structured Knowledge Protocol
    for AI Coding Agents."** arXiv:2603.15566, 16 Mar 2026. `https://arxiv.org/pdf/2603.15566`
    *Supplies:* the **Decision Shadow** — constraints, rejected alternatives and forward-looking
    context discarded by the diff.
    *The Standard already flags this correctly:* the concept is sound, the protocol proposal is
    unvalidated.

### C10 — Independent review beats self-review

The best-cited section in the Standard — three independent results plus two panel caveats.

12. ● **"Improving LLM Output Quality by Separating Production and Review Sessions"
    (Cross-Context Review).** arXiv:2603.12123, 12 Mar 2026. `https://arxiv.org/pdf/2603.12123`
    *Supplies:* F1 28.6% fresh-session vs 24.6% same-session, p=0.008; and that reviewing twice in
    the same session did not beat once — the "context separation itself" finding.
    *Also supplies* the "absolute review performance is poor / ~29% F1" honest caveat.
13. ● **Chen, K.-Y. et al. — "The Self-Correction Illusion: LLMs Correct Others but Not
    Themselves."** arXiv:2606.05976, 4 Jun 2026. `https://arxiv.org/pdf/2606.05976`
    *Supplies:* 23–93 percentage-point correction lift from relabelling voice alone — the
    role-label-artifact / addressability mechanism.
14. ● **Wataoka, K. et al. — "Self-Preference Bias in LLM-as-a-Judge."** arXiv:2410.21819,
    29 Oct 2024. `https://arxiv.org/html/2410.21819v1`
    *Supplies:* the bias is **familiarity, not vanity** — judges over-reward low-perplexity text,
    so panels penalise correct-but-unusual answers.
15. ● **Zhao, J. et al. — "CARE: Confounder-Aware Aggregation for Reliable LLM Evaluation."**
    arXiv:2603.00039, 9 Feb 2026. `https://arxiv.org/pdf/2603.00039`
    *Supplies:* shared latent confounders induce correlated errors across vendors — the
    "if your panel always agrees, you paid three times for one verdict" warrant.
16. ○ **Zhu, Z. et al. — "CyclicJudge: Mitigating Judge Bias Efficiently in LLM-based
    Evaluation."** arXiv:2603.01865, 2 Mar 2026. `https://arxiv.org/pdf/2603.01865`
17. ○ **Gubitosa, B. (CodeRabbit) — "Code context: The evidence behind trustworthy AI code
    review."** 24 Jun 2026. `https://www.coderabbit.ai/guides/code-context`
    *Supplies:* the industry-convergence quote, "a clean-context reviewer catches bugs the coder
    can't see."
    ⚠️ **Vendor with a direct interest** — CodeRabbit sells independent AI review and the article's
    thesis is that self-review fails. Cite only for convergence, never as evidence.

### C12 — More agents is not more capability

18. ● **Tran, D. & Kiela, D. — "Single-Agent LLMs Outperform Multi-Agent Systems on Multi-Hop
    Reasoning Under Equal Thinking Token Budgets."** arXiv:2604.02460, 2 Apr 2026.
    `https://arxiv.org/pdf/2604.02460`
    *Supplies:* the equal-token-budget result and the confound in reported multi-agent gains.
19. ● **Cognition — "Don't Build Multi-Agents."** 2025. `https://cognition.com/blog/dont-build-multi-agents`
20. ● **Cognition — "Multi-Agents: What's Actually Working."** Apr 2026.
    `https://cognition.com/blog/multi-agents-working`
    *Supplies (C12a):* the revised position — writes single-threaded, extra agents contribute
    intelligence rather than actions. **19 is superseded by 20; the Standard cites the pair
    deliberately** to show the position moved.
21. ● **Anthropic — "How we built our multi-agent research system."** Jun 2025.
    `https://www.anthropic.com/engineering/multi-agent-research-system`
    *Supplies (C12b):* the vendor's own stated boundary — shared-context and high-dependency
    domains are a poor fit, naming coding explicitly.

---

## 1a. v1.4 — External tools and declining a rule (C13–C16, SOP-7)

**Compiled 2026-07-27 from a two-model research pass — the same question put independently to
two models — then verified by reading every source below at its primary location. The raw
responses, the liveness check and the model-by-model comparison are kept in the project's
research corpus and are not reproduced here; the verdicts and the rejections are.**

⚠️ **Different method from §1 and §2, and stronger.** Those sections were reconstructed by matching
the Standard's phrasing back to a research corpus. **These entries were read.** Where a source was
paywalled, offline or returned a 404 it is listed under *rejected* rather than cited — the v1.4 pass
produced eleven citable sources and seven rejections, and the rejections are the more useful half.

### C15 — Elevated code resolves by absolute path (best-supported material in the Standard)

1. ● **CWE-426 — Untrusted Search Path.** MITRE. `https://cwe.mitre.org/data/definitions/426.html`
   *Supplies:* the vulnerability class for bare-name resolution under privilege — *"searches for
   critical resources using an externally-supplied search path that can point to resources that are
   not under the product's direct control."*
2. ● **CWE-732 — Incorrect Permission Assignment for Critical Resource.** MITRE.
   `https://cwe.mitre.org/data/definitions/732.html`
   *Supplies:* the writable-target half — *"specifies permissions for a security-critical resource
   in a way that allows that resource to be read or modified by unintended actors."*
   ⚠️ **Use this, not CWE-427, for the "an absolute path is not sufficient" argument.** Both models
   returned CWE-427 *Uncontrolled Search Path Element* and both were loose: CWE-427 describes a
   **search path containing** an attacker-controlled location, whereas C15 claims **no search path is
   needed at all**. CWE-427 remains correct for the resolution-order half only. *This was the one
   citation both models agreed on and both got wrong — agreement is a signal about confidence, not
   about fit.*
3. ● **IEEE Std 1003.1 / The Open Group Base Specifications — `unlink`.**
   `https://pubs.opengroup.org/onlinepubs/9699919799/functions/unlink.html`
   *Supplies:* the POSIX inversion, verbatim — *"**[EACCES]** Search permission is denied for a
   component of the path prefix, or **write permission is denied on the directory containing the
   directory entry to be removed.**"* The entry's own mode and owner are not a factor. `S_ISVTX`
   appears separately under *Directory Protection* — the sticky-bit caveat.
4. ● **The Open Group — `rename`.**
   `https://pubs.opengroup.org/onlinepubs/9699919799/functions/rename.html`
   *Supplies:* the same for `rename` — *"one of the directories containing old or new denies write
   permissions."*
5. ● **[MS-ADTS] §6.1.3.4 — Blocking Implicit Owner Rights.** Microsoft.
   `https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-adts/fb7c101d-ec8b-4fbf-bca8-7d7c2d747d0c`
   *Supplies:* why ownership is decisive — *"The Owner of a security descriptor is implicitly granted
   READ_CONTROL and **WRITE_DAC** rights by default."*
   ⚠️ **State it as a default, not an absolute:** the same page records those implicit rights being
   blocked when `BlockOwnerImplicitRights` is set.
6. ● **`sudoers(5)`.** `https://man7.org/linux/man-pages/man5/sudoers.5.html`
   *Supplies:* the elevated-contexts note — and argues C15 independently. `secure_path` exists *"to
   help protect scripts and programs that execute other commands without first setting PATH to a safe
   value … a user with limited privileges may be able to run arbitrary commands by manipulating the
   PATH if the command being run executes other commands **without using a fully-qualified path
   name**."*
   ⚠️ Also the source of the *"where configured"* qualifier: this page says the option is **disabled
   by default**, while sudo 1.9.16 release material says it is enabled by default. Version- and
   distribution-dependent — do not state it flatly.
7. ○ **`systemd.exec(5)`.** `https://man7.org/linux/man-pages/man5/systemd.exec.5.html`
   *Supplies:* that units carry their own resolution path — `ExecSearchPath=` *"overrides `$PATH` if
   `$PATH` is not supplied by the user through `Environment=`…"*

### C16 and SOP-3's `Revisit if:` — risk acceptance

8. ● **NIST SP 800-53 Rev. 5, RA-7 *Risk Response*.**
   `https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf`
   *Supplies:* two things, one of them a limit on our own claim.
   **(a)** Acceptance requires *"accepting risk with appropriate **justification or rationale**"* —
   **and nothing further. No revisit condition, no review date, no trigger.** So `Revisit if:` is a
   **local extension**, in the same position as C8, and must not be presented as established practice.
   **(b)** *"Risk response addresses the need to determine an appropriate response to risk **before**
   generating a plan of action and milestones entry … **if the risk response is to mitigate the
   risk**, and the mitigation cannot be completed immediately, a plan of action and milestones entry
   is generated."* ⇒ **The POA&M is a remediation instrument. An accepted risk does not generate one**
   — so the date-based federal artifact is not the acceptance artifact and does not bind §14.
9. ● **NIST SP 800-37 Rev. 2**, Appendix F (reauthorization).
   `https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-37r2.pdf`
   *Supplies:* directional support for *event over date* — *"In general, reauthorization actions may
   be time-driven or event-driven. However, under ongoing authorization, reauthorization is **in most
   instances, an event-driven action** … in response to an event that results in security and privacy
   risk above the level of risk previously accepted."*
   ⚠️ **Directional, not mandatory.** 800-37r2 treats both modes as legitimate. Argue the direction of
   travel; do not claim a requirement.
10. ○ **NIST SP 800-137**, §3.2.2 Event-Driven Assessments.
    `https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-137.pdf`
    *Supplies:* that trigger criteria should be written down — expected output is *"**Documented
    criteria and thresholds** for event-driven assessments/authorizations."*
    ⚠️ **Does not support the third-party-observable test.** That refinement is ours alone.

### §12 anti-pattern — *unfixed generator*

11. ● **ISO 9001 Auditing Practices Group — *Review of Nonconformity, Correction and Corrective
    Action*, 2015.** `https://committee.iso.org/files/live/sites/tc176/files/documents/ISO%209001%20Auditing%20Practices%20Group%20docs/Auditing%20General/APG-ReviewNonconformity2015.pdf`
    *Supplies:* the distinction the anti-pattern rests on. Response to a nonconformity has three
    parts — *"correction, analysis of cause, and corrective action"* — and *"for software, **it is
    inadvisable to implement a correction until the cause is known**."* Fixing the artifact is the
    *correction*; fixing the spec that generates it is the *corrective action*.

### Rejected during the v1.4 pass — do not resurrect

| Source | Why rejected |
|---|---|
| **CWE-427** for the writable-target claim | Adjacent, not identical. Correct for resolution order only |
| **OMB M-02-01** (POA&M) | The page self-declares *"historical material … **not current OMB guidance**."* RA-7 carries the point and is current |
| **NTIA / CISA SBOM minimum elements** | Supply-chain **transparency**, not tool **discovery**. No support for SOP-7's discoverability claim |
| **Google SRE Book** — `sre.google/sre-book/documentation/` | **404.** It was the sole source offered for "recorded decisions" and "derived docs go stale" |
| **`google.com/search?q=…`** | A search query returned as a citation |
| **ISO/IEC 27005** | Cited as :2022, URL resolves to :2018, paywalled catalogue listing with no normative text. One model marked its inability to read it; the other did not |
| **`csf.tools`** RA-7 mirror | 403, and third-party where an authoritative source exists |
| **CSRC `/pubs/…/final` landing pages** | Do not contain the quoted passages — cite the `nvlpubs` PDFs |

---

## 1b. v1.9 — Least privilege, and how a control is proposed (C17, C18)

**Compiled 2026-07-28. Same method as §1a and the same bar: every source below was fetched and
read, and the quoted text was extracted from the retrieved document — not from an abstract, a
landing page or a summary.** Metadata was cross-checked against two independent indexes (Crossref
and OpenAlex/Semantic Scholar) before any source was fetched.

⚠️ **Do not treat an HTTP 403 as a dead link.** Three ACM DOIs in this pass return 403 to a
scripted fetch and are entirely live; the same misreading produced the 39 bogus DEAD verdicts
described at the top of this file. Where the publisher blocked retrieval, the paper was located at
its **workshop proceedings** instead (`nspw.org`), which is the authoritative copy for both NSPW
entries below.

### C17 — Lowest privilege that achieves the goal

1. ● **Saltzer, J. H. & Schroeder, M. D. — "The Protection of Information in Computer Systems."**
   *Proceedings of the IEEE* 63(9), 1975. `doi:10.1109/proc.1975.9939`
   Read at the author's canonical copy: `https://web.mit.edu/Saltzer/www/publications/protection/Basic.html`
   *Supplies:* the principle verbatim — *"**Least privilege:** Every program and every user of the
   system should operate using the least set of privileges necessary to complete the job. Primarily,
   this principle limits the damage that can result from an accident or error."*
   ⚠️ Cite the `Basic.html` section, not the paper's landing page — the landing page carries the
   abstract only, and the principles are one level down.
2. ● **NIST SP 800-53r5 — AC-6, Least Privilege.**
   Read from the machine-readable catalogue: `https://raw.githubusercontent.com/usnistgov/oscal-content/main/nist.gov/SP800-53/rev5/json/NIST_SP-800-53_rev5_catalog.json`
   *Supplies:* the extension from users to **processes**, which is the half C17 actually rests on —
   *"applied to system processes, ensuring that the processes have access to systems and operate at
   privilege levels no higher than necessary to accomplish organizational missions or business
   functions."*

**No external source supports C17's actual contribution.** Neither reference addresses privilege
that *outlives its justification*, which is the failure C17 records and the reason the rule exists.
That claim rests on one recorded instance and is marked as such in the Standard. The citations
establish the principle, not the failure mode — do not let them launder the claim status.

### C18 — Alternatives are priced together

3. ● **Herley, C. — "So Long, and No Thanks for the Externalities: The Rational Rejection of
   Security Advice by Users."** NSPW 2009. `doi:10.1145/1719030.1719050`
   Read at `https://www.nspw.org/papers/2009/nspw2009-herley.pdf` (the ACM DOI returns 403 to
   scripted fetch and is live in a browser).
   *Supplies:* the reclassification of refusal as economics rather than obstruction — *"users'
   rejection of the security advice they receive is **entirely rational** from an economic
   perspective. The advice offers to shield them from the direct costs of attacks, but burdens them
   with far greater indirect costs in the form of effort."*
   ⚠️ **Population-scale result, and C18 applies it at n=1.** The rationality finding is derived from
   aggregate arithmetic over the whole US adult population, and the paper says so of itself: *"It is
   hard to make this calculation for an individual user. However aggregate estimates across the whole
   population are easier to reason about."* **Entry 4 is what rescues this** — the compliance budget
   is explicitly an individual-level construct (*"the economics of compliance from an individual's
   point of view"*), so the pair carries the claim where Herley alone would not. Cite them together
   for any statement about a single owner.
4. ● **Beautement, A., Sasse, M. A. & Wonham, M. — "The Compliance Budget: Managing Security
   Behaviour in Organisations."** NSPW 2008. `doi:10.1145/1595676.1595684`
   Read at `https://www.nspw.org/papers/2008/nspw2008-beautement.pdf`.
   *Supplies:* the mechanism that makes an unnecessary control costly rather than merely unwelcome —
   compliance is *"a finite resource that needs to be carefully managed"*, and *"individuals and
   organisations place different values on the cost and benefits"* of security behaviours.

**Neither source addresses the ratchet or the prerequisite framing.** They establish that owner
resistance carries information and that compliance capacity is finite. The sequencing failure — two
sufficient fixes applied in order, each retroactively justifying the other's redundancy — is argued
from mechanism and one recorded case, and the Standard says so.

### C18 — when the owner's choice looks wrong

5. ● **NIST SP 800-37 Rev. 2 — *Risk Management Framework for Information Systems and
   Organizations*.** `https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-37r2.pdf`
   *Supplies:* where the authority to accept risk actually sits, which is what makes deferring to
   the owner correct rather than merely polite — the authorizing official *"is the only person who
   can accept risk"*, and is *"the only organizational official who can accept the security and
   privacy risk to organizational operations, organizational assets, and individuals."* Also the
   basis for recording it: risk acceptance is an explicit, documented decision, and under ongoing
   authorization the official remains *"responsible and accountable for explicitly understanding and
   accepting the risk."*
   ⚠️ **Scope — what transfers is the separation, not the office.** The authorizing official is a
   **formally designated** role (*"a senior official or executive with the authority to formally
   assume responsibility…"*, typically holding budgetary oversight), bounded by organizational risk
   tolerance and a risk-executive function. A Workspace owner has none of that apparatus, so do not
   argue from the AO's designation. What transfers cleanly is the **assessor ≠ acceptor separation**
   — the party who evaluates risk is not the party who accepts it — and that is all C18 needs for
   *"by right rather than by courtesy."*
6. ● **ACM Code of Ethics and Professional Conduct** (§1.2, §2.5). `https://www.acm.org/code-of-ethics`
   *Supplies:* **the obligation half only** — a computing professional *"has an additional obligation
   to report any signs of system risks that might result in harm"*, and §2.5 requires *"comprehensive
   and thorough evaluations… including analysis of possible risks."*
   ⚠️ **It does NOT supply the limit half, and an earlier draft of this file claimed it did** — that
   draft called the "capricious" line *"the one that bounds escalation"*, which names the error
   precisely: the Code bounds nothing of the sort. The
   full passage runs: *"…report any signs of system risks that might result in harm. **If leaders do
   not act to curtail or mitigate such risks, it may be necessary to 'blow the whistle' to reduce
   potential harm.** However, capricious or misguided reporting of risks can itself be harmful.
   **Before reporting risks, a computing professional should carefully assess relevant aspects of the
   situation.**"* Two corrections follow. First, the sentence *preceding* the "capricious" line
   licenses escalation precisely when the decision-maker declines to act — so the source's net
   direction on *"leader won't act"* is **escalate**, not stop. Second, "capricious or misguided" is
   bounded by the sentence *after* it, which prescribes careful assessment: **the ACM's limit is on
   the groundedness of a report, not its frequency.** Quoting it for a *count* is arguing from a
   passage that measures *quality of basis* — the same move as C1a/R5's authorship-from-tuning
   overread recorded and corrected above. **Do not cite the ACM for the one-round bound.** That bound now rests on
   entry 5's authority allocation and the absence of a chain of command above the owner.
7. ○ **Bezos, J. — 2016 Letter to Shareholders.** Amazon.com Inc., filed as Exhibit 99.1.
   `https://www.sec.gov/Archives/edgar/data/1018724/000119312517120198/d373368dex991.htm`
   *Supplies:* the disposition required after deferring — *"use the phrase 'disagree and commit'…
   If you have conviction on a particular direction even though there's no consensus"* — and Bezos'
   own worked example, *"I disagree and commit and hope it becomes the most watched thing we've ever
   made."* ○ rather than ● because it is a management essay, not a standard; it names the posture
   the Standard wants and supplies no evidence for it.
   ⚠️ **Fetch from SEC EDGAR with a User-Agent carrying a contact address**, per SEC access policy —
   a generic browser UA returns 403 and reads as a dead link.

8. ● **AHRQ TeamSTEPPS — *Tool: Two-Challenge Rule*.** Agency for Healthcare Research and Quality.
   `https://www.ahrq.gov/teamstepps-program/curriculum/mutual/tools/rule.html`
   Corroborated at Loyola's TeamSTEPPS IPE module,
   `https://stritch.luc.edu/lumen/meded/softchalkhdht/teamsteppsipe/mobile_pages/teamsteppsipe28.html`
   *Supplies:* the **first-stage** trigger, which is not C18's — it applies *"if your initial
   assertion is **ignored**"*, requiring the concern to be voiced *"at least two times to ensure that
   it has been heard."* That is the source of C18's requirement that a round be *received and
   answered* to count.
   ⚠️ **The rule has a second stage, and it covers C18's case and points the other way.** *"If the
   outcome is still not acceptable: The challenger must take a stronger course of action. The
   challenger should turn to the supervisor and move up the chain of command if necessary."* That
   triggers on the **outcome** — i.e. on being **heard and overruled**, which is exactly C18's
   situation — and prescribes escalation. An earlier draft of this file claimed *"C18 governs the
   second; this rule governs the first."* **That was wrong: the source governs both.** What actually
   distinguishes them is the apparatus the second stage presumes — a chain of command above the
   person who decided. Under entry 5's allocation there is none above a Workspace owner, so the
   escalation this rule prescribes has nowhere to go. **That, and not the trigger, is what bounds
   C18 to one round.**
   *Corrected scope note:* the domain framing — that these sources situate the rule in high-stakes
   real-time operational settings, aviation and clinical care — **is the argument that survives**,
   because it travels with the chain-of-command apparatus. An earlier version of this note told the
   reader the opposite: to rely on the trigger distinction and avoid the domain argument. It was
   exactly backwards, and it is recorded here rather than quietly rewritten.
   ⚠️ **Cite this URL, not the pocket guide.** `…/instructor/essentials/pocketguide.pdf` now
   **returns `200` while redirecting to a generic landing page** — a soft-404. An earlier pass in
   this project read that as evidence the rule could not be sourced; it was a wrong URL, not a
   missing document, and the correction came from the owner rather than from the search.
   *Scope note, non-blocking:* the sources situate the rule in high-stakes real-time operational
   domains — aviation and clinical care — by construction rather than by an explicit exclusion
   clause. Rely on the trigger distinction above, which is stated in the source; do not lean on the
   domain argument, which is inferred from context.

### Rejected during the v1.9 pass — do not resurrect

9. ❌ **Freedman, J. L. & Fraser, S. C. — "Compliance Without Pressure: The Foot-in-the-Door
   Technique."** *JPSP* 4(2), 1966. `doi:10.1037/h0023552`
   **Dropped on fit, not availability.** Foot-in-the-door concerns a small request preceding a
   larger one. C18's failure was a mitigation **misdescribed as a prerequisite** — a different
   mechanism. Citing it would repeat the C1a/R5 overread this file records and corrects above:
   arguing from data that measures something adjacent to the claim.
10. ⚠️ **Staw, B. M. — "Knee-Deep in the Big Muddy: A Study of Escalating Commitment to a Chosen
   Course of Action."** *OBHP* 16(1), 1976. `doi:10.1016/0030-5073(76)90005-2`
   Apt for the ratchet, and **not used.** No open-access copy exists via Unpaywall, OpenAlex or
   Semantic Scholar; metadata is confirmed but the text was never retrieved. **Do not quote it
   until someone has read it.** The same applies to Staw 1981 (`doi:10.2307/257636`) and Brockner
   1992 (`doi:10.2307/258647`), both checked and both closed.
11. ⚠️ **Adams, A. & Sasse, M. A. — "Users Are Not the Enemy."** *CACM* 42(12), 1999.
   `doi:10.1145/322796.322806`
   Live, paywalled, content not retrieved. Its argument is substantially covered by entries 3 and 4,
   so it was cut rather than cited unread. Four verified sources beat six gestured at.
12. ❌ **The "two-man rule" / dual control** (e.g. `https://williamhale.co.uk/two-man-rule-explained-how-dual-control-improves-access-control-security/`)
   **Checked and excluded — different problem entirely.** Dual control requires two authorised
   principals to jointly execute a sensitive *action*; it is an access-control mechanism, not a
   protocol for handling disagreement about a decision. Named here only because the similar name
   makes it a plausible wrong turn for the next reader.

⚠️ **Method note — an empty search result is not evidence of absence.** DuckDuckGo served results
for the first query of this pass and zero for every subsequent one; the harvester's *"tried 0
sources"* is indistinguishable from *"no such paper"* without a control. Every empty result in this
pass was re-run against a control query known to be indexed. The reliable sources were APIs
(Crossref, OpenAlex, Semantic Scholar, Unpaywall) and direct proceedings URLs — scraping was the
weakest link and the least necessary one.

---

## 2. The SOPs

The SOPs are **substantially thinner on external citation than the Charter**, and lean on the
five-Workspace survey. This is not a gap to be filled by finding more citations; it is what the
evidence actually looks like.

### SOP-2 (documenting a process) and SOP-4 (automation and health signals)

22. ● **Google — SRE Workbook, Ch. 11 "Being On-Call."** 2018. `https://sre.google/workbook/on-call/`
    *Supplies:* the alert↔playbook pairing invariant; "a deterministic runbook is a bug report
    against your automation"; staleness rate bounded by deploy rate; keep entries general so they
    change slowly.
    *Flagged as older, retained deliberately* — still definitional, no successor has displaced it.
    ⚠️ **The source itself calls playbook granularity "a contentious topic."** Also a **terminology
    conflict**: SRE uses "playbook" for the alert-response doc; ITSM/DR sources invert it.
23. ○ **Sérié, E. — "OxyMake: A Formally-Specified, Content-Addressable Workflow Engine."**
    arXiv:2606.20989, 18 Jun 2026. `https://arxiv.org/pdf/2606.20989`
    *Supplies:* docs-as-tests, executable examples that fail the build (SOP-2 step 2).

### SOP-6 (pipeline Workspaces)

24. ● arXiv:2603.16021 (entry 10) — **this is the "one published paper" SOP-6 refers to.**
    SOP-6 is otherwise an explicitly labelled **local convention**; a deliberate search found no
    spec, standard, or controlled study for queue-folder / directory-as-state-machine patterns in
    agent workspaces.

### Rubric — scored per layer, never as a total

25. ● **Octopus Deploy — "DevOps Uses A Capability Model, Not A Maturity Model."** Mar 2023.
    `https://octopus.com/blog/devops-uses-capability-not-maturity`
    *Supplies:* the capability-checklist-not-maturity-ladder decision — why the rubric refuses a
    total score and refuses to rank Workspaces against each other.
26. ○ **Google Cloud / DORA — State of AI-assisted Software Development 2025.**
    `https://dora.dev/dora-report-2025` · announcement:
    `https://cloud.google.com/blog/products/ai-machine-learning/announcing-the-2025-dora-report`
27. ○ arXiv:2605.04093 (entry 5) — per-dimension scoring as what makes a rubric actionable.

### General reference

28. ○ **AGENTS.md specification.** Living spec, undated. `https://agents.md/`
    Now stewarded by the Agentic AI Foundation (Linux Foundation); 60k+ repos.

---

## 3. Claims in the Standard with **no** external citation

Listed because a citation list that hides its gaps is doing the thing C2 warns about.

| Claim | Basis |
|---|---|
| **C5** — one authored home per rule | Survey (one team re-authored policy across 5–7 docs until two contradicted) |
| **C7** — green is a claim, not a fact | Survey: four independent instances in one round, including this project's own citation check |
| **C7a** — absence of signal is the alert | GitLab 2017 data-loss incident — public and well-documented, but **not in the research corpus**; no URL was carried |
| **C7b** — PowerShell 5.1 `&&`, `-ErrorAction`, `$LASTEXITCODE` traps | Local, reproduced in-house |
| **C8** — record execution mode | **Explicitly labelled a local extension.** A deliberate search found no authoritative source. Internal incident evidence only |
| **C11** — address by stable ID | Survey: one sync tool duplicated a backup tree |
| **C17** — a privilege *outlives its justification* and nothing re-checks it | One recorded instance (§1b). The least-privilege principle itself **is** cited; this failure mode is not, and the two must not be conflated |
| **C17** — reducing privilege can remove the ability to reverse it | One recorded instance, local, reproduced |
| **C18** — the ratchet, and the prerequisite framing | One recorded case (§1b). The cost-signal reading of resistance **is** cited; the sequencing failure is not |
| **C18** — a Workspace has no chain of command above its owner | **Structural claim, asserted.** NIST (§1b entry 5) supplies that acceptance is a *single role's* call; it does not supply *"and nobody is above that role"* — RMF's own authorizing official is accountable upward. Stated as *generally*, with an explicit exception clause. This premise is what bounds C18 to one round, so it is the load-bearing uncited claim in the criterion |
| **SOP-1, SOP-3, SOP-5** and most of **SOP-4** | Survey of five production Workspaces |

The corpus's own **thin-evidence flag** belongs here too: "runbook-as-code" and "intelligent
runbook execution" as categories are dominated by vendor marketing, with no independent measurement
that executable runbooks reduce MTTR versus well-maintained static ones. The Standard correctly
does not claim it.

---

## 4. Rejected during verification — do not resurrect

29. ❌ **Jha, S. et al. — "Think Locally, Explain Globally: Graph-Guided LLM Investigations."**
    arXiv:2601.17915. `https://arxiv.org/pdf/2601.17915`
    Widely quoted as the source of a multi-agent failure distribution (step repetition ~15.7%,
    termination blindness ~12.4%, ~28% together). **The paper is about graph-guided investigation
    of operational data.** The distribution is not in it. Excluded from the Standard.
30. ⚠️ **Cemri, M. et al. — "Why Do Multi-Agent LLM Systems Fail?" (MAST).** arXiv:2503.13657,
    17 Mar 2025. `https://arxiv.org/abs/2503.13657`
    The taxonomy is real and well-grounded; its **authors state category percentages are
    dataset-dependent.** Cite the taxonomy, never a precise split.
31. ❌ **`watchflow.io/blog/why-cron-jobs-fail-silently`** — hard 404, one of only 8 genuinely dead
    URLs in the corpus. The argument it supported is independently sourced and survives.

Six further arXiv IDs in the corpus were mapped to claims unrelated to their actual contents
(2310.01798, 2405.14092, 2605.07395 and others). Three of those papers were **re-used correctly**
elsewhere in this list after re-verification — 2410.21819 and 2603.12123 among them — which is why
the entries above cite them for what they actually say, not what the corpus originally claimed.

---

## Two headline studies genuinely disagree

Recorded in the Standard's §15 and worth carrying here: one study measured **efficiency** on
focused changes and found context files produced less runtime and fewer output tokens;
arXiv:2602.11988 measured **correctness** and found success rates fell while cost rose >20%. The
reconciliation the Standard offers is that context files **reduce wandering without improving the
destination.** C1 and C1a are written to survive both results. Anyone citing one alone is giving
you half the picture.

---

*Corpus, verification passes and the live-check script are held in the maintainer's local research
corpus and are not published — `citations.csv`, `livecheck.tsv`, `check-urls.sh`, and the two
model-specific notes.*
