---
description: Spec <-> code compliance review (step 5)
---
Spec: $ARGUMENTS (otherwise, the most recent one).

0. Prepare the review: base = `git merge-base origin/main HEAD` (after `git fetch`); write the full diff and its file list to a scratch file. Choose a mode and say why:
   - **parallel** if the diff touches a migration or more than 10 files outside docs/ and specs/;
   - **solo** otherwise (a sub-agent starts from scratch and costs more).
1. Re-read spec.md and compare it with the code actually produced.
2. Check: is every requirement covered? Are the tests present and meaningful? Any scope creep (code with no matching requirement)?
3. Check each applicable convention of CLAUDE.md, explicitly naming those that do not apply (and why). Group them in axes, for example:
   - **axis A, schema and security**;
   - **axis B, fields and data**;
   - **axis C, interface and documentation**.
   In parallel mode, launch in a single message one `review-axis` sub-agent per axis (read-only), each given only the spec, the plan, the diff file and its axis. Do steps 1 and 2 while they work.
4. Consolidate: re-check every reported gap at its file:line before keeping it. An unconfirmed report is dropped, and said so.
5. Verdict: COMPLIANT / GAPS (precise list, with file:line).
6. Fix nothing without my approval.
