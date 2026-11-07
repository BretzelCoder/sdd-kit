# Tasks 001 — Export my contacts to CSV

> Plan: approved 2026-01-12 · Branch: `001-csv-export`

- [x] T-00 — Back up the local database.
- [x] T-01 — Unit test + serialisation of contacts with the CSV helper. Done when: hostile-name test passes (AC-3).
- [x] T-02 — Route `GET /api/export/contacts` with access-control integration test. Depends on: T-01. Done when: two-user test passes (AC-1, AC-2).
- [x] T-03 — Export button, disabled when there are no contacts, with end-to-end test. Depends on: T-02. Done when: e2e passes (S1, S2, AC-4).
- [x] T-04 — Help page section. Done when: text reviewed.
- [x] T-05 — Full test suite and delivery checklist green.
