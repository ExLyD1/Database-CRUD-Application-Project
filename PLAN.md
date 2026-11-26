# Team plan: Simulated Crypto Exchange

Course: Database Systems (FHWN, B.CSCI.V.26). This file is our internal plan. It is **not submitted**. The submitted spec is `description.md`.

## Project in one paragraph

A simulated crypto exchange. No real money, no external APIs. The admin sets coin prices by hand (each with a timestamp). Users buy and sell at the current listed price (no order book). One currency (EUR), one time zone.

## Hard requirements (from Hegyhati)

- Groups of 4, fixed.
- Rust + PostgreSQL are mandatory. CLI or TUI expected (a GUI only with his later restrictions).
- `description.md` must follow the FlightTracker template: title, short intro, features grouped by role and ordered by dependency, each feature = bold name + one line + bullet rules, separated by `---`. No tables or columns in the text.
- No draft on 1 Dec means no feedback. A missing or too weak final proposal means 0 points for everyone.
- Grading is per person, but equal if everyone worked about equally.

## Deadlines (Moodle deadlines are 08:00)

| Date | What |
|------|------|
| 27 Nov | Our internal draft done. Moodle assignment opens. |
| 30 Nov | Everything merged and reviewed. Submit in the evening. |
| 1 Dec 08:00 | Submit the first `description.md` |
| 10 Dec | Revision assignment opens |
| 12 Dec | Submit revised spec (after feedback) |
| 4 Jan | Final upload opens |
| 6 Jan | Final code and documentation |
| 7-8 Jan | Presentations (slot not published yet) |

## Planned features (names only, text goes into description.md)

**Admin**: add network, list networks, add coin, delist coin, list and search coins, set price.

**User**: register, deposit EUR, withdraw EUR, buy coin, sell coin, view portfolio, view transaction history.

**Analyst** (3 features with real SQL, top-N / grouping / time windows):
- Top coins (or networks) by trading volume
- Top gainers and losers (price change in a period)
- Biggest profits and losses

## Who owns what

Each person owns a few features end to end (spec, schema, code, docs), so everyone can defend their part.

| Person | Features | Status |
|--------|----------|--------|
| A | TBD | |
| B | TBD | |
| C | TBD | |
| D | TBD | |

## Open items

- [ ] Agree on the topic with the group
- [ ] Choose the 3 analysis features
- [ ] Split features between 4 people
- [ ] Fill in the `description.md` skeleton
- [ ] Peer review of each other's sections before 30 Nov
- [ ] Optional: ask Hegyhati whether AI help is allowed for the proposal text
- [ ] Update the Notion DB Systems page with his 24 Nov email facts (what is needed now, grading, stack)

## Working rules

- Work in branches, merge via pull request, someone else reviews.
- Every analysis feature must need real SQL. If it could be done by one `SELECT *`, it is too easy.
