# Maintaining the kit

The kit is extracted from a real project (the "upstream") where the workflow keeps evolving. This document explains how upstream changes reach the kit, and which ones do not.

## 1. Last upstream sync

| Field | Value |
|---|---|
| Upstream state used | 2026-11-14 |
| Kit version | 1.1.1 |

Update this table at every release.

## 2. What is tracked upstream

Only the files that describe the process, never the product:

| Upstream file | Kit file |
|---|---|
| `.claude/commands/*.md` | `.claude/commands/*.md` |
| `.claude/agents/*.md` | `.claude/agents/*.md` |
| `specs/000-template/*` | `specs/000-template/*` |
| `docs/constitution.md` | `docs/constitution.md` |
| Method sections of the continuous-improvement document | `docs/continuous-improvement.md` |
| "Spec-Driven Development workflow" section of `CLAUDE.md` | same section of the kit's `CLAUDE.md` |

Everything else upstream (product rules, stack, security conventions, runbooks, specs) stays out.

## 3. Generic or project-specific?

For each upstream change, ask one question: **would a team with a different product and a different stack benefit from it?**

| Port it | Leave it upstream |
|---|---|
| A change to how a command behaves (when it stops, what it checks, in which order) | A rule about a specific table, library, provider or screen |
| A new step, gate or status in the cycle | A threshold or timing tuned to the upstream machine or CI |
| A new section in a template | A product decision or an abandoned feature |
| An improvement to the retrospective method | A reference to an upstream spec, action or incident by number |
| A new kind of guardrail (as a pattern, not as the upstream script) | Anything containing upstream names, paths, people or data |

When a change mixes both, port the generic principle and rewrite the example.

## 4. Release routine

1. **Detect**: list the upstream commits that touched the tracked files since the last sync date, and cross-check the upstream journal entries marked "kit impact: yes".
2. **Triage**: classify each one with the table in section 3.
3. **Port**: rewrite in English, generic wording, no upstream names. Update `docs/GUIDE.md` if the behaviour changes, and the worked example if a template changes. If the cycle changes (a step, a gate, a command), update the visuals from their sources in `docs/images/src/` and re-render them (see the README in that folder): the workflow visual shows the cycle, the evolution visual gets a new dated milestone.
4. **Check**: no upstream name or path left, internal links valid, commands consistent with the guide and with the visuals.
5. **Release**: bump the version (patch: wording or visuals; minor: new behaviour, step or template section; major: change to the cycle itself), add a CHANGELOG entry, update section 1 of this file. Once merged, tag `vX.Y.Z` on main and publish a GitHub release whose notes come from the CHANGELOG entry.

Suggested cadence: once a month, or right after an upstream change to the cycle itself.
