---
description: Frame a still-unclear topic before specifying it (optional step, before /specify)
---
Topic to frame: $ARGUMENTS

**Optional** step before `/specify`: study a topic that is still unclear, then decide whether it becomes a spec. Framing produces a decision, never code.

1. **Entry test.** If the problem, the solution and the scope are already clear (a fix, a small UX change), say so and suggest `/specify` directly, without framing. Framing is for topics with several possible solutions, external methods or documents to analyse, or a privacy, security or production stake.
2. **Register and history.** Re-read the open actions in `docs/continuous-improvement.md`, especially those triggered by `/specify`. Check whether the topic was already explored: notes in `docs/brainstorm/`, related specs in `specs/`, postponed actions in the register.
3. **Interview, one question at a time.** Problem and why first (for whom, what pain), before any solution. Then the appetite: a fix, a medium spec, or a spec split into batches. Ask only when the answer changes what will be built; otherwise propose a default. Before asking about a behaviour or a user action, read the code that handles it.
4. **Verified current state.** Every statement about existing behaviour cites the file and line read during the session, never from memory; every claimed absence cites the search that proves it. For a UI element, compare with the neighbouring screen that shows the same data, and measure the space available on the existing screen. For anything that touches production data, check it against the project's data-access rules.
5. **External research**, when it helps (methods, market practices, documents supplied by the owner): sources cited; copyrighted material paraphrased, without long quotes; no third-party names or faces.
6. **Options.** Two or three real approaches with their trade-offs, always including the leanest one and "do nothing". Recommend one and argue for it.
7. **First pass on the cross-cutting rules** of `CLAUDE.md` (Conventions) and of the constitution: for each, applies, does not apply, or to be decided in the spec.
8. **Mandatory outcome**, chosen by the owner:
   - **to `/specify`**: a framing note `docs/brainstorm/<slug>.md`, where `<slug>` is a short English name (two or three words in kebab-case, e.g. `csv-export.md`): date, status, sources, problem, appetite, current state with its evidence, options and recommendation, decisions made, out of scope, open questions. If the framing was long, suggest running `/specify` in a fresh session that starts from the note;
   - **postpone**: the note if it has substance, and an action in the register of `docs/continuous-improvement.md` (owner, trigger) pointing to it;
   - **drop**: no note; the reason is given in the closing message.

Framing never lives only in the agent's memory: that memory is neither versioned nor visible to the owner.

**Forbidden during framing**: writing code, creating a `specs/NNN-…` folder or a `spec.md`, picking a spec number, creating or switching branches. Reading, searching and browsing the web remain allowed. Nothing is committed without the owner's approval: the note joins the branch of the spec it prepares, or a separate `docs:` commit, on request, if the topic is postponed.
