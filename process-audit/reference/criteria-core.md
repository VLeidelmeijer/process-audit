# Core criteria

## Contents

- How to read an entry
- What makes a criterion blocking
- C01 Process boundary and handoffs
- C02 Required input stated
- C03 Missing or ambiguous input has a declared response
- C04 Completion verified in the actual result
- C05 Declared failure does not fall through to success
- C06 Terminal failure reaches someone who can act
- C07 The assessed version is reconstructable
- C08 Effective permissions are bounded
- C09 Material actions leave a record
- C10 Declared outcomes and failure classes are covered by evaluation
- Criteria deferred, with their reasons
- Where these criteria come from

These ten apply to all six process types. Some apply only conditionally; each entry says on what
condition, so that `not applicable` is a decision with a stated ground and never a way out.

## How to read an entry

| Field | What it does |
|---|---|
| **Condition** | The substantive statement, written so a reader can disagree with it |
| **Observable** | What you look at. If the entry names a *proxy*, the proxy is declared here and the criterion is stated on the proxy, not on the underlying judgement |
| **Applies when** | The applicability rule. Failing it means `not applicable`, with the property of the object that put it outside written in the reason |
| **Label** | `blocking` or `non-blocking` — the consequence of uncertainty, declared in advance |
| **Basis** | The source cluster the principle is carried from, and separately what is local operationalisation here |

A strong source label on a *principle* does not transfer to the precise pass/fail *gate* built on
it. Every entry therefore names both, and where nothing is carried the basis is the label
`reasoned`.

## What makes a criterion blocking

One test, applied to all ten: **is the failure non-substitutable for the decision "may this process
be relied on as it stands"?** Strength elsewhere cannot compensate for a non-substitutable failure,
which is what a gate expresses. Five of the ten pass that test.

The test is stated so it can be argued with. It is local operationalisation — no validated
severity formula was located in the source material, and no numeric threshold separates a systemic
cause from a local one.

---

## C01 Process boundary and handoffs

**Condition.** Each handoff in the process identifies its input, its output and the next
responsible step.

**Observable.** A process description, procedure, dependency graph or control-flow definition that
names inputs, outputs, steps and, per handoff, what receives the output.

**Applies when.** Always. A process with exactly one step has zero handoffs and satisfies this
trivially — record that, do not mark it `not applicable`.

**Label.** `blocking`. An undefined required handoff is a path on which work stops or is silently
dropped, and no downstream finding can be scoped without it.

**Basis.** Carried from cluster CL-001 (process definition and handoffs), whose own decision rule
is "pass if each handoff identifies its input, output and next responsible step; fail if a required
handoff is undefined". The source grades the underlying standard basis strongly and the concrete
handoff gate as its own operationalisation; that split is preserved here. The blocking label is
local.

---

## C02 Required input stated

**Condition.** The input the process requires, and the constraints on it, are stated rather than
left implicit.

**Observable.** A specification, input contract, prompt, form or intake rule that names the required
fields and their constraints.

**Applies when.** Always.

**Label.** `non-blocking`. An implicit constraint degrades reliability but does not by itself
disqualify the process, and the source material explicitly does not support a universal "no
implicit constraint" requirement.

**Basis.** Carried from CL-005 (input specification and instruction hygiene). The source supports
specification discipline as a principle and states that the full universal requirement of zero
implicit constraints is not supported by it. The non-blocking label follows that limit and is
local.

---

## C03 Missing or ambiguous input has a declared response

**Condition.** Where required information is absent or ambiguous, the response to its absence is
specified, and missing information cannot silently become an assumed fact.

**Observable.** An input contract, missing-data rule, clarification step or explicit rejection
path; and, on a sample of incomplete inputs actually processed, whether they were rejected,
clarified or explicitly qualified.

**Applies when.** Always.

**Label.** `blocking`. Missing information silently becoming an assumed fact is a fabrication path,
and everything downstream of it inherits a claim nothing supports.

**Basis.** Carried from CL-006 (missing input and ambiguity handling), decision rule "pass if
required information and the response to its absence are specified; fail if missing information can
silently become an assumed fact". Note the source's own caution, carried here: output consistency
across repeated runs is a usable but unreliable signal of ambiguity, and consistent output does not
rule out under-specification. The blocking label is local.

---

## C04 Completion verified in the actual result

**Condition.** Completion is checked against the produced output or the resulting state,
independently of the executor's own success message.

**Observable.** An output artifact, or a confirmation of external state, that was checked; and the
check itself — where it lives and when it ran.

**Applies when.** Always.

**Label.** `blocking`. This is the difference between "it reported success" and "it worked", and
nothing else in the set substitutes for it.

**Basis.** Carried from CL-023 (completion verified in actual state), decision rule "pass if success
is checked independently of the executor's success message; fail if the message is the sole proof".
The blocking label is local, though the source's framing makes it close to inevitable.

---

## C05 Declared failure does not fall through to success

**Condition.** Each declared failure state leads to a stop, a recovery or an escalation, and does
not fall through into a success path.

**Observable.** Error paths, a state model, an exception procedure, or the equivalent written step
in a manual procedure; plus, where a trace exists, whether a real failure took one of those routes.

**Applies when.** The process declares any failure state, or can produce one. A process with no
reachable failure state is rare — record the ground before marking `not applicable`.

**Label.** `blocking`. A failure that reads as a success is an actively wrong result, not a missing
control.

**Basis.** Carried from CL-116 (failure transitions and completion states), decision rule "pass if
each declared failure state leads to stop, recovery or escalation; fail if it falls through to
success". The blocking label is local.

---

## C06 Terminal failure reaches someone who can act

**Condition.** A terminal failure produces a visible signal that identifies the failed step and the
response required.

**Observable.** An error catalogue, a status output, a notification route, or the recorded
escalation step in a procedure; and whether a real terminal failure produced one.

**Applies when.** The process runs unattended at any point, or its failures are not immediately
visible to the person responsible.

**Label.** `non-blocking`. A swallowed failure is serious, but it does not by itself make the output
wrong — the failure it causes is delay and repeated loss, which the profile carries.

**Basis.** Carried from CL-117 (actionable failure notification), decision rule "pass if terminal
failures identify the failed step and next response; fail if failures are silently swallowed". The
non-blocking label is local and is the one most worth arguing with in this set.

---

## C07 The assessed version is reconstructable

**Condition.** The instructions, code and relevant configuration of the run being assessed can be
identified as a version.

**Observable.** Version control with diffs, a version manifest, a retained baseline, a dated
procedure revision, or a retained prompt version. For a data pipeline, a prompt chain or an agentic
loop, the version also covers the model or service identity, tool versions, the prompt and
configuration, the relevant input distribution, external state, and the evaluation protocol.
Versioned source files alone do not identify the version for these types.

**Applies when.** Always.

**Label.** `non-blocking` — but note the consequence: **where C07 does not hold, no finding about
this process may be reused later.** M03 reuse depends on being able to say what changed, and an
ambiguous baseline makes every reuse decision unfounded.

**Basis.** Carried from CL-012 (process version reconstruction), decision rule "pass if the assessed
instructions, code and relevant configuration can be identified; fail if the baseline is
ambiguous". The reuse consequence is local operationalisation and follows from mechanism M03. So is
the observable's extension for a data pipeline, a prompt chain and an agentic loop: it follows from
M03's rule that a changed model, tool version or external data calls for re-assessment even where
the files are identical.

---

## C08 Effective permissions are bounded

**Condition.** The access the process effectively holds maps to operations it actually needs.

**Observable.** A permission inventory, credential scopes, tool specifications, or the equivalent
account and access list for a human procedure — and, where obtainable, evidence of *effective*
access rather than intended access.

**Applies when.** The process holds any credential, permission or capability beyond reading its own
declared inputs. Where it holds none, this is `not applicable` and the reason names that.

**Label.** `blocking`. Unnecessary effective access is a non-substitutable exposure: no strength
elsewhere reduces what the process is able to do by mistake.

**Basis.** Carried from CL-123 (least privilege), decision rule "pass if granted access maps to a
required operation; fail if unnecessary effective access is identified". The distinction between
intended and effective access is in the source. The blocking label is local.

---

## C09 Material actions leave a record

**Condition.** A material action can be reconstructed from a record naming actor, action, target,
time and result, and that record is kept with access protection. A complete record that can be
freely altered does not meet this.

**Observable.** Logs, an audit event schema, a signed-off form, a ticket, or a change record — and
the access protection it is kept with: who can alter or delete it.

**Applies when.** The process performs actions with effects outside itself. A purely
read-and-report process is `not applicable`, and the reason names that.

**Label.** `non-blocking`. Absent records make later assessment harder rather than making this run's
result wrong; the cost lands on reuse and on incident reconstruction, which the profile carries.

**Basis.** Carried from CL-121 (protected action audit records), decision rule "pass if actor,
action, target, time and result are recorded with access protection; fail if material actions are
untraceable". The non-blocking label is local.

---

## C10 Declared outcomes and failure classes are covered by evaluation

**Condition.** Each declared outcome and each material failure class maps to an evaluation case or
to a written, reasoned exclusion.

**Observable.** A coverage matrix, a case set, a test list, or a set of worked examples — checked
against the process's own declared outcomes and its known failure classes.

**Applies when.** The process has declared outcomes, or a known failure class. A process with
neither has nothing for this criterion to cover; record that ground.

**Label.** `non-blocking`. Coverage gaps are exactly what the two denominators in the report are
for; converting them into a gate would double-count the same information.

**Basis.** Carried from CL-019 (evaluation coverage of outputs and failures), decision rule "pass if
each declared outcome and material failure class maps to a case or documented exclusion; fail if a
required class is unexamined". The non-blocking label is local.

Note the boundary this criterion does **not** cross: it asks whether classes are covered, not
whether the case set is large enough. No defensible universal sample size was located — see the
deferrals below.

---

## Criteria deferred, with their reasons

Deferral is a recorded decision, not silence. Each of these was a candidate and was left out
because forcing it into a binary statement would assert something the evidence does not carry.

| Deferred | Reason |
|---|---|
| **Maturity ladder as an improvement route** | The proposition a ladder claims — that performing the prescribed actions of a level causes movement to the next — is the one proposition the source material finds unsupported. A criterion built on it would assert what the evidence denies. Correct level *naming* and the correlation of higher scores with better outcomes are different propositions and are not what a ladder criterion would test |
| **Multidimensional productivity framing** | A classification frame rather than a checkable property of the audited process; and any productivity claim needs measurement denominators the source material leaves unresolved |
| **Improvement-cycle discipline** (DMAIC, PDCA) | The *presence* of an improvement programme is observable, but the value claim attached to it is not, and organisational-change instruments are out of scope by declaration |
| **Evaluation sample-size adequacy** | No evidence-based universal item or case count was located, and a defensible local number requires a stated inference target the audit does not have. Practitioner heuristics of 30, 60 or 100 cases are operational advice, not constants |
| **Efficiency criteria** (cycle time, rework, cost per accepted case) | Measurement definitions exist in the source material, but their denominators are recorded there as an unresolved conflict. An efficiency criterion without a fixed denominator produces a number that cannot be compared to itself. Efficiency observations may still be recorded as unverified judgements |

**A criterion that resists a binary statement is never forced.** Where a condition is genuinely an
integrated judgement, this skill either states it on a named observable proxy — with the proxy
written into the entry, as in C10's coverage-versus-adequacy boundary — or defers it here with the
reason. If a later enumeration produces a substantial block of genuinely integrated-judgement
criteria, that is a signal to reopen the no-ordinals decision rather than to proxy-state everything.

## Where these criteria come from

The ten are selected from the 43 clusters the source dossier grades as core. That grade is the
dossier's own judgement, scored on evidence strength, applicability and discriminating power; it is
not a count of agreeing reports, and in that dossier only an explicitly bounded finding of
independent convergence carries confirmation. Several core clusters rest on a single register line,
and two of them carry gates here: CL-023 under C04 and CL-116 under C05, for neither of which the
dossier establishes independent convergence. Selection was on: applicability to all six process
types; statability as a binary substantive condition on a named observable; and being a property
of the *audited process* rather than of the audit itself. Clusters that are rules for the assessor
rather than properties of the assessed object — evidence sufficiency, evidence appropriateness,
claim-specific reporting, the examine and interview evidence methods — are carried in
[mechanisms.md](mechanisms.md) and [register.md](register.md) instead, where they govern how the
audit works.

**Nothing here is validated.** The dossier grades no row `measured`, deliberately, and
"corroborated" in it means sources agree — never that anything has been replicated. See
[limitations.md](limitations.md).
