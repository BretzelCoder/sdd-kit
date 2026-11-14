# SDD kit — user guide

This guide explains how to run the kit day to day, why each rule exists, and how to adapt it. Read the README first for the overview.

## 1. Vocabulary

| Term | Meaning |
|---|---|
| **Spec** | `spec.md`: WHAT the feature does and WHY. No technical decision. |
| **Plan** | `plan.md`: HOW, traced back to the spec's requirements. |
| **Tasks** | `tasks.md`: the plan cut into steps under 1 hour, each testable. |
| **Owner** | The human who approves specs and plans and decides merges. |
| **Constitution** | `docs/constitution.md`: the few principles nothing may override. |
| **ADR** | Architecture Decision Record, in `docs/architecture-decisions.md`. |
| **Rulebook** | `CLAUDE.md` (or `AGENTS.md`): the rules the agent reads at every session. |
| **Gap** | A difference between the spec and what the code needs. Always resolved by amending the spec. |
| **Rapport d'étonnement** | French for "astonishment report": what surprised the agent during a session. Kept in French on purpose: the concept comes from French management practice. |

## 2. Setup (10 minutes)

1. Copy the kit into the root of your repository.
2. Rename `.claude/settings.example.json` to `.claude/settings.json` and adjust the allowed commands to your stack.
3. Fill in the `<placeholders>` in `CLAUDE.md`: product context, stack, project commands, checklist.
4. Read `docs/constitution.md` and replace principle 8 with one of your own. Remove any principle you do not intend to enforce.
5. Write your first ADR (your main stack choice) in `docs/architecture-decisions.md`.
6. In `.claude/commands/implement.md`, replace `<your commands here>` with your lint, typecheck and scoped test commands.

The commands are standard Claude Code slash commands: each `.md` file in `.claude/commands/` becomes `/name`, and `$ARGUMENTS` receives what you type after it.

## 3. Running one feature

| Step | You type | What you get | Your job |
|---|---|---|---|
| 0 (optional) | `/brainstorm import contacts from a CSV file` | Questions one at a time, verified current state, two or three options, then `docs/brainstorm/<slug>.md` | Choose: specify, postpone or drop |
| 1 | `/specify export my contacts to CSV` | 3 to 6 questions, then `specs/NNN-slug/spec.md` | Answer, read the spec, approve or correct it |
| 2 | `/plan` | `plan.md` with a traceability table | Check every requirement has an answer and nothing extra was added |
| 3 | `/tasks` | `tasks.md` | Check the order and the definitions of done |
| 4 | `/implement` | Tasks chained, one commit each, on branch `NNN-slug` | Step in only when it stops on a gap |
| 5 | `/review` | Verdict: COMPLIANT or GAPS, with file:line | Decide whether to fix, then ask for the pull request and merge |

See `examples/001-csv-export/` for a complete spec, plan and task list at the expected level of detail.

### Spec statuses
`DRAFT` → `IN REVIEW` → `APPROVED` → `DELIVERED` → `CLOSED`, or `ON HOLD` / `ABANDONED`. The header must always tell the truth. A useful first CI check is to fail when a spec merged into main is still `DRAFT` or `IN REVIEW`.

### When `/implement` stops on a gap
This is the process working, not failing. Read the proposed amendment, edit `spec.md` (add an "Amendment YYYY-MM-DD" note), update `plan.md` and `tasks.md` if needed, then run `/implement` again. Never let the code drift silently from the spec.

## 4. Why the rules exist

| Rule | Problem it prevents |
|---|---|
| Optional framing before the spec | Specs reworked during implementation often rest on a claim about existing behaviour written from memory. Framing makes the current state verified, with evidence, before the spec is written. |
| Questions before the spec | The agent fills ambiguity with plausible guesses. |
| No technical decision in the spec | The spec becomes a disguised plan and nobody challenges the approach. |
| Traceability table in the plan | Features grow beyond what was asked (scope creep). |
| Tasks under 1 hour, tests with the code | Large unverifiable changes; tests written afterwards to fit the code. |
| Dedicated branch per spec | Half-finished work on main; mixed changes across features. |
| Database backup (T-00) | Local data lost by a migration during development. |
| Merge only on explicit request | The agent ships something the owner has not looked at. |
| Retrospective after each session | The same mistake repeated from one spec to the next. |

## 5. Turning incidents into guardrails

The kit starts light on purpose. Your rulebook should grow from real incidents, in three steps:

1. **Fix the incident** in the current spec.
2. **Write the rule** in `CLAUDE.md`, naming the spec that triggered it: `Decided spec 012`. The reference lets anyone find why the rule exists, and remove it when it no longer applies.
3. **Automate it** whenever possible: a script, a lint rule or a test that fails in CI when the rule is broken. A rule that only lives in text depends on the agent remembering it.

Examples of rules that can be automated: forbidden patterns (`grep` against an allowlist), every database table has access control, every user-facing text goes through the translation function, spec headers are valid, documentation links point to existing files.

Prune regularly. When the rulebook gets long, review it rule by rule: merge duplicates, move details to the docs, delete what no longer applies.

## 6. The retrospective

At the end of each session that covers a spec, ask the agent for its self-critique and its rapport d'étonnement, following `docs/continuous-improvement.md`. Keep only findings with an action, an owner and a trigger. Re-read the open actions at the start of the next session. An action that changes a rule is a proposal: the owner decides.

## 7. Using it with other agents or tools

The method does not depend on Claude Code.
- **Other coding agents**: put the rulebook in `AGENTS.md` (or the file your agent reads) and turn each command into a prompt or a saved instruction.
- **GitHub Spec Kit**: it applies the same principle with more tooling (`specify init`). This kit is deliberately lighter and easier to bend to an existing repository.

## 8. Adapting it to a team

- The owner role can be split: the product owner approves the spec, the tech lead approves the plan.
- Keep one constitution per organisation and one rulebook per repository.
- Treat changes to the rulebook and commands like code: through pull requests, reviewed.
- Track a few outcome metrics: lead time from approved spec to production, share of specs amended during implementation, defects found after merge, human time spent per spec.

## 9. FAQ

**Isn't this waterfall again?** No. Waterfall freezes the spec for months. Here a spec covers one feature, takes minutes to amend, and amendments are expected: they are how gaps get resolved instead of being patched in the code.

**Is it worth it for a one-line fix?** No. Use a `fix:` commit on a short branch. The full cycle is for features and anything that changes behaviour.

**When should I use `/brainstorm`?** When the topic is still fuzzy: several possible solutions, a method or documents to analyse, a privacy or production stake. If you can already say what, for whom and what is out of scope, go straight to `/specify`.

**How long does a cycle take?** It depends on the feature. The spec and plan validations are the part that needs you; `/implement` runs on its own.

**Can I skip `/review`?** You can, but it is the step that catches code with no requirement behind it. For large diffs, the parallel mode spreads the check across read-only sub-agents.
