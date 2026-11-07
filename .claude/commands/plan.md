---
description: Produce the technical plan for an approved spec (step 2)
---
Spec: $ARGUMENTS (otherwise, the most recent one in specs/).

1. Check that spec.md contains no `[TO CLARIFY]` anymore. If any remain, STOP and ask me.
2. Re-read `docs/constitution.md`, `docs/architecture-decisions.md` (ADRs) and CLAUDE.md (imposed stack). No plan may contradict an ADR without a human discussion.
3. Create `plan.md` in the spec folder from `specs/000-template/plan.md`: architecture, data model (including access control), routes/API, UI components, test strategy, risks, and rejected alternatives (with justification).
4. Trace every technical choice back to a requirement of the spec. Flag any new dependency.
5. Present the plan for validation. NO code.
