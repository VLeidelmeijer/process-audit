# Authoring constraints, established against official documentation

**Checked: 12 September 2026. Re-measured against v0.2 on 18 September 2026** — the check dossier row
IN-46 required as an open task. The documentation was not re-read on the second date; only this
skill was re-measured against what the 12 September reading established. No authoring constraint was
carried into this build from any pre-existing project document, and no tool default was accepted in
place of this check.

## Pages read

| Page | URL |
|---|---|
| Agent Skills — overview | `https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview` |
| Skill authoring best practices | `https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices` |
| Extend Claude with skills (Claude Code) | `https://code.claude.com/docs/en/skills` |

The first two redirect from `docs.claude.com`; the third from `docs.anthropic.com`. Both redirects
were followed to the destination and the destination is what was read.

## Constraints, and what this build did

| Constraint | As documented | v0.2 |
|---|---|---|
| `SKILL.md` required | Yes, with YAML frontmatter | present |
| Opening `---` | Must be the file's first line, or the whole file is treated as content | first line |
| `name` | Required. Max 64 characters; lowercase letters, numbers and hyphens only; no XML tags; must not contain the reserved words "anthropic" or "claude" | `process-audit`, 13 characters, compliant |
| `description` | Required. Non-empty, max 1,024 characters, no XML tags. Must say both what the skill does and when to use it. Third person | **1,005 characters** — 19 below the limit. v0.1 measured **901**, not the 906 this row previously recorded |
| Body size | "Keep SKILL.md body under 500 lines"; the overview's loading table gives Level 2 as "under 5k tokens" | **299 body lines**, 316 including frontmatter. v0.1 measured 293 body lines, not the 304 this row previously recorded |
| Reference files | Loaded on demand; referenced by relative markdown link from SKILL.md | 6 files, all linked from SKILL.md |
| Reference depth | "Keep references one level deep from SKILL.md" — Claude may only partially read a file reached through another referenced file | all one level deep |
| Table of contents | Required in reference files longer than 100 lines, so the scope is visible under a partial read | all 6 have one |
| Paths | Forward slashes, even on Windows | forward slashes throughout |
| Time-sensitive content | Avoid, or isolate in an "old patterns" section | the one dated item is this file |
| Packaging | Claude Code skills are filesystem-based: `~/.claude/skills/<name>/` personal, `.claude/skills/<name>/` project, `<plugin>/skills/<name>/` for a plugin. No upload step | filesystem layout |

## Two findings from the check

**1 · The two documentation sets state different `description` limits, and the tighter one governs
here.**

- The platform docs state `description` max **1,024** characters.
- The Claude Code docs state `description` **plus `when_to_use`** capped at **1,536** characters
  before truncation in skill listings.

These are different limits on different things and neither page mentions the other. This skill is
written to the 1,024-character platform limit and uses no `when_to_use` field, so it satisfies both.
Recorded because a later edit that grew the description past 1,024 characters would pass in one
surface and fail in the other.

**At v0.2 that is no longer a hypothetical.** The description is 1,005 characters — **19 below the
limit**, against 123 at v0.1. Batch 4.1 spent nearly all of the remaining budget, and it did so
buying a negative trigger the description did not have. Any later batch that wants to say something
new here has to cut something else first, and the cut has to be argued rather than assumed. Carried
to Stage 6 as an observation, not repaired here: the plan carries no change for it.

**2 · Frontmatter fields are not portable, and one obvious field would break an upload.**

The Claude Code docs list around twenty frontmatter fields (`when_to_use`, `argument-hint`,
`arguments`, `disable-model-invocation`, `user-invocable`, `allowed-tools`, `disallowed-tools`,
`model`, `effort`, `context`, `agent`, `background`, `hooks`, `paths`, `shell`, `metadata`,
`license`, `compatibility`, …) and then state that when uploading to claude.ai or the Skills API
**only six are accepted**: `name`, `description`, `license`, `compatibility`, `metadata`,
`allowed-tools`. Anything else fails the upload with an "Unexpected key(s)" error.

`version` is not among the six. The first draft of this skill carried `version: 0.1` in frontmatter;
it was changed to `metadata: {version: "0.1"}`, which is inside the portable set. Recorded as a
manual correction in the run log.

**Consequence adopted for this skill:** v0.1 restricts itself to the six portable fields, using only
`name`, `description` and `metadata`. Any future field outside that set is a deliberate choice to
make the skill Claude Code-only, and needs recording as one.

## What this check does not establish

The documentation states no measured effect for any of these limits. "Under 500 lines" and "under
5k tokens" are stated as guidance for performance, not as enforced limits, and no measurement is
offered. That matters for one open question this build did not close: whether splitting instructions
across files produces a resource benefit is **not** established, and this check does not change
that. The split in v0.1 is a declared convention with a stated observable — see
`reference/conventions.md` §10 — not a decision this documentation supports.

The documentation also recommends building evaluations before writing extensive instructions, and
testing across models. Neither was done here, deliberately: this build was not permitted to
benchmark its own draft.
