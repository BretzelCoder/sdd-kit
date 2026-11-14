# Changelog

This kit is extracted from the workflow used on a real production project between July and November 2026. The dates below are those of that project.

![How the workflow evolved from July to November 2026](docs/images/evolution.png)

## 1.2.0 — 2026-11
### Added
- **Claude Code plugin**: `/plugin install sdd-kit --marketplace BretzelCoder/sdd-kit`. The repository is its own marketplace (`.claude-plugin/`). With the plugin, the commands run as `/sdd-kit:specify`, `/sdd-kit:plan`, and so on.
- **`/sdd-kit:init`** (plugin only): copies the rulebook, the docs and the spec templates into the project without overwriting anything, then lists what remains to fill in.
- **Contributing**: `CONTRIBUTING.md`, issue forms (experience report, problem with a command, port to another agent, rule proposal), a pull request template, and Discussions for questions.
- **`Kit checks` workflow**: fails if the plugin's copy of the review agent differs from the kit's, or if the plugin version differs from the latest CHANGELOG entry.
- Plugin icon, with its source in `docs/images/src/`.

### Changed
- `/implement` runs the commands listed under "Project commands" in `CLAUDE.md`, instead of a placeholder inside the command. That removes a setup step, and the command works unchanged when installed as a plugin.
- `/review` gives the plugin's name for the review agent (`sdd-kit:review-axis`).

## 1.1.2 — 2026-11
### Added
- Repository social preview (`docs/images/social-preview.png`, 1280 × 640 px), with its source in `docs/images/src/`.

### Changed
- Workflow visual says "commands" instead of "skills", like the README, the guide and `.claude/commands/`.

## 1.1.1 — 2026-11
### Changed
- Workflow visual (`docs/images/workflow.png`) shows the optional `/brainstorm` step: a dashed step 0 before `/specify`, and an optional human gate (specify, postpone or drop). The three mandatory human gates stay unchanged.
- Evolution visual (`docs/images/evolution.png`): no more references to the source project (its name, spec and action numbers), as section 3 of `MAINTAINING.md` requires; new 14 November milestone for `/brainstorm`. The image now sits at the top of this changelog, since it covers every version.

### Added
- Editable sources of both visuals, with render instructions: `docs/images/src/`.

## 1.1.0 — 2026-11
### Added
- `/brainstorm`: optional framing step before `/specify`, for topics that are still unclear. Entry test, one-question-at-a-time interview, current state backed by file:line evidence, two or three options including "do nothing", mandatory outcome (framing note, postpone or drop). No code, no spec, no branch.

### Changed
- `/specify` starts from an existing framing note and asks only its open questions.

### How the workflow got there
- **2026-11-14** — Optional framing step before `/specify`, after several specs were reworked because of unverified claims about existing behaviour.

## 1.0.0 — 2026-11 (first public version, MIT licence)
Generic, English version of the workflow as of November 2026.

### How the workflow got there
- **2026-07-17** — Initial light kit: 5 slash commands, 6 rules. `/implement` did one task, then stopped for a go-ahead. Built on the same principle as GitHub Spec Kit, lighter.
- **2026-08-14** — Tasks chained by default; one dedicated branch per spec; pull request and merge only on explicit request.
- **2026-08-15 / 16** — Database backup before every `/implement` (T-00); scoped tests per task, full suite at the end of the spec.
- **2026-08-27** — Isolated git worktree only when a concurrent session is a real risk.
- **2026-09-08** — CI/CD: project rules start becoming automated checks.
- **2026-10-15** — Spec lifecycle statuses, verified in CI.
- **2026-10-16** — Retrospective after every session (self-critique and rapport d'étonnement); `/review` split into parallel read-only sub-agents.
- **2026-10-28** — Rulebook streamlined; every rule traced to the spec that created it.
