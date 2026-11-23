# The three mechanisms

## Contents

- M01 · Planning the evidence work, and stopping
  - Ordering the work
  - Evidence methods and what each can carry
  - The evidence request
  - Stopping
- M02 · Checking the chain
  - The five properties
  - Deriving an invariant instead of inventing one
  - The minimal record
  - Three things that look like findings and are not
- M03 · Reusing an earlier conclusion
  - Currency
  - Which change invalidates which conclusion
  - Monitoring blind spots
  - The calendar backstop
  - When something surfaces after the audit closed
  - Auditing the reuse mechanism itself

**None of these is a document package every process must produce.** M01 runs on every audit because
every audit chooses what to look at. M02 runs where the process has handoffs. M03 runs where a prior
finding is being carried forward. A small process can satisfy all three with a filled-in walkthrough
and two short tables.

Build order, if you are implementing this rather than running it: the findings register first, then
M02, then M01, then M03. M02 detects substantive faults, M01 makes the audit usable, M03 pays off
only on repeat use.

---

# M01 · Planning the evidence work, and stopping

Assessment **depth** — how hard you look at one thing — is separate from assessment **coverage** —
how many things you look at. Both are chosen against the consequence of being wrong, not against a
target number of checks. Stopping because enough boxes are ticked hides the choice entirely.

## Ordering the work

1. **Inventory.** List the in-scope components and set provisional applicability per criterion.
   Unknown applicability is not exclusion.
2. **Consequence and contradiction first.** Take the decisions with the largest consequences, and
   the places where evidence already conflicts. A missing risk description is not evidence of low
   risk.
3. **Existing artifacts before new ones.** Look for what already exists before asking anyone to
   produce anything. The burden of producing evidence is part of the audit's cost and counts as
   much as its correctness. The second reason is reactivity — the effect an assessment can have on
   the process it looks at: a log or trace produced *before* the assessment cannot have been shaped
   by it, and a run staged for it may have been. Where a comparison is possible, prefer
   pre-existing logs and traces over a run staged for the assessment.
4. **Cheapest sufficient check.** Within comparable urgency, choose the least burdensome check that
   can actually settle the open question. "Cheapest" is not "cheapest available" — it is cheapest
   among those that can carry the claim.
5. **Requests carry their purpose.** Ask for evidence only with the open question and the judgement
   that could change written on the request.
6. **One reasoned check outside the high-risk set.** Choose it and record the choice *before*
   running it. This is a coverage floor, not a percentage: no fixed quota of 10%, 20% or any other
   figure is evidenced, and this must not be presented as a statistically representative sample.

Step 6 exists because of a measured tendency the source material records: assessors underweight
external disconfirming evidence when their internal evidence has consistently suggested low risk.
The sentinel is the cheapest available correction for that.

## Evidence methods and what each can carry

Match the method to what the claim needs, and state the limit rather than letting the method imply
more than it shows.

The five rows are the five acquisition modes of the closed list in [register.md](register.md)
§"Acquisition mode — the closed list", under the same names and in the same alphabetical order. The
mode a finding records is the row whose limit its `claim ceiling` is written within. The order is
not a ranking.

| Acquisition mode — the method | Can carry | Cannot carry |
|---|---|---|
| `document or artifact` — examining documents, code, configuration | A claim the artifact itself demonstrates. Static code can show a missing branch | Behaviour that was never run. It cannot show untested performance or an untested environment. And an artifact can evidence only what it was ever able to contain: sampling recorded items cannot reveal items missing from the records |
| `independent reperformance` — running it yourself | What the process does under the conditions you reproduced | That your reproduction matched production conditions, unless you evidenced that separately |
| `instrumented measurement` — an automated oracle | Highly repeatable evidence about whatever the oracle actually tests | That the oracle tests the right proposition. Automation raises repeatability, not validity |
| `observation or execution trace` — watching a run, or reading its trace | What happened in the observed instances and conditions | What happens in unobserved ones. Where the run was watched, or staged for the assessment, record that the process was observed; do not "correct" the result with a generic reactivity percentage |
| `subject claim` — asking a person | What a person can attest to about intent, history or practice | That a control actually works. A statement alone is not evidence of a working control |

Two rules that follow, and both are load-bearing:

- **Sufficiency and appropriateness are different.** A large amount of weak evidence does not
  substitute for evidence of the right kind. No numeric threshold for "enough" exists.
- **Contradictory evidence is worked in, not filtered out.** Where evidence conflicts, both sides
  go in the finding and the conflict is stated as a conflict. An extractor or a summary that
  silently selects one, averages them, or collapses them is producing the failure this rule exists
  to catch, and no benchmark exists for how often that happens.

## The evidence request

A request carries six things, so the person receiving it can see why the work is needed:

`claim id` · the missing evidence · where you expect it to be · why it is needed · the investigation
method permitted · **what happens to the conclusion if it does not arrive**.

That last field is what turns a request into a decision. It also pre-writes the evidence reason,
because issuing a request is what separates the two acquisition reasons. If the evidence was
requested and does not arrive, and no alternative procedure was performed and recorded, the reason
is `selected, not obtained`. If it arrives and does not settle the question, the reason is
`obtained, insufficient`. A criterion for which no request was issued and nothing was examined is
`never sought`, however fully it was planned. The full order of the four reasons is in `SKILL.md`
Step 3, not in step 3 of the ordering above.

## Stopping

Stop deepening a claim once its decision rule is sufficiently assessed within the declared depth,
or once usable evidence is inaccessible. Stop the run at a pre-set time or resource budget.

Three stop types, and only the first can support a *completed* judgement about the thing it stopped
on:

| Stop | Meaning |
|---|---|
| **Evidential** | The available evidence can settle the question, or demonstrably cannot |
| **Decisive** | A blocking finding settles the decision this audit exists to make |
| **Administrative** | Time, budget or attention ran out |

The stop type does not choose the evidence reason for what it leaves open; whether an evidence
request was issued does — see "The evidence request" above.

- Budget exhaustion never converts `not established` into `meets` or `not applicable`.
- Distinguish `completed for declared scope` from `partial`. The first means only that the planned
  assessment was carried out — not that the process is sound, and not that a known serious fault
  stopped mattering.
- Stopping at a blocking finding licenses **nothing** about the remainder. "I stopped because I
  found a blocker" and "the rest is fine" are different statements.
- "No new problems in the last stretch" does **not** establish completeness. No saturation rule is
  validated. If you use one anyway, label it an administrative stop.

---

# M02 · Checking the chain

Every step can satisfy its own local rule while the end-to-end result is wrong. That is not a
hypothetical: local correctness is not evidence of end-to-end correctness whenever the requirement
spans several steps, and the same result appears independently in systems architecture, clinical
handoffs and privacy accounting — three mechanisms that agree precisely because they are unrelated.

Run M02 where the process has handoffs between steps.

## The five properties

These are the properties worth checking at a boundary. They are **examples of what to look for, not
five mandatory checks**, and they are not interchangeable with each other: a count reconciliation
cannot establish that meaning was preserved, and a semantic comparison does not establish that
every record arrived.

| Property | When it applies | A testable invariant |
|---|---|---|
| **Meaning preserved** | A value or status is passed on | Producing and consuming steps use the same unit and the same meaning of a status, or there is an explicit conversion |
| **Completeness accounted for** | A set of items is processed | Every input identifier has a traceable outcome or a stated exclusion |
| **Uncertainty preserved** | Uncertain information feeds a later decision | Unknown is not presented as confirmed without new evidence |
| **Identity and authorization continuous** | Something proposed is executed later, or a step acts on behalf of whoever asked for it — a person, an account or an earlier step | The executed target and payload match the applicable authorization record — and a negative test shows the handoff cannot silently broaden authority: the subject the authority was granted for against the actor now executing, and the audience, scope and expiry it executes under against what was authorized |
| **Total budget respected** | Local steps have limits or recovery behaviour | Composed execution stays inside the declared total time or effect budget |

Summarising, filtering and aggregating may legitimately remove information where that fits the
purpose and is stated. Accounted completeness is therefore not the same as identical counts
everywhere.

**The receiving side.** All five ask whether content survives a boundary, and each can be answered
from the producing step alone. A handoff is not evidenced by a correct payload leaving the
producer: at each boundary you check, ask also whether the consuming step took the payload up. A
valid payload that the consumer never processed satisfies every property above and still breaks
the chain, and the fault then sits on the consuming side of the handoff, not in the payload.

## Deriving an invariant instead of inventing one

Derive invariants from acceptance requirements, explicit agreements, or observable consequences.
Requirement-bearing words are the cheapest source:

| Wording in the requirement | The check it implies |
|---|---|
| "all", "every" | completeness |
| "unless", "except", "may", "not" | qualifier preservation |
| "on behalf of" | actor and delegation continuity |
| "at most", "within" | cumulative budget |

**Where a requirement is not stated, mark the proposed invariant a hypothesis and say so. Never
reject a process on a self-invented domain rule.** Deriving an invariant after seeing the output is
how an audit manufactures findings.

## The minimal record

One table is enough: `invariant id` · requirement and its source · producer · consumer · permitted
transformation · possible violation · evidence · verdict.

Then assess one complete path with suitable test data or historical artifacts. Include a fault that
stays locally valid — a number carried across a boundary under a misread unit is the standard
example. Make visible which of three the finding is: an unclear contract, a demonstrable
transformation fault, or missing evidence. Those need different remedies.

**Record a chain fault once as a root finding and link the affected criteria to it.** Splitting is
for genuinely different deficiencies with separate effects and separate remedies.

## Three things that look like findings and are not

- **An explicit, correct conversion is not a violation.** Two steps using different units with a
  stated conversion between them is the meaning-preservation invariant being satisfied, not broken.
  The difference alone is not a finding.
- **A budget cannot be exceeded if none was declared.** A chain-budget finding needs arithmetic or
  observed evidence of the total overrun. Nested retries on their own are not a fault, and
  inventing the total budget you then find exceeded is the self-invented domain rule again.
- **"Insufficient documentation" is not a localisation.** Where a concrete fault is visible in the
  available output, reporting only that documentation is lacking does not identify it. And a
  chain test that was not run stays a design check or an open verification question — never a
  behavioural finding.

One more limit, because the arithmetic is tempting: **multiplying per-step accuracies is not a
valid estimate of chain success.** Real chains have correlated errors, recoveries, masking, retries,
and errors that are harmless for the final decision.

---

# M03 · Reusing an earlier conclusion

A stored conclusion has no defensible universal shelf life. It remains usable while the parts of
the object, environment, assumptions, evidence and external dependencies it relied on stay within
the conditions actually assessed.

The distinction that does the work, and it is easy to lose:

> A relevant change usually establishes that **the old evidence no longer justifies reusing the
> conclusion** — not that the conclusion has become false. "Something changed" is not evidence that
> the old conclusion is wrong, and "nothing in the main artifact changed" is not evidence that it
> still holds.

**Keep the historical judgement intact.** Reuse is expressed by a separate currency field, never by
editing or deleting what was concluded before.

## Currency

Six values. The historical outcome does not change when currency changes; a reason accompanies
every change of currency.

| Value | Meaning |
|---|---|
| `current` | Re-assessed within the current scope |
| `reuse-supported` | Older evidence, with a current and explicit reason for reusing it |
| `stale` | A relevant change has undermined the earlier support |
| `unverified` | Whether it currently applies cannot be established |
| `superseded` | A later conclusion replaces it; the link between the two is retained |
| `revoked` | Withdrawn, with the ground recorded; the record is retained |

An old `meets` marked `stale` is **not** a current positive conclusion. It is equally **not** an
automatic `does not meet` — the process may well still satisfy the criterion, but that has to be
re-established.

`stale` and `unverified` are deliberately separate: a detected relevant change and an
undeterminable applicability are different situations calling for different next actions. This
six-value set is a declared convention — see [conventions.md](conventions.md).

## Which change invalidates which conclusion

The operative question, applied per stored conclusion: **can the changed fact reach a premise,
dependency, scope boundary, control, evidence item, operating condition or causal path that this
particular conclusion depended on?**

| Change | Rule |
|---|---|
| Relevant code, prompt, procedure or contract changed | Mark directly dependent claims, and claims resting on their result, for re-assessment |
| Permissions, tool version, model version, external data or intended use changed | Re-assess claims resting on that context — **even where the files are identical** |
| The people who execute the process changed — their role, competence assumption, handoffs, workload or authority, where material | Mark claims resting on how the work is actually done for re-assessment — **even where the written procedure is identical**. This is the people doing the work, not the assessor |
| The criterion, the evaluator or the reference outcome changed | Re-relate the affected judgements to the rule version. A change of assessor is not a process improvement |
| A new incident contradicts a conclusion | Reopen the claim and retain the counter-evidence |
| A dependency is missing, or the extent of a change is unknown | Choose broader re-assessment. There is no automatic exemption |
| Only presentation changed, outside the instructions and evidence used | Reuse is possible with a concrete argument for irrelevance. "Cosmetic" is not an automatic exemption |

Record per reusable finding: what it depends on, its assumptions, the relevant environment, the
criterion version, and the assessment method. A short table is enough; a dependency graph is not
required, and dependency bookkeeping should be budgeted — maintaining trace links is the principal
cost of doing this at all. Keep no access keys or sensitive configuration values in it.

For a model-mediated process, an identical model name evidences neither a fixed backend nor
identical behaviour. Where that environment is not verifiable, limit reuse to historical results
and to design claims that can still genuinely be inspected.

## Monitoring blind spots

A manually checkable dependency table is the right starting point, and it is enough for scripts,
procedures and manual workflows.

It is **not** enough for a data pipeline or a model-mediated process, where the relationship
between input and outcome can change with no edit to any stored artifact. For those, either monitor
the inputs and operational invariants the assessment depended on, or — where no monitoring exists —
**record the blind spot explicitly**: for example, "current status assumes upstream API behaviour is
unchanged; no automated detector exists."

The governing condition, and the reason blind spots must be written down:

> A conclusion is current only when there is positive reason to believe the evidence-to-conclusion
> relationship still applies. Absence of a detected change is sufficient only to the extent that
> the mechanism for detecting relevant change is itself adequate.

Note also what a detection does **not** establish: "drift detected" is not "the conclusion is now
false". Separate change detection from impact judgement — a detected change creates a review task,
it does not flip `meets` to `does not meet`.

## The calendar backstop

Change-triggered re-assessment is primary. A calendar date exists only to catch changes the
detection mechanism may have missed.

**The backstop is 12 months. It is a review backstop chosen for burden reasons, not a validated
lifetime.** Write it that way in any report: "12-month review backstop, chosen for burden reasons"
— never "conclusion valid for 12 months". Its full basis, and what would replace it, are in
[conventions.md](conventions.md).

## When something surfaces after the audit closed

There is no general continuing duty to keep investigating after a report is issued. There **is** a
duty once potentially relevant new information reaches you:

`trigger` → `triage its reliability and materiality` → `reopen` → `investigate` →
`revised conclusion` → `supersede or revoke the prior conclusion` → `identify who relies on it` →
`notify where required` → `retain the link between old and new records`.

**Never delete the superseded conclusion.** Its existence is what makes the revision auditable.

Set this protocol up before you need it; deciding how to reopen while reopening is how the old
record gets quietly overwritten. Note that no cross-scheme data exists on how often reopening
actually happens — the mechanism is specified, not shown to be frequently exercised.

## Auditing the reuse mechanism itself

Periodically re-run a sample of conclusions marked `reuse-supported` and compare.

**The disagreement rate is the most direct local evidence you can get about whether the dependency
tracking is missing important causes of invalidation.** It is also what turns the declared 12-month
backstop from an arbitrary number into a measured one, which is the only route by which either
declared convention in this skill stops being a convention.
