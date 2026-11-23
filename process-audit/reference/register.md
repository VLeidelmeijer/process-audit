# The findings register

## Contents

- One register, not three
- The five quantities that must never collapse into one
- The mandatory core, per finding
- The evidence fields
- Acquisition mode — the closed list
- Fields promoted by a trigger
- The per-run record
- Which fields were confirmed load-bearing, and which moved
- The reverse trace

## One register, not three

One shared findings register, with optional per-mechanism tables. Not three frameworks and not a
document package per process.

The register carries a **small mandatory core**; everything else is promoted into a finding only
when a stated trigger fires. That discipline is not tidiness. Maintaining trace links is measurably
the principal cost of doing this at all, and a register that costs more than the errors it catches
is a net loss regardless of how complete it looks.

This is a logical contract, not a prescribed file format. A table, a set of notes with headings, or
a structured file all satisfy it.

## The five quantities that must never collapse into one

These are five different things. Collapsing any of them into a single grade is the failure this
whole register exists to prevent, because the grade is what survives when a finding gets shortened,
and the qualification is what drops.

1. **Source confidence** — how much you trust the source of an evidence item.
2. **Evidence basis** — how the evidence was obtained, recorded as separate fields and never as a
   rank.
3. **Claim level** — the strongest proposition the evidence actually demonstrates.
4. **Audit outcome** — the criterion value.
5. **Currency** — how fresh the support is, and whether it still applies.

## The mandatory core, per finding

| Field | What it holds |
|---|---|
| `proposition` | The claim being made, written so it can be re-tested |
| `criterion` | Which criterion, and which version of it |
| `outcome` | `meets` / `does not meet` / `not applicable` / `not assessed` / `not established` |
| `evidence reason` | Required on `not assessed` and `not established`, never on `not applicable`: `does not exist` / `selected, not obtained` / `obtained, insufficient` / `never sought` — the first whose condition holds, in that order; the conditions are in `SKILL.md` Step 3 |
| `evidence fields` | The six below |
| `source locator` | Where the evidence is — file, line, run id, record, date of observation |
| `applicability and scope` | What this finding covers, and on what ground it is or is not applicable. A `not applicable` carries its ground here, in place of an evidence reason |
| `currency` and `reason` | One of the six currency values, and why it has that value |
| `causal issue id` | The root finding this belongs to. Severity is assigned here, once, and not chosen: the blocking label of the most consequential affected criterion — `blocking` if any affected criterion is — read off the criterion entries. No other severity value exists |
| `affected criteria` | The reverse index: which criteria this root finding explains |

`observed at` is the date of the observation — not the date on which an old document was read
again. A file hash shows identical bytes, not identical external circumstances.

**An evidence reference is not credible because the field is filled.** The content pointed at has
to carry the claim. A reference that does not is a defect in the finding, not a formality.

Where one deficiency shows under several criteria, `causal issue id` and `affected criteria` are
what let you deduplicate at the severity layer while keeping every failed criterion, every evidence
item, and the recurrence count. Merge is never implemented as deletion — duplicates carry
information about breadth and recurrence that the single merged record does not.

## The evidence fields

Six fields, and no ordinal among them. There is no validated universal scale that ranks evidence
acquisition, in any tradition that was searched for one; the acquisition mode of evidence does not
by itself determine the permissible strength of a conclusion.

| Field | What it holds |
|---|---|
| `acquisition mode` | One value from the closed list below |
| `producer or controller` | Who or what produced this evidence, and who controlled it |
| `coverage` | Which instances and conditions it covers. Repetition counts live here |
| `integrity` | How the integrity of the evidence-producing mechanism was checked |
| `claim ceiling` | One sentence in three parts: *this evidence supports* the strongest proposition it actually demonstrates, *under* the conditions it was obtained in — among them, where it applies, that the run was watched or staged for the assessment — *and does not establish* what lies beyond those conditions |
| `confidence` | The assessor's confidence — an independent field, never computed from the mode |

The `claim ceiling` does the epistemic work that a rank would pretend to do, and it does it per
finding rather than per category. A high formal assurance grade can accompany a wrong conclusion,
and an automated oracle can supply highly repeatable evidence for the wrong proposition. Only the
ceiling sentence catches either.

`coverage` is where repetition belongs. Recording repeated observations as a separate acquisition
mode would put the same fact in two places that can disagree.

## Acquisition mode — the closed list

Five values, **listed alphabetically**. The order is not a ranking and position in it licenses
nothing.

| Mode | What it covers |
|---|---|
| `document or artifact` | A document, configuration, procedure or other static artifact |
| `independent reperformance` | You re-ran the step yourself |
| `instrumented measurement` | An automated oracle or measurement produced it |
| `observation or execution trace` | Direct observation, or a trace of an execution |
| `subject claim` | A statement by the process owner — including an agent's own account of what it did |

What each mode can and cannot carry is in [mechanisms.md](mechanisms.md) M01 §"Evidence methods
and what each can carry", one row per mode under the same name. A finding's `claim ceiling` is
written within the limit of the row for the mode it records; the limits bound a claim, they do not
rank the modes.

Boundary cases that do **not** need a sixth value, because the other fields absorb them: a
third-party attestation is a `document or artifact` with a different `producer or controller`; an
agent's explanation of its own run is a `subject claim`; and repeated independent observations are
one mode with a larger `coverage`.

Adding a mode later invalidates no earlier finding, which is why this list can be closed now. That
would not be true of a scale, where changing the granularity changes what every earlier record
meant.

## Fields promoted by a trigger

Not carried by default. Each is added to a finding when its trigger fires.

| Trigger | Fields promoted |
|---|---|
| Any evidence for this finding conflicts with any other | `contrary evidence` — both sides recorded, and the conflict stated *as* a conflict. Not resolved by selecting one, averaging them, or dropping the weaker |
| The finding is being reused, or may be | `depends on`, `assumptions`, `relevant environment`, `criterion version`, `assessment method`, `revalidation trigger`, `last dependency check` |
| No detector exists for a dependency that can change silently | `monitoring blind spot` — written out, e.g. "assumes upstream API behaviour unchanged; no automated detector exists" |
| The finding came from a chain check | `invariant refs`, `producer`, `consumer`, `permitted transformation` |
| A correction is proposed that the assessor undertakes to verify | `proposed change`, `verification action`, `verification result` — three separate fields |
| The finding is condensed, summarised or carried forward into another record | `transformation history`, `downstream summary id` |
| A conclusion is replaced or withdrawn | `supersedes` / `superseded by`, `reason for status change`, `who relies on it` |

**A proposed correction does not close a finding.** Keeping `proposed change`, `verification
action` and `verification result` as three fields is what stops a suggested improvement being read
as demonstrated repair. Severity belongs to the causal issue, not to the proposed fix. A finding's
`Action` line (`SKILL.md` Step 6) is not such a correction on its own: it names one observable
change and promotes nothing.

## The per-run record

Distinct from the per-finding register, and kept separately. Merging them loses both: one is
evidence about a claim, the other is evidence about the audit.

| Field | Why |
|---|---|
| Process, version, type, declared scope | What was assessed |
| `instrument status` | `provisional on this object class` or `in use`. A run-level property, not a currency value and not a per-finding field |
| **Coverage statement** | What was examined and what was not, and **how the examined subset was chosen** — risk-targeted, by convenience, or on another basis, stated for each part — including the sentinel check outside the high-risk set ([mechanisms.md](mechanisms.md) M01 step 6): which check, and when it was chosen. Never "no issues found" unqualified — only "no issues found in the examined subset" |
| Criteria left `not assessed` | Listed, not counted |
| Stop reason and stop type | Evidential, decisive or administrative |
| `completed for declared scope` or `partial` | The first means only that the planned assessment ran |
| Overall position | `acceptable`, `not acceptable` or `suspended`, with its qualifier, its route and the ids of the blocking criteria that triggered it — `SKILL.md` Step 5 |
| The two denominators | *met, among applicable and assessed*; *positively established, among all applicable* |
| Criteria `not applicable` | Listed, not counted, beside the two denominators — so two runs over different applicable sets can be told apart |
| AI-assistance configuration, if used | Model or version, prompt, scale, settings, input context |
| Calibration record | Production effort, assessment effort, **assessment-triggered rework**, coverage achieved, serious findings, marginal findings per successive block of effort — by process type, from the first run. Three separate effort buckets, never one |

**A hybrid keeps one per-run record per declared type** (`SKILL.md` Step 1). The overall position
is the one field not kept per type: Step 5 sets it once, for the whole process, and each type's
record carries that same position.

The calibration record is the only thing that will ever convert the two declared conventions in
this skill into measured numbers. See [conventions.md](conventions.md).

## Which fields were confirmed load-bearing, and which moved

The core above was checked field by field rather than adopted as a list. Two fields moved; none was
cut. What each column says is what breaks if the field is absent.

| Candidate field | What fails without it | Verdict |
|---|---|---|
| `proposition` | The outcome is a verdict on nothing nameable, and cannot be re-tested later | core |
| `outcome` | There is no finding | core |
| evidence fields (six) | The outcome floats free of what supports it — the failure the whole evidence design exists to prevent | core |
| `currency` + reason | A carried-forward finding is indistinguishable from a fresh one, and reuse becomes unauditable | core |
| `applicability and scope` | `not applicable` has no ground, and neither denominator can be computed | core |
| `source locator` | The evidence reference cannot be checked, which is the filled-but-empty field failure | core |
| `causal issue id` | One deficiency showing under several criteria receives several severities | core |
| `affected criteria` | The root finding cannot be reached from the criteria it explains, and breadth cannot be reported as breadth | core |
| `blocking flag` | Nothing — **it is a property of the criterion, declared in advance, not of the finding.** Copying it per finding creates a second place it can be wrong, and a place where it could be set after seeing the evidence | **moved** to the criterion entry; referenced, not copied |
| open-or-unexamined statement | Nothing at finding level — **it is a coverage property of the run.** Per finding it would be either duplicated across every row or, worse, partially filled | **moved** to the per-run record |

Three additions the core did not originally carry, all required rather than optional:

- **`evidence reason`** on `not assessed` and `not established`. Without its four values the narrow
  adverse treatment in Step 5 is unimplementable, and with it unimplementable the whole arrangement
  rewards an assessor for looking less. A `not applicable` carries its ground in
  `applicability and scope` instead: a scope decision is not an evidence position, and none of the
  four describes one.
- **`criterion version`** alongside the criterion id, because a change of criterion is not a change
  of process and the two must stay distinguishable when a finding is reused.
- **`contrary evidence`**, promoted whenever evidence conflicts. Without a place to put it, the
  conflict is resolved by whoever writes the finding and disappears. No benchmark exists for
  whether an extraction or summary preserves two mutually inconsistent claims *as* two conflicting
  claims rather than selecting, averaging or silently collapsing them — so this has to be designed
  in explicitly, not assumed from care.

Neither the source templates this core was drawn from ranks its own fields, so the ranking above is
judgement. It is offered as a starting list that survived a check, not as a finding.

## The reverse trace

On a **sample of high-impact claims** — not every finding — trace backwards from the headline
statement to the raw evidence, and check that the qualifiers, exceptions and contrary evidence
survived each condensation.

This is scoped as a sample deliberately. No blanket policy of reconciling every boundary,
capturing full lineage everywhere or back-translating every summary is supported; what is supported
is risk-weighted deployment of these checks, not ritual machinery.

Treat the result as an **alarm requiring calibration, not a pass/fail certificate.** A round-trip
that comes back clean tells you less than one that does not.
