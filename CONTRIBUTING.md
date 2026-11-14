# Contributing to the SDD kit

Thank you for helping. The kit improves the same way it asks you to improve your own project: from real incidents, one small rule at a time.

## Ways to contribute

| You want to… | Open… |
|---|---|
| Tell how the kit went on your project: what worked, what got in the way | an issue, **Experience report** |
| Report a command that misbehaves, or docs that contradict each other | an issue, **Problem with a command** |
| Adapt the kit to another agent (Cursor, Codex, Copilot, Gemini CLI…) | an issue, **Port to another agent** |
| Suggest a new rule, gate or template section | an issue, **Rule proposal** |
| Ask a question or share an idea that isn't ready yet | a [discussion](https://github.com/BretzelCoder/sdd-kit/discussions) |

Experience reports are the most useful contribution. Every rule in the kit came from an incident, and your incidents are how the next rules get found.

## What makes a good change

The kit follows the triage in [MAINTAINING.md](MAINTAINING.md), section 3. Before you propose a change, check that:

- **It is generic.** A team with a different product and a different stack would benefit from it.
- **It comes from something that happened.** Describe the incident or the friction behind it. A rule with no story behind it is hard to judge.
- **It keeps the kit light.** Prefer sharpening an existing rule to adding a new one. If your change adds a step, say what it replaces or why the cost is worth it.
- **It contains no private data.** No company, product, person or customer names, and no internal paths.

## Pull requests

1. For anything beyond a typo, open an issue first, so we agree on the problem before you write the fix.
2. Branch from an up-to-date `main` and keep one topic per pull request.
3. Write in English, plain and short, like the rest of the kit.
4. Keep everything consistent: a change to a command updates `docs/GUIDE.md`, and `README.md` when the cycle changes. If you change a visual, edit its source in `docs/images/src/` and re-render it.
5. Add a line under `## Unreleased` at the top of `CHANGELOG.md`. The maintainer picks the version number at release time.
6. The `Kit checks` workflow must pass.

The maintainer reviews, merges and releases. Releases follow the routine in [MAINTAINING.md](MAINTAINING.md), section 4.

## Licence

By contributing, you agree that your contribution is licensed under the [MIT licence](LICENSE) of this repository.
