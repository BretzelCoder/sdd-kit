---
description: Create a new functional specification (step 1 of the SDD cycle)
---
Requested feature: $ARGUMENTS

1. Find the next number NNN by listing `specs/`, then create `specs/NNN-<slug>/spec.md` from `specs/000-template/spec.md`, with status `DRAFT`.
2. ASK ME FIRST: 3 to 6 targeted questions on the grey areas (target user, edge cases, what is OUT of scope, measurable success criteria). Write the spec only after my answers. If a framing note exists for this topic (`docs/brainstorm/*.md`, produced by `/brainstorm`), start from its decisions, ask only its open questions and what it left undecided, and cite it in the spec. If the topic is still too unclear for these questions (several possible solutions, external documents to analyse), suggest `/brainstorm` first.
3. Write the spec: WHAT and WHY only, no technical decision (no library name, no database schema). Every requirement must be testable. Fill in every section of the template, saying for each project rule whether it applies.
4. Mark any remaining uncertainty with `[TO CLARIFY]`.
5. Present the spec for validation. Write NO code, create neither plan.md nor tasks.md. When I approve, set the status to `APPROVED` with the approval date.
