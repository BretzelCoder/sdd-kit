# Plan 001 — Export my contacts to CSV

> Spec: `specs/001-csv-export/spec.md` (APPROVED 2026-01-11) · Plan status: APPROVED 2026-01-12

## 1. Summary
A server route reads the signed-in user's contacts through the existing repository, serialises them with the CSV helper already in the codebase, and returns a file download.

## 2. Requirement traceability
| Requirement | Technical answer |
|---|---|
| S1, AC-2 | `GET /api/export/contacts` returns `text/csv` with the five columns |
| AC-1 | Query goes through the repository, filtered by the session user; access-control test with two users |
| AC-3 | Existing CSV helper escapes per RFC 4180; unit test with a hostile name |
| S2, AC-4 | Button disabled when the contact count is 0 |

## 3. Architecture
Reuses the contacts repository (ADR-2). No new component outside the route and one button.

## 4. Data model
No change.

## 5. Interfaces
- Route: `GET /api/export/contacts`.
- UI: "Export contacts" button on the contacts page.

## 6. Test strategy
- Unit: CSV serialisation of the hostile name (AC-3).
- Integration: user A never receives user B's contacts (AC-1).
- End-to-end: click, download, check the header row (S1, AC-2), and the disabled state (AC-4).

## 7. Dependencies
None.

## 8. Risks and mitigations
| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Spreadsheet tool misreads accents | Medium | Low | UTF-8 with BOM, checked manually in staging |

## 9. Alternatives considered
- Client-side generation: rejected, it would require sending all contacts to the browser first, which the page does not do today.

## 10. Impact on project rules
Access control: applies (AC-1 test). New table: not applicable. Help page: applies.
