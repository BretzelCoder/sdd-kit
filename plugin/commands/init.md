---
description: Add the SDD kit's rulebook, templates and docs to this project (run once, plugin install only)
---
Set up the SDD kit in the current project. The kit's files are in `${CLAUDE_PLUGIN_ROOT}`. The workflow commands themselves come from the plugin: do not copy `.claude/commands/` or `.claude/agents/`.

1. **Check first.** List which of these files already exist in the project, then show me the plan (copy, skip or merge for each file) and wait for my go-ahead:

   | Kit file (in `${CLAUDE_PLUGIN_ROOT}`) | Project file |
   |---|---|
   | `CLAUDE.md` | `CLAUDE.md` |
   | `docs/constitution.md` | `docs/constitution.md` |
   | `docs/architecture-decisions.md` | `docs/architecture-decisions.md` |
   | `docs/continuous-improvement.md` | `docs/continuous-improvement.md` |
   | `specs/000-template/spec.md`, `plan.md`, `tasks.md` | same paths |
   | `.claude/settings.example.json` | `.claude/settings.json`, only if it does not exist |

2. **Copy** each missing file as it is. **Never overwrite** an existing file:
   - an existing `CLAUDE.md`: propose to append the kit's sections that are missing ("Spec-Driven Development workflow — STRICT RULES", "Conventions", "Project commands", "Guardrails", "Delivery checklist") at the end, and append them only after my approval;
   - an existing `.claude/settings.json`: leave it, and list the kit's permissions it lacks, for me to add by hand if I want them;
   - any other existing file: skip it and say so.
3. **Adapt one thing in the copied `CLAUDE.md`**: the commands are installed by the plugin, so they run as `/sdd-kit:specify`, `/sdd-kit:plan`, and so on. Add this line under the "Spec-Driven Development workflow" heading: `Commands come from the sdd-kit plugin: /specify is /sdd-kit:specify, and so on.`
4. **Commit nothing.** I decide when and how to commit these files.
5. **Finish with what remains for me to do**, as a short checklist:
   - fill in the `<placeholders>` of `CLAUDE.md`: product context, stack, conventions, project commands (lint, typecheck, scoped tests, build), delivery checklist;
   - read `docs/constitution.md`, replace principle 8 with one of my own, and remove any principle I will not enforce;
   - write the first ADR (the main stack choice) in `docs/architecture-decisions.md`;
   - then run `/sdd-kit:specify <first feature>`.

   Point to the full guide: https://github.com/BretzelCoder/sdd-kit/blob/main/docs/GUIDE.md
