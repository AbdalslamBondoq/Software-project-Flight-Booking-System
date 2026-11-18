# Incremental Development Plan - Flight Booking System (Group 17)

Each capability is built in two steps: a design version (`-design`, diagrams and specifications) and a working version (code, AI-run tests, demo).

## 1. Incremental Development Overview

| Version | Type | Capability / Scope | Deliverable / Evidence | Requirements / Design Links |
|---|---|---|---|---|
| v0.1.0-design | Design | Users, authentication, and administrator account creation | Updated diagrams, specifications | FR-01 Register, FR-02 Admin account creation, FR-03 Login and Logout, NFR-01 Password hashing, NFR-04 Admin-only access; `/uml/use_case_diagram.md`, `/uml/class_diagram.md` |
| v0.1.0 | Working | Users, authentication, and administrator account creation | Functional code, AI-run tests, demo | `src/auth`; `tests/test_auth` |
| v0.2.0-design | Design | Flight data management (admin) | Updated diagrams, specifications | FR-15 Manage flights, FR-16 Manage airports and aircraft, NFR-04 Admin-only access; `/uml/erd.md` |
| v0.2.0 | Working | Flight data management (admin) | Functional code, AI-run tests, demo | `src/flights`; `tests/test_flights` |
| v0.3.0-design | Design | Flight search | Updated diagrams, specifications | FR-04 Search flights, FR-05 Filter results, NFR-02 Search speed; `/uml/use_case_diagram.md` |
| v0.3.0 | Working | Flight search | Functional code, AI-run tests, demo | `src/search`; `tests/test_search` |
| v0.4.0-design | Design | Seat selection and booking | Updated diagrams, specifications | FR-06 View seats, FR-07 Book seat, FR-08 Prevent double booking; `/uml/sequence_booking.md`, `/uml/state_booking.md` |
| v0.4.0 | Working | Seat selection and booking | Functional code, AI-run tests, demo | `src/booking`; `tests/test_booking` |
| v0.5.0-design | Design | Simulated payment and e-ticket | Updated diagrams, specifications | FR-09 Pay, FR-10 E-ticket; `/uml/sequence_booking.md` |
| v0.5.0 | Working | Simulated payment and e-ticket | Functional code, AI-run tests, demo | `src/payment`; `tests/test_payment` |
| v0.6.0-design | Design | Booking management, cancellation, notifications | Updated diagrams, specifications | FR-11 View bookings, FR-12 Cancel booking, FR-13 Refund, FR-14 Confirmation; `/uml/state_booking.md` |
| v0.6.0 | Working | Booking management, cancellation, notifications | Functional code, AI-run tests, demo | `src/bookings_mgmt`, `src/notifications`; `tests/test_cancellation` |
| v1.0.0 | Final | Integration, report, documentation | Final system, report PDF | All requirements, including NFR-03 Responsive UI |

Paths under `src` and `tests` are planned and will be updated as the code is written.

## 2. Increment Details

### v0.1.0 - Users and Authentication

- **Main question:** How do users register and log in securely, and how are administrator accounts created?
- **Tools:** Claude Code (implementation), Mermaid (diagrams), pytest (tests).
- **Scope:**
  - Customers can register new accounts.
  - Customers and administrators can log in and log out.
  - Passwords are stored using secure hashing.
  - The System Manager creates and configures administrator accounts in advance.
  - Public administrator registration is not allowed.
  - The system restricts administrator account creation to the System Manager.
- **Acceptance criteria:**
  - A new customer can register.
  - The System Manager can create and configure administrator accounts.
  - Public administrator registration is not available.
  - A registered user can log in and out.
  - Passwords are stored hashed.
  - Wrong credentials are rejected.
  - Only authorized users can access protected administrative functions.

### v0.2.0 - Flight Data Management (Admin)

- **Main question:** How does the admin maintain flights, airports, and aircraft?
- **Tools:** Claude Code, Mermaid (ERD), pytest.
- **Acceptance criteria:**
  - Admin can add, edit, and delete flights, airports, and aircraft.
  - A non-admin user cannot open administrative management pages.

### v0.3.0 - Flight Search

- **Main question:** How does a customer find matching flights quickly?
- **Tools:** Claude Code, Mermaid, pytest.
- **Acceptance criteria:**
  - Search by origin, destination, and date returns matching flights.
  - Results can be filtered and sorted by price and time.
  - Search results appear within 3 seconds.

### v0.4.0 - Seat Selection and Booking

- **Main question:** How do we let a customer reserve a seat without two customers getting the same one?
- **Tools:** Claude Code, Mermaid (sequence and state diagrams), pytest.
- **Acceptance criteria:**
  - Available seats are listed.
  - Selecting a seat creates a pending booking and holds the seat for 10 minutes.
  - A held or booked seat cannot be selected by another customer.
  - The hold expires if payment is not completed within 10 minutes.

### v0.5.0 - Simulated Payment and E-ticket

- **Main question:** How does a booking become confirmed after payment?
- **Tools:** Claude Code, Mermaid, pytest.
- **Acceptance criteria:**
  - A successful simulated payment confirms the booking and issues an e-ticket.
  - A failed payment releases the seat and does not confirm the booking.

### v0.6.0 - Booking Management, Cancellation, and Notifications

- **Main question:** How does a customer manage and cancel bookings, and what refund applies?
- **Tools:** Claude Code, Mermaid (state and activity diagrams), pytest.
- **Acceptance criteria:**
  - Customer can list their bookings.
  - Cancelling 14 or more days before departure refunds 50%.
  - Cancellation less than 14 days before departure gives no refund.
  - The seat is released after cancellation.
  - A simulated confirmation notification is recorded.

### v1.0.0 - Final Release

- **Main question:** Does the whole system work end to end and is it documented?
- **Tools:** Claude Code, pytest, GitHub.
- **Acceptance criteria:**
  - All functional and non-functional requirements are implemented.
  - All tests pass.
  - The traceability matrix is complete.
  - The user interface supports desktop and mobile browsers.
  - The final report PDF is finished.

## 3. Development and Evidence Guidelines

- Each capability must have a design version before its working version.
- Design versions include the required diagrams and specifications.
- Working versions include functional code, AI-run tests, and a demonstration.
- Requirement IDs must remain consistent with `docs/requirements.md`.
- The traceability matrix in `docs/traceability_matrix.md` must be updated as requirements, designs, implementation, and tests change.
- Development work must be documented in the AI development log.
- Each increment must be supported by appropriate testing evidence.
- Changes must be committed through individual branches and Pull Requests.
