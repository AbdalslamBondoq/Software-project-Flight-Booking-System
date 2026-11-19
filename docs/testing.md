# Testing - Flight Booking System (Group 17)

This document describes how the system is tested and records the test results for each working version. The tests are generated, run, and maintained through the Agentic AI workflow. The team reviews each test, classifies it, and links it to its requirements in the [Traceability Matrix](traceability_matrix.md).

## 1. Test Levels

| Level | What it verifies | Location |
|---|---|---|
| Unit | One function or class in isolation, such as refund calculation or password hashing | `tests/unit/` |
| Component | One module through its public interface, such as the seat hold component | `tests/component/` |
| Integration | API endpoints working with the database, such as creating a pending booking | `tests/integration/` |
| System / end-to-end | A complete user workflow through the running application | `tests/system/` |

## 2. Tools

- `pytest` runs all automated tests.
- FastAPI's test client sends requests to the Backend API in integration tests.
- Each test run uses a fresh SQLite test database with synthetic seed data.

## 3. Key Test Scenarios

| Scenario | Requirements | Level | Version |
|---|---|---|---|
| Register a customer; reject a duplicate email | FR-01 | Integration | v0.1.0 |
| Only the System Manager can create administrator accounts | FR-02, NFR-04 | Integration | v0.1.0 |
| Log in with valid and invalid credentials; log out | FR-03 | Integration | v0.1.0 |
| Stored passwords are hashes, not plain text | NFR-01 | Unit | v0.1.0 |
| Admin adds, edits, and deletes flights, airports, and aircraft; other roles are rejected | FR-15, FR-16, NFR-04 | Integration | v0.2.0 |
| Search by origin, destination, and date; filter and sort results | FR-04, FR-05 | Integration | v0.3.0 |
| Search responds within 3 seconds on the documented test data | NFR-02 | System | v0.3.0 |
| Two simultaneous requests for the same seat: only one obtains the hold | FR-07, FR-08 | Integration | v0.4.0 |
| An expired 10-minute hold releases the seat and expires the booking | FR-08 | Component | v0.4.0 |
| Successful payment confirms the booking and issues an e-ticket | FR-09, FR-10 | Integration | v0.5.0 |
| Failed payment cancels the booking and releases the seat | FR-09 | Integration | v0.5.0 |
| Refund is 50% at 14 or more days before departure and zero otherwise | FR-13 | Unit | v0.6.0 |
| A customer sees only their own bookings and can cancel an eligible one | FR-11, FR-12 | Integration | v0.6.0 |
| Search, book, pay, and view the e-ticket on desktop and mobile widths | NFR-03 | System | v1.0.0 |

## 4. Results by Version

| Version | Tests run | Passed | Failed | Notes |
|---|---|---|---|---|
| v0.1.0 | - | - | - | Not yet implemented |
| v0.2.0 | - | - | - | Not yet implemented |
| v0.3.0 | - | - | - | Not yet implemented |
| v0.4.0 | - | - | - | Not yet implemented |
| v0.5.0 | - | - | - | Not yet implemented |
| v0.6.0 | - | - | - | Not yet implemented |
| v1.0.0 | - | - | - | Not yet implemented |

For each working version, record the `pytest` summary, explain any failure and how it was fixed, and link the pull request.
