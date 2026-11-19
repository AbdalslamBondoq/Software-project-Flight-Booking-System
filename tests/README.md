# Tests

This folder contains the automated tests for the Flight Booking System. The tests are generated and run through the Agentic AI workflow, and the team reviews and classifies each one.

| Test level | What it verifies | Example |
|---|---|---|
| Unit | One function or class in isolation | Refund calculation for 14 days before departure |
| Component | One module through its interface | Seat hold component holds and releases seats |
| Integration | Modules working together through the API and database | Booking API creates a PENDING booking and holds the seat |
| System / end-to-end | A complete user workflow | Search, book, pay, and receive an e-ticket |

Each test is linked to its requirement IDs in `docs/traceability_matrix.md`. Results for each version are recorded in `docs/testing.md`. Tests run with `pytest`.
