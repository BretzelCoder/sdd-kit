# Spec 001 — Export my contacts to CSV

> Status: APPROVED
> Created: 2026-01-10 · Approved: 2026-01-11

> Worked example for the kit. It shows the expected level of detail, not a real product.

## 1. Problem / Why
Users want to reuse their contact list in a spreadsheet or another tool. Today the data is locked in the app.

## 2. Users
Any signed-in user with at least one contact, mostly on desktop.

## 3. Expected behaviour (WHAT, not HOW)
- **S1** — As a user, when I click "Export contacts", then a CSV file with all my contacts is downloaded.
- **S2** — As a user with no contacts, when I open the contacts page, then the export button is disabled with an explanation.

## 4. Edge cases and errors
- Names containing commas, quotes or line breaks are exported without breaking the file.
- Accented characters open correctly in common spreadsheet tools.
- If the export fails, an error message is shown and nothing is downloaded.

## 5. Out of scope (explicit)
- Import from CSV.
- Exporting other objects (companies, applications).
- Scheduled or emailed exports.

## 6. Acceptance criteria (testable)
- [ ] AC-1 — The file contains exactly the user's contacts, never another user's.
- [ ] AC-2 — Columns: name, email, company, phone, last interaction date.
- [ ] AC-3 — A name with a comma, a quote and a line break survives a round trip in a CSV parser.
- [ ] AC-4 — The button is disabled when the user has no contacts.

## 7. Open questions
None (resolved: dates use ISO 8601, decided 2026-01-11).

## 8. Digital sobriety
The file is generated on demand, never stored. A server-side stream was considered and rejected: contact lists stay small, so a single generation is enough.

## 9. Decisions
- 2026-01-11, owner: ISO 8601 dates, no time zone.
- Help page: updated (export section). Search index: not applicable (no new text field).

## 10. Delivery and acceptance
Manual check in staging with a 500-contact account.
