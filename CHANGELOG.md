# Changelog

This kit is extracted from the workflow used on a real production project between July and November 2026. The dates below are those of that project.

## 1.0.0 — 2026-11 (first public version, MIT licence)
Generic, English version of the workflow as of November 2026.

### How the workflow got there

![How the workflow evolved from July to November 2026](docs/images/evolution.png)

- **2026-07-17** — Initial light kit: 5 slash commands, 6 rules. `/implement` did one task, then stopped for a go-ahead. Built on the same principle as GitHub Spec Kit, lighter.
- **2026-08-14** — Tasks chained by default; one dedicated branch per spec; pull request and merge only on explicit request.
- **2026-08-15 / 16** — Database backup before every `/implement` (T-00); scoped tests per task, full suite at the end of the spec.
- **2026-08-27** — Isolated git worktree only when a concurrent session is a real risk.
- **2026-09-08** — CI/CD: project rules start becoming automated checks.
- **2026-10-15** — Spec lifecycle statuses, verified in CI.
- **2026-10-16** — Retrospective after every session (self-critique and rapport d'étonnement); `/review` split into parallel read-only sub-agents.
- **2026-10-28** — Rulebook streamlined; every rule traced to the spec that created it.
