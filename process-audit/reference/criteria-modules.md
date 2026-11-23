# Modules, one per process type

## Contents

- How a module is used
- Module H · Manual workflow
- Module C · SOP checklist
- Module S · Script
- Module D · Data pipeline
- Module P · Prompt chain
- Module A · Agentic loop
- Why the gates are distributed unevenly
- Where coverage is thin, per type

## How a module is used

Take the module for the process type declared in Step 0, and only that one. A hybrid process takes
the module of each declared type and is reported against each separately — its profile, its
denominators and its criterion list — while its overall position is one, set across all declared
types (`SKILL.md` Step 5).

**Two hard constraints, from the transfer decision:**

- **Module results are never added to the core.** That composite has not been validated.
- **No total crosses a type boundary.** Cross-type comparison would need at least a demonstrated
  configural equivalence, and no measurement-invariance literature was located for one
  instrument spanning these six structural kinds.

The consequence is deliberate: the same wording can represent a different construct in a different
type. "The operator follows the prescribed step order" is procedural compliance in a manual
workflow, deterministic sequencing in a script, orchestration correctness in a pipeline, and
possibly the wrong construct entirely in a deliberately adaptive agent. Identical wording would not
demonstrate construct equivalence, so the modules do not try to share wording where the construct
differs.

**A new object class is a new use.** The first assessments of a type this instrument has not met
carry the run-level marker `provisional on this object class`, and keep it until the condition in
`SKILL.md` Step 0 holds. That marker is not a currency value and does not live on a finding.

Entry fields are the same as in [criteria-core.md](criteria-core.md), and the blocking test is the
same one.

---

## Module H · Manual workflow

Three criteria. The core carries the gates for this type; what is distinctive here is drift between
what is written and what is done.

### H1 · Recorded execution matches the recorded step

**Condition.** For a sample of completed runs, an artifact independent of the completion mark shows
that the step was actually performed.

**Observable — this is a declared proxy.** The underlying question, whether following the procedure
changes what people do, is not binary and is not answerable from one process. The proxy is:
per sampled run, does an artifact other than the tick or signature show the step happened?

**Applies when.** Completion is recorded by a mark, a signature or a report rather than by the work
product itself.

**Label.** `non-blocking`.

**Basis.** Carried from CL-089 (checklist implementation fidelity). The source is explicit that
universal effectiveness must not be inferred from adoption, and that execution, baseline quality
and other concurrent changes have to be examined separately — which is why this is stated as a
proxy on execution and not as a claim about effect. The proxy is local operationalisation.

### H2 · Recovery has been tried, not only written

**Condition.** Recovery identifies the saved state and the steps required, and a trial shows the
recovery state was actually reached.

**Observable.** A recovery procedure plus a record of a completed trial: when, from what state, to
what state.

**Applies when.** The process has a declared recovery, rollback or restart path.

**Label.** `non-blocking`.

**Basis.** Carried from CL-113 (recovery and restore trial), decision rule "pass if recovery
identifies the saved state and required steps; fail if only a recovery promise exists". The source
states explicitly that tested recovery is needed for human execution too. A completed trial
evidences the tested state and environment only; it establishes nothing about untested ones.

### H3 · A changed procedure is checked before it becomes live

**Condition.** A change to the procedure is connected to relevant re-check results before it
becomes the live version, or to a recorded reasoned exception.

**Observable.** A change record paired with a re-check result, a dated review, or the written
exception.

**Applies when.** The procedure has been changed at least once, and a prior version exists.

**Label.** `non-blocking`.

**Basis.** Carried from CL-018 (regression review before release), decision rule "pass if relevant
regression results precede release or a reasoned exception is recorded; fail if changes bypass
both". Translating "release" to "becomes the live procedure" is local operationalisation.

---

## Module C · SOP checklist

Three criteria. A checklist differs from a manual workflow in that the steps were fixed in writing
beforehand, which is what makes ticking-without-doing and unstable grading its characteristic
failures.

### C1 · Recorded execution matches the recorded step

As H1, identically stated and identically a declared proxy. Carried from CL-089.

**Label.** `non-blocking`.

### C2 · Rating levels carry content-specific anchors

**Condition.** Where the checklist grades rather than confirms, each level carries a
content-specific descriptor and at least one worked example.

**Observable — this is a declared proxy.** Whether the anchors make a judgement's meaning clear is
an integrated judgement. The proxy is presence: per level, a descriptor specific to this content
and one example.

**Applies when.** The checklist produces a graded judgement rather than a confirmation. A purely
confirmatory checklist is `not applicable`, and the reason names that.

**Label.** `non-blocking`.

**Basis.** Carried from CL-087 (analytic rubric anchors). The source names content-specific
descriptors, examples and training as the observable signal and records no standalone decision
rule; the presence proxy and the "one worked example" bound are therefore local operationalisation,
and should be treated as the weakest-founded criterion in this set.

### C3 · The single user's own consistency has been examined

**Condition.** The person who applies the checklist has re-rated retained cases while blind to
their earlier scores, and the disagreements are recorded.

**Observable.** A set of retained cases, a second set of judgements taken blind to the first, and
the disagreement record.

**Applies when.** One person is the sole assessor and the checklist calls for judgement rather than
observation of a fact.

**Label.** `non-blocking`.

**Basis.** Carried from CL-084 (intra-rater repeatability). Carry the source's limit with the
criterion, every time it is reported: **self-consistency is not inter-rater agreement and is not
evidence of correctness.** One assessor cannot estimate inter-rater reliability — the rater facet
is simply not observed — and a lone assessor can be perfectly self-consistent and systematically
wrong.

---

## Module S · Script

Five criteria. A script's characteristic failures are what happens on the second run and what
happens when the environment is not the one intended.

### S1 · Repeating an action does not add effects

**Condition.** Re-running the same intended mutation preserves the intended effects or is blocked;
it does not silently create extra ones.

**Observable.** An idempotency rule, a deduplication record, stable idempotency keys, or a
performed repeat trial with its resulting state.

**Applies when.** The script performs any mutation that could be retried or re-run.

**Label.** `blocking`. A silent duplicate effect is a wrong result that no strength elsewhere
offsets.

**Basis.** Carried from CL-108 (idempotent repeat-action semantics), decision rule "pass if
retryable mutations preserve intended effects or repeats are blocked; fail if duplicates can
silently create extra effects". The source is explicit that byte-identical responses are **not**
required — this is about effects, not outputs. The blocking label is local.

### S2 · Test activity cannot reach production unnoticed

**Condition.** The process cannot act on production without a gate; environments are separated in a
way that is technically enforced rather than only agreed.

**Observable.** Separate environments, an enforced freeze or gate, target configuration, and
credential scoping per environment.

**Applies when.** A production environment exists and is reachable from where the script runs.

**Label.** `blocking`. An unguarded path to production is non-substitutable exposure.

**Basis.** Carried from CL-128 (dev/prod environment separation), rule "scores if the process cannot
touch prod without a gate". The blocking label is local.

### S3 · Retries distinguish transient from final errors

**Condition.** The retry policy states which errors are eligible for repetition, and unsafe
repetition is excluded.

**Observable.** The retry policy or error-handling code, and the classification it applies.

**Applies when.** The script retries anything.

**Label.** `non-blocking`.

**Basis.** Carried from CL-109 (retry error eligibility), facet "eligible errors are explicit;
unsafe repetition fails". Attempt limits and deadlines are a separate criterion, S4 — the source
separates them and so does this module.

### S4 · Repetition is bounded

**Condition.** A maximum attempt count and a total deadline are explicit, and they connect to a
defined terminal behaviour.

**Observable.** Timeout and attempt configuration, and what the process does when the bound is hit.

**Applies when.** The script retries anything, or waits on anything.

**Label.** `non-blocking` for this type. The same cluster is `blocking` in Module A, because
unbounded repetition in an agentic loop is a runaway rather than a stall. The consequence of
uncertainty is a property of the type, not of the wording — which is one concrete reason totals
must not cross type boundaries.

**Basis.** Carried from CL-158 (retry attempt and deadline bounds), facet "attempt limits and a
total deadline are explicit; fail if repetition is unbounded". The per-type label split is local.

### S5 · Progress survives an interruption

**Condition.** Saved progress supports consistent resumption from a checkpoint after interruption.

**Observable.** A state store, checkpoint records, or the resumption path in the code.

**Applies when.** The script's run is long enough, or its work costly enough, that resumption is
meaningful. Record the ground before marking `not applicable`.

**Label.** `non-blocking`.

**Basis.** Carried from CL-112 (checkpoint restartability). The source records a decision rule for
resumption and separately requires a **performed** recovery trial as its own evidence — inspecting
the failure path is not the trial. Where the trial matters, use H2's condition.

---

## Module D · Data pipeline

Five criteria. What distinguishes a pipeline is that the object flowing through can change
properties with no change to the program, so its characteristic failures are at the boundary and in
what came from where.

### D1 · Structurally invalid data is stopped at the boundary

**Condition.** Required structure is checked at the processing boundary, and invalid data cannot
silently proceed.

**Observable.** A declared schema and a validator, rejection or quarantine behaviour, and evidence
that a violation was actually rejected.

**Applies when.** Always, for this type.

**Label.** `blocking`. Invalid data proceeding silently corrupts everything downstream of it.

**Basis.** Carried from CL-010 (boundary schema validation), decision rule "pass if required
structure is checked and invalid data cannot silently proceed; **fail if parsing success is treated
as complete validation**". That second clause is the one most often missed. The blocking label is
local.

### D2 · Exchange has a stated contract

**Condition.** Data exchange has stated agreements on structure and, where described, on meaning,
version compatibility and responsibility.

**Observable.** A data contract, schema, API specification, or interface agreement — with its
version.

**Applies when.** Data crosses a boundary between a producer and a consumer.

**Label.** `non-blocking`. Structure enforcement is D1's gate; the contract is what makes a
violation diagnosable rather than what prevents it.

**Basis.** Carried from CL-009 (schema and semantic data contracts). The source carries the contract
principle from an open standard and is explicit that this is a normative basis and not a measured
outcome gain; the semantic and responsibility additions are its own operationalisation. The
non-blocking label is local.

### D3 · Repeating a run does not add effects

As S1, identically stated. Carried from CL-108. **Label.** `blocking`.

For a pipeline the observable is usually the resulting dataset state after a deliberate re-run,
rather than a key in the code.

### D4 · Each run records what it read and what it produced

**Condition.** Run metadata connects the data used and produced to a run, a version and its
upstream origin.

**Observable.** Dataset in/out metadata emitted per run, and whether the upstream is traceable from
it.

**Applies when.** Always, for this type.

**Label.** `non-blocking`.

**Basis.** Carried from CL-240 (dataset lineage and provenance), rule "scores if each run records
inputs, outputs and version". One limit travels with it, and it is local — `reasoned`, not
carried from CL-240: **lineage tells you where an output came from; it does not establish that the
transformation was correct.** Provenance is not a correctness oracle.

### D5 · Recovery has been tried, not only written

As H2, identically stated. Carried from CL-113. **Label.** `non-blocking`.

For a pipeline this includes historical reprocessing where the pipeline claims one. Note that the
source records reprocessing capability as thinly grounded, so a claim about it needs its own local
evidence.

---

## Module P · Prompt chain

Four criteria. The steps are fixed beforehand; the content of each is produced by a model, so the
characteristic failures are at the parse boundary, in format assumptions, and in what the received
content is allowed to do.

### P1 · Structurally invalid output is stopped at the boundary

As D1, identically stated. Carried from CL-010. **Label.** `blocking`.

**Applies when.** A step's output is parsed as structured data by a later step. Where every handoff
is free text read by a person, this is `not applicable` and the reason names that.

Read the source's second clause literally here: successful parsing is not complete validation. A
model can emit well-formed JSON with a field that means something other than the consumer assumes,
which is exactly what the chain check in [mechanisms.md](mechanisms.md) is for.

### P2 · Received content cannot grant authority

**Condition.** Content the chain receives cannot itself grant or change the authority for an
action.

**Observable.** A trust-boundary map; where the action policy is enforced; and whether that
enforcement sits outside the model's own output path.

**Applies when.** The chain can cause any effect beyond producing text for a person to read.

**Label.** `blocking`. If received content can authorise, every other control is advisory.

**Basis.** Carried from CL-125 (authority outside untrusted content), decision rule "pass if
external instructions cannot change the authority policy; fail if received content can authorize
actions". The source is explicit that a prompt instruction is not a control that can refuse an
action. The blocking label is local.

### P3 · The format choice was tested on the target component

**Condition.** Where a specific output or input format is required, that choice was tested on the
component that consumes it, using meaning-equivalent variants.

**Observable.** Equivalent input variants and their evaluation results.

**Applies when.** The chain requires a particular format at any step.

**Label.** `non-blocking`.

**Basis.** Carried from CL-080 (prompt format sensitivity), decision rule "pass if selected
formatting is tested on the target component; fail if universal superiority is asserted without
evidence". The source names "always JSON" as an example of a claim that is not defensible as a
universal criterion.

### P4 · An automated judge has been compared against an independent reference

**Condition.** Where an automated judge decides anything, its judgements have been compared with an
independent reference check, and the disagreements were resolved rather than noted.

**Observable — this is a declared proxy.** Whether a judge is *calibrated* is an integrated
judgement. The proxy is: a recorded comparison against a reference that is genuinely independent of
the judge's own prompt and examples, plus a disagreement log.

**Applies when.** An automated judge, scorer or classifier decides an outcome in the chain.

**Label.** `non-blocking`.

**Basis.** Carried from CL-082 (LLM judge calibration and bias probes), decision rule "pass if
automated judgements are compared with independent reference checks and discrepancies are resolved;
fail if unvalidated judgements are treated as truth". Two source limits travel with it, and both
should be reported when this criterion is used: preference agreement is not factual correctness,
and a consistently wrong judge is still wrong. Position swapping and avoiding self-judging are
named signals, not the whole criterion.

---

## Module A · Agentic loop

Five criteria, four of them gates. The model chooses the next step, so the characteristic failures
are about what it is able to do and whether it stops.

### A1 · Received content cannot grant authority

As P2, identically stated. Carried from CL-125. **Label.** `blocking`.

### A2 · Protected actions require authorization bound to the action

**Condition.** Pre-declared protected actions require verifiable authorization that is bound to the
target and payload actually executed.

**Observable.** The authorization rule, the linked action record, and whether the approval can be
bypassed or applies to something other than what ran.

**Applies when.** The loop can perform destructive, irreversible or otherwise pre-declared
protected actions.

**Label.** `blocking`.

**Basis.** Carried from CL-126 (action-bound human authorization), decision rule "pass if protected
actions require verifiable authorization for their target and payload; fail if approval is
bypassable or unrelated". Two limits from the source, both load-bearing: a general up-front
approval click is not by itself sufficient, and — recorded as an unresolved conflict in the source
material — **there is no established universal duty for a human to approve everything.** This
criterion is about binding, not about volume of approvals.

### A3 · Outbound communication stays inside stated boundaries

**Condition.** Destinations and transferable data are constrained, and no prohibited transfer path
remains available.

**Observable.** The egress policy, the effective network or connector restriction, and whether
agent-constructed destinations are blocked.

**Applies when.** The loop can send anything outward.

**Label.** `blocking`.

**Basis.** Carried from CL-127 (egress data boundaries), decision rule "pass if destinations and
transferable data are constrained; fail if a prohibited transfer path remains available". The
dossier grades the boundary-protection principle A, on a NIST control catalogue and OWASP community
guidance, and marks the exact pass/fail wording as an operationalisation, not the catalogue's own
text. The concrete failure to look for — allowlist bypass through trusted vendor domains — does not
rest on that basis: it comes from a single author's web publication, graded C, whose own "broadly
applied" label the dossier finds wider than its traceable basis. Treat it as a place to look, not as
part of the rule.

### A4 · The loop is bounded

**Condition.** A maximum attempt count and a total deadline are explicit and connect to a defined
terminal behaviour.

**Observable.** As S4.

**Applies when.** Always, for this type.

**Label.** `blocking` for this type — see S4 for why the same cluster is labelled differently there.

**Basis.** Carried from CL-158. The per-type label split is local operationalisation.

### A5 · No claim of complete protection by filtering

**Condition.** No design note, document or report claims more for filtering, retrieval augmentation
or fine-tuning than its recorded evidence demonstrates: every claim that they protect against
injection is bounded explicitly to the conditions that evidence tested. A claim that they fully or
generally prevent injection never meets this, whatever test evidence is recorded — an attack test,
adaptive or not, is a bounded trial.

**Observable.** The claim, where it is written, and the evidence offered for it.

**Applies when.** Always, for this type.

**Label.** `non-blocking`. This criterion checks a *claim*, not a control, so it cannot gate a
decision about the process — but an unfounded immunity claim is what makes the other four look
unnecessary.

**Basis.** Carried from CL-136 (universal filter protection), rule "assume no general filter
immunity; test actual unauthorized effects". Note what this criterion does not license in the other
direction: the absence of a demonstrated bypass in one bounded trial establishes no general
injection resistance either.

---

## Why the gates are distributed unevenly

Module A carries four gates; modules H and C carry none. That is a design claim about where
non-substitutable failures live in each type, made with the blocking test in
[criteria-core.md](criteria-core.md), and it is local operationalisation — not a measurement, and
not something the source material establishes.

It has a direct consequence worth stating in the report: because a blocking criterion can exist for
one type and not another, the overall position is conditioned on the type. A `suspended` or
`not acceptable` can originate in a criterion another type does not have. That is coherent, and it
is a further reason no position is comparable across types.

## Where coverage is thin, per type

The source dossier names its own thin spots per process type. Carry these into the report's
limitations rather than letting a full-looking module imply full coverage.

| Type | Named thin, in the source dossier |
|---|---|
| Manual workflow | Maintenance and audit value; checklist length thresholds; cross-domain validation; human sustainability is only lightly worked out. **110 of 240 clusters have no direct mapping to this type** |
| SOP checklist | Universal item caps; a mandatory checklist-plus-global-rating design; prescribed documentation forms. Health and education results are not direct validation of technical SOP audits. **110 of 240 clusters have no direct mapping** |
| Script | Effective repeatability; specific dependency pinning; log density. A one-off script yields no reliable trend or benchmark. **76 unmapped** |
| Data pipeline | Incident reduction attributed to contracts; historical reprocessing; low case counts. ML risk categories carry no worked test rules. **73 unmapped** |
| Prompt chain | Flat-context-only claims; fixed evaluation set sizes; few-shot and output format as quality guarantees; instruction delimiters treated as enforcement. **18 unmapped** |
| Agentic loop | Vendor architectures; the Rule-of-Two heuristic; tool interfaces; concrete transfer of agent failure taxonomies. No safe label on a heuristic. **12 unmapped** |

The mapping codes in that dossier measure neither quality nor established non-applicability, and
more mappings do not mean stronger evidence. The two types with the thinnest mapping — manual
workflow and SOP checklist — are also the two whose modules are smallest here, which is a
consequence of the same gap and not an independent judgement that less needs checking.
