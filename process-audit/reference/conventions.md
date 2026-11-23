# Declared conventions

## Contents

- Why this file exists
- 1 · The working ceiling of 15 criteria per declared type
- 2 · The 12-month calendar backstop
- 3 · The three-value overall position
- 4 · The five acquisition modes
- 5 · The six currency values
- 6 · The core-plus-module split, and its membership
- 7 · The blocking test and the blocking labels
- 8 · The register core
- 9 · Where the provisional marker lives
- 10 · Splitting this skill across files
- The calibration record

## Why this file exists

Every number and every closed vocabulary in this skill is a **choice**, not a finding. Some of them
look derived. None is.

The honest form for such a value is the one this file uses throughout: state it, state the reason,
and state what would replace it — never present it as empirical. "12-month review backstop chosen
for burden reasons" is honest. "Conclusion valid for 12 months" is not, and the difference is the
whole point.

A convention that is scheduled to be measured is defensible. A derived-sounding number is not.

---

## 1 · The working ceiling of 15 criteria per declared type

**The convention.** At most 15 criteria per declared process type: the 10 core criteria plus at
most 5 module criteria. A hybrid counts each declared type as its own run for the ceiling
(`SKILL.md` Step 1), so a prompt-chain and agentic-loop hybrid assesses 14 criteria on its chain
and 15 on its loop, not 19 in one run.

**Why this value.** It is a layout and burden bound, inherited from an earlier design lineage for
this skill where it was a design target. It is **re-labelled here as a burden convention** and
carries none of its former standing. It is retained only because it is a number the practitioner
already works to, and because a bound the assessor will actually respect is worth more than a
better-argued one they will not.

**What it is not.** It is not a derived count and not a completeness claim. No evidence-based
universal item count for a checklist or rubric was located in the source material, and any round
number is a layout choice unless a model derives it. Length alone cannot establish that an
instrument is complete enough. Competing prescribed maxima — 15, 10, 5–9, 10–15 — are conventions
too, not positions in an evidential dispute.

**What would settle it.** A local derivation against a stated objective, using the calibration
record below: marginal findings per successive block of assessment effort, by process type. The
stopping question is "what additional decision-relevant coverage would the next criterion buy, at
what assessment cost?" — and that requires runs that have not happened yet.

**One thing the ceiling must never do.** A unique high-consequence criterion is not deleted to hit
a length target. Correlation between two criteria is the wrong reason to remove either when they
protect against different failures.

**What counting per type costs.** The bound now limits the burden of each declared type, not of a
whole audit. A hybrid of two types can carry up to 30 criterion assessments, because the core is
assessed on each type's part — against 15 for a single type. That is accepted rather than trimmed:
where the ceiling and a criterion collide, the ceiling yields and the criterion does not. The
calibration record, kept by process type, is what will show whether that burden is borne.

---

## 2 · The 12-month calendar backstop

**The convention.** Where no change trigger has fired, a stored conclusion is reviewed after 12
months.

**Why this value.** It is a burden choice: an annual cycle is a period the practitioner is already
organised around, and the backstop's job is only to catch what the change-detection mechanism
missed. Change triggers remain primary.

**What it is not.** It is not a lifetime, a shelf life or an expiry. Certification intervals in
published standards — a three-year cycle, an annual scope confirmation — have no located empirical
calibration either; the requirements exist, their calendar lengths are not experimentally
established lifetimes of conclusions. Decay figures measured in one discipline (roughly half of a
guideline set outdated after ~5.8 years, a median of ~5.5 years free of an update signal) do not
transfer here; the heterogeneity *inside* that one discipline is itself the argument against
importing a period.

**Why there is a backstop at all,** given that a review of 377 systematic reviews found only about
9% of updated ones changed conclusion: because that finding does not reach the case where detection
is weakest. For a drifting pipeline or a model-mediated process, "no edits since assessment" proves
nothing, and change triggers alone would never fire.

**Why not tiered by consequence.** No calibration was located for any tier, so tiering multiplies
uncalibrated numbers by three and buys precision the evidence cannot support.

**What would settle it.** The reuse-mechanism self-audit in [mechanisms.md](mechanisms.md):
periodically re-run a sample of `reuse-supported` conclusions. The disagreement rate is the most
direct local evidence about whether dependency tracking is missing causes of invalidation, and it
is what turns this interval into a measured one.

---

## 3 · The three-value overall position

**The convention.** The overall position is one of `acceptable`, `not acceptable`, `suspended`, and
is always printed with its qualifier: *for the declared scope, on the criteria assessed, for this
process type* — for a hybrid, *for the declared types*, and still one position (`SKILL.md` Step 5).

**Why these names.** `suspended` names the action — reliance is suspended — rather than a quality,
which is what keeps it from being read as a soft failure. Three reports gave three incompatible
answers for what a gate does when the evidence is insufficient; suspension is the only
representation that obeys both constraints at once, that missing evidence must not be forced into a
failure and must not read as a pass.

**What it is not.** Not a score, not a grade, not a maturity level, and not comparable across
process types. The qualifier is not decoration: a blocking criterion can exist for one type and not
another, so the position is type-conditioned.

**What would settle the naming.** Nothing in the source material — no report names this set. It is
a naming choice, and the cost of changing it later is a rename, not a re-interpretation of stored
findings.

---

## 4 · The five acquisition modes

**The convention.** A closed list of five modes, printed alphabetically: `document or artifact`,
`independent reperformance`, `instrumented measurement`, `observation or execution trace`,
`subject claim`.

**Why five and not six.** The source table has a sixth row, repeated independent
observations. That is a statement about **coverage**, and coverage is already one of the evidence
fields — carrying it as a mode would duplicate one field inside another and let a finding record
repetition in two places that can disagree. The source itself grades that row differently from the
other five, which is consistent with it not being the same kind of thing.

**Why alphabetical.** The source table runs weakest to strongest. Any list printed in ascending
order of apparent strength will be read as a ranking whatever the surrounding text says, and the
measured evidence on condensation says the qualification is exactly what drops when a finding is
shortened. Alphabetical order is arbitrary, which is the property wanted here.

**What it is not.** Not a scale. Position licenses nothing. This is a nominal vocabulary, and the
epistemic work is done by the claim-ceiling sentence and the other three evidence fields.

**What would settle it.** Nothing needs to: adding a mode later invalidates no earlier finding.
That is precisely why this could be closed now, and it would not be true of a scale.

---

## 5 · The six currency values

**The convention.** `current`, `reuse-supported`, `stale`, `unverified`, `superseded`, `revoked`.

**Why six.** Two source lists disagree and neither ranks itself. One carries `current` / `reused` /
`stale` / `unverified`; the other carries a five-value set that merges stale and unverified into one
label and adds `superseded` and `revoked`. Merging would drop a distinction the first list holds — a
*detected relevant change* and an *undeterminable applicability* are different situations calling
for different next actions — and dropping a distinction is the collapse this register exists to
prevent. Both additions are kept, both originals are kept.

**What it is not.** Not validated. No controlled study compares an explicit stale-or-unverified
state against silently coercing staleness to a pass or a fail; that is recorded in the source
material as one of the clearest evidence gaps in the area. The two-axis outcome-by-currency
representation is a logically conservative consequence of the evidence, not a validated interface
design.

**What would settle it.** Local use: whether the two states ever diverge in practice. If, after
enough runs, no conclusion is ever `stale` without also being `unverified`, merge them.

---

## 6 · The core-plus-module split, and its membership

**The convention.** A common core of 10 criteria plus one module of at most 5 per process type.
Modules never add into the core; no total crosses a type boundary.

**Why this architecture.** It is the only one of the three candidates with an evidentiary rationale
behind it. A single flat set with per-item applicability marking would force the instrument to
express its own ignorance as `not applicable` — the one state whose rate of misuse cannot be
established, because no defensible estimate of it was located. Each `not applicable` ground stays
inspectable; what cannot be established is how often the state is misused. No comparison of an
a-priori taxonomy of quality dimensions against failure-derived generation was located at all.

**What the membership is not.** The selection of *which* clusters became criteria is judgement
applied to the source dossier's 43 core clusters, on three stated tests: applicability to all six
types, statability as a binary condition on a named observable, and being a property of the audited
process rather than of the audit. Those tests are local operationalisation. The dossier's own
organisation is by failure-derived cluster, and it carries no category structure to inherit.

**What must not be claimed of the dimensions.** Named categories do not acquire measurement reality
by being named. Whatever the core and the modules are called, **they may not be reported as
independently meaningful scores** until the assessor's own re-rating data shows they actually
diverge — and the halo evidence says a single rater judging several dimensions of the same object is
exactly the configuration where separability is most likely to be lost.

**What would settle it.** Whether the split is right is an empirical question on which no literature
was located: the source material holds no measurement-invariance evidence for one instrument
spanning manual workflows, scripts, pipelines, prompt chains and agentic systems. Locally, what
would move it is observed non-applicability rates per type and whether the module criteria ever
change a decision the core did not already reach.

---

## 7 · The blocking test and the blocking labels

**The convention.** A criterion is `blocking` when its failure is non-substitutable for the decision
"may this process be relied on as it stands". Five of the ten core criteria are blocking; the
module distribution runs from four gates (agentic loop) to none (manual workflow, SOP checklist).

**Why a test rather than a list.** So the labels can be argued with rather than merely disagreed
with. No validated universal severity formula was located, and no numeric threshold separates a
systemic cause from a local one.

**What it is not.** Not a severity scale, and not a claim that the gated failures are the *worst*
ones — only that they are the ones nothing else compensates for. Note also what the gate
architecture does not buy: it is harder to game through compensating excellence, but it is not
manipulation-proof; it redirects optimisation toward passing the nearest gate. The counter to that
is wording, not architecture — each criterion states the substantive condition that must hold, and
the evidence must demonstrate the condition rather than satisfy a surface signal.

**What would settle it.** Whether a labelled-blocking criterion ever fails without the practitioner
agreeing the process should not be relied on. Disagreements there are the signal to relabel.

---

## 8 · The register core

**The convention.** Eight mandatory per-finding fields, two relocated, two added — the table in
[register.md](register.md).

**Why this set.** Two source templates were available, totalling roughly two dozen fields between
them, and **both disown their own template**: one says its design is evidence-informed rather than
directly validated, the other that nothing in the reviewed research establishes its exact template
as optimal. Against that sit better-evidenced burden findings, including a measured result that
establishing and maintaining trace links is the principal cost of this kind of bookkeeping. Adopting
both templates whole would pay that cost on every finding for two acknowledged syntheses.

**What it is not.** Not a schema and not a validated minimum. It is a starting list that survived a
field-by-field check.

**What would settle it.** Local burden measurement: which promoted fields are ever actually read
back, and how long the register takes to maintain per finding.

---

## 9 · Where the provisional marker lives

**The convention.** `instrument status` is a field on the **run**, valued `provisional on this
object class` or `in use on this object class`, printed in the report header.

**When `in use` becomes available.** Only after a completed blinded re-rate of this instrument on
cases of that object class — the process type — run to the protocol in
[limitations.md](limitations.md) and recorded; never on the number of runs already done. The
condition acts in `SKILL.md` Step 0.

**Why that condition.** It is the claim ladder in [limitations.md](limitations.md) applied to the
marker: `in use` says no more than "repeatable for this assessor" on that type, and the evidence for
that rung is the re-rate. A count of runs is not on the ladder — a run that is not re-rated produces
no evidence about the instrument, however many there are. `in use` is not a validity claim, not
evidence of transfer to another type, and not inter-rater reliability.

**Why the run and not the finding.** It is confidence in the *instrument* on this object class, not
freshness of the *evidence* behind a claim. Those are different quantities. Storing it as a
currency value would be the collapse the five-way separation forbids, and storing it per finding
would duplicate one value across every row in the run — with the same disagreement risk that
excluded a sixth acquisition mode.

**What would settle it.** Nothing empirical; this is a placement choice. It changes if the instrument
ever becomes provisional for reasons that vary *within* a run, which the transfer rule does not
currently allow.

---

## 10 · Splitting this skill across files

**The convention.** One entry file plus six reference files, all one level deep, split along the
core-and-modules seam.

**Why split at all.** The entry file has to stay short enough to be read in full every time it
triggers, and the module a given run needs is one of six. The seams are not arbitrary: the
core-plus-module architecture supplies them.

**What the real risk is, and it is not cost.** Whether context reduction produces a measured
resource benefit is not established, and that is not why this split exists. The risk a split carries
is **silence**: a single file always loads, while a retrieval split can quietly fail to deliver the
required material at the point of need. Multi-agent practice reports exactly this failure —
decomposition makes supplying each part with appropriate context harder, and a handoff that does not
propagate context fails without an error.

**The named observable that settles it.** Whether the assessment actually had the material it
needed: before Step 3, the core criteria, each declared type's module and `register.md` are either
in front of the assessor or they are not. If any is not, the run stops rather than proceeding on
memory. That is locally observable in a way the resource benefit is not. `register.md` belongs in
the check because `SKILL.md`'s own file table marks it "Step 3 — always": a check that omits it
passes a run that will then work from memory of the register contract.

**Still open.** Flat progressive disclosure against task-dependent retrieval remains an unresolved
conflict in the source material. This is a declared convention with a stated observable, not a
resolution of it.

---

## The calibration record

Kept from the first run, per run and by process type. It is a **per-run** record, separate from the
per-finding register.

| Field | Why |
|---|---|
| Production effort | The work the process itself took |
| Assessment effort | The work the audit took, **including the time spent producing evidence for it** |
| Assessment-triggered rework | Kept in its own bucket, not folded into either of the above |
| Coverage achieved | Which criteria were assessed, on what evidence |
| Serious findings | Count and identity |
| Marginal findings per successive block of effort | The only input to the stopping question |

Three separate effort buckets, never one. The published overhead figures — roughly six developer
hours a week on code review, verification and validation at 20–50% of software development cost,
manual inspection at 32–50% of one manufacturing process's time — use incompatible denominators and
are not observations of a single "QA overhead" variable. The accounting separation transfers; the
ratios do not.

**Reactivity magnitudes do not transfer either.** The folklore claim that observation improves
performance is not supported as a general law, and the one measured range available (4.2% to 65.3%
in hand-hygiene research) is from a domain unusually observable and norm-laden. Its midpoint
transfers nowhere. The two rules that act on this — prefer evidence produced before the assessment,
and record an observed run without correcting it — sit where the evidence method is chosen:
[mechanisms.md](mechanisms.md) M01, step 3 of "Ordering the work" and the
`observation or execution trace` row.
