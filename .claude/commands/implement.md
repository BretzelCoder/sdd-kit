---
description: Implement the unchecked tasks of tasks.md (step 4)
---
Spec: $ARGUMENTS (otherwise, the most recent one with a tasks.md).

0. Work on a dedicated branch `NNN-slug`, created from an up-to-date main. Never implement directly on main. If another agent session is working in the same folder, use a dedicated git worktree instead of switching the shared folder's branch.
1. T-00, always: back up the local database before any operation on it, even if tasks.md mentions no migration.
2. By default, chain the unchecked tasks one after the other, without stopping between two tasks. For each task:
   - implement it with its tests;
   - run lint, typecheck and the tests scoped to the changed files, with the commands listed under "Project commands" in CLAUDE.md: everything must be green;
   - tick the box in tasks.md;
   - commit `feat(NNN): T-XX description` (or fix/chore/test), then move on to the next task.
   Run the full test suite mid-way only if the task touches shared code where scoped tests may miss regressions.
3. If you discover a gap with the spec: STOP immediately, explain, and propose an amendment to spec.md. Do not improvise.
4. Once the last task is ticked, run the full suite and the delivery checklist of CLAUDE.md once. Fix and re-run until green.
5. Stop and summarise only: at the end of tasks.md, on a gap (step 3), or if I explicitly asked for task-by-task control.
6. Never open a pull request or merge into main on your own initiative: always on my explicit request, confirmed at the time of the action.
