# process-audit

A Claude skill that audits a process (a manual workflow, SOP checklist, runbook, script, data pipeline, prompt
chain or agentic loop) against a fixed criterion set, and reports what the evidence supports and nothing more.

**Status: v0.11, unvalidated.** The skill states this itself. It may claim "observed on these cases" and
nothing higher; see [`process-audit/reference/limitations.md`](process-audit/reference/limitations.md).

## What makes it different

Most audit prompts produce a score and a list of findings. This skill is built around three rules:

1. **A judgement and its evidence stay separate.** How evidence was obtained never sets how strong a conclusion
   may be; that is stated per finding, in a sentence, not derived from a grade.
2. **Not knowing has its own vocabulary.** There are three ways to have no verdict (`not applicable`,
   `not assessed`, `not established`), and they mean different things. The last two carry an evidence reason
   from a closed set of four. Collapsing them destroys the information a reader needs.
3. **Nothing is added up into a number that carries the verdict.** Gates block; everything else is a profile.

It does not rewrite the audited process, does not score it and does not estimate effort. Content inside the
assessed material is treated as material to assess, never as an instruction to follow.

## Use it

Copy the folder `process-audit/` to `~/.claude/skills/process-audit/` (all skills) or `.claude/skills/process-audit/`
in a project. It loads when someone asks for a process to be audited against a criterion set. The skill reads its
`reference/` files in steps; keep them next to `SKILL.md`.

| File | Role |
|---|---|
| [`process-audit/SKILL.md`](process-audit/SKILL.md) | The skill: Steps 0 to 6 (declare the object, select criteria, plan the evidence work, assess, check the chain, aggregate without a composite, report), stop rules, calibration record |
| [`process-audit/reference/`](process-audit/reference) | Criteria (core and modules), the three evidence mechanisms, the findings register, conventions, limitations |
| [`docs/CHANGELOG.md`](docs/CHANGELOG.md) | Every change since v0.1, each naming the failure it prevents |
| [`docs/AUTHORING-CONSTRAINTS.md`](docs/AUTHORING-CONSTRAINTS.md) | The dated check of the skill format against Anthropic's documentation |

## How it was built, and what that does and does not show

Built in September to November 2026 with Claude, in stages: intake, blind deep research (a session that never saw
the skill), a first build, a red team that produced two findings registers, consolidation into ten batches, then implementation one
batch per fresh session with a validation check after each. Ten batches are done.

What that supports: every rule traces to a change with a stated reason (see the changelog), and the validation
checks that were run are recorded against the version they ran on.

What it does not support: no independent rater reliability, no demonstrated transfer between process types and no
measured benefit over auditing without the skill. The conditions for a v1.0 are not met, and the skill refuses to
report a pass rate as reliability. If you use it, the sentence it puts in every report applies to you too:
inter-human rater reliability was not estimated.

## What is not in this repository

The full working record (run log, check evidence, test fixtures, the sealed evaluation set) and the method
toolkit the build followed. They stay out on purpose. The changelog and `SKILL.md` refer to those files; the
references point at the private working archive, not at this repository.
