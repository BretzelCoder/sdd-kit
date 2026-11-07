---
description: Break the plan into atomic, verifiable tasks (step 3)
---
Spec: $ARGUMENTS (otherwise, the most recent one with an approved plan.md).

1. Create `tasks.md` in the spec folder from `specs/000-template/tasks.md`: ordered list of tasks `- [ ] T-XX — description`, with explicit dependencies.
2. Each task: doable in under 1 hour, testable on its own, with an explicit definition of done (a passing test, an observable behaviour).
3. First task = migrations / data model. Tests are written BEFORE or WITH the code, never afterwards in bulk.
4. Present the list for validation. NO code.
