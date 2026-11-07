# Project: <name>

## Product context
<One paragraph: what it is, for whom.> See `docs/constitution.md` for the non-negotiable principles and `docs/architecture-decisions.md` for the ADRs.

## Stack
<Your imposed stack.>

## Spec-Driven Development workflow — STRICT RULES

1. **Never code without an approved spec.** Every feature starts with `/specify`.
2. Full cycle: `/specify` → human validation → `/plan` → human validation → `/tasks` → `/implement` (chained by default, see rule 4) → `/review`.
3. A spec lives in `specs/NNN-slug/` (spec.md, plan.md, tasks.md). NNN = sequential number. **Each spec is developed on a dedicated branch** `NNN-slug`, created from an up-to-date main. No feature code ever committed directly on main.
4. During `/implement`: chain the unchecked tasks of tasks.md (lint + typecheck + scoped tests green after each task, full suite once at the end, box ticked, then commit) without stopping between tasks. Stop only: (a) at the end of tasks.md, (b) on a gap with the spec (rule 5), (c) if the user explicitly asks for task-by-task control.
5. Any gap discovered during implementation = back to the spec (amend it), no improvisation in the code.
6. **The spec header always tells its real status** (DRAFT → IN REVIEW → APPROVED → DELIVERED → CLOSED, or ON HOLD / ABANDONED).
7. Atomic commits per task: `feat(NNN): T-XX description` (or fix/chore/test).
8. **Pull request and merge into main: always on the user's explicit request**, confirmed at the time of the action. Never on Claude's initiative, even when every task is done.
9. **Continuous improvement**: at the end of every session that covers a spec, write a self-critique and a "rapport d'étonnement" in `docs/continuous-improvement.md`, each finding with an action (owner + trigger). At the start of a session, re-read the open actions.

## Conventions
<Your conventions. The pattern that pays off: every incident becomes a dated rule here, naming the spec that triggered it ("Decided spec NNN"), and then, whenever possible, an automated check in the CI. Do not rely on the agent remembering a rule: make the pipeline fail when it is broken.>

## Project commands
- `<lint>` / `<typecheck>` / `<test>` / `<build>`

## Guardrails
- Never read or modify secret files (`.env*`).
- Never run a destructive migration without explicit confirmation.
- When in doubt about a requirement: ask, do not assume.

## Delivery checklist (end of spec / before merge)
- Lint, typecheck, full test suite, build: green.
- <Your automated checks: licences, security audit, forbidden patterns, docs coherence…>
