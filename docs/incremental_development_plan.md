# Incremental Development Plan - Flight Booking System (Group 17)

Each capability is built in two steps: a design version (`-design`, diagrams and specifications)
and a working version (code, AI-run tests, demo).

| Version | Type | Capability / Scope | Deliverable / Evidence | Requirements / Design Links |
|---------|------|--------------------|------------------------|-----------------------------|
| v0.1.0-design | Design | Users and authentication | Updated diagrams, specifications | Register, Login, Password hashing; `/uml/use_case_diagram.md`, `/uml/class_diagram.md` |
| v0.1.0 | Working | Users and authentication | Functional code, AI-run tests, demo | `src/auth`; `tests/test_auth` |
| v0.2.0-design | Design | Flight data management (admin) | Updated diagrams, specifications | Manage flights, Manage airports and aircraft, Admin-only access; `/uml/erd.md` |
| v0.2.0 | Working | Flight data management (admin) | Functional code, AI-run tests, demo | `src/flights`; `tests/test_flights` |
| v0.3.0-design | Design | Flight search | Updated diagrams, specifications | Search flights, Filter results, Search speed; `/uml/use_case_diagram.md` |
| v0.3.0 | Working | Flight search | Functional code, AI-run tests, demo | `src/search`; `tests/test_search` |
| v0.4.0-design | Design | Seat selection and booking | Updated diagrams, specifications | View seats, Book seat, Prevent double booking; `/uml/sequence_booking.md`, `/uml/state_booking.md` |
| v0.4.0 | Working | Seat selection and booking | Functional code, AI-run tests, demo | `src/booking`; `tests/test_booking` |
| v0.5.0-design | Design | Simulated payment and e-ticket | Updated diagrams, specifications | Pay, E-ticket; `/uml/sequence_booking.md` |
| v0.5.0 | Working | Simulated payment and e-ticket | Functional code, AI-run tests, demo | `src/payment`; `tests/test_payment` |
| v0.6.0-design | Design | Booking management, cancellation, notifications | Updated diagrams, specifications | View bookings, Cancel booking, Refund, Confirmation; `/uml/state_booking.md` |
| v0.6.0 | Working | Booking management, cancellation, notifications | Functional code, AI-run tests, demo | `src/bookings_mgmt`, `src/notifications`; `tests/test_cancellation` |
| v1.0.0 | Final | Integration, report, documentation | Final system, report PDF | All requirements, plus Responsive UI |

Paths under `src` and `tests` are planned and will be updated as the code is written.

## Increment Details

### v0.1.0 - Users and authentication
- **Main question:** How do users register and log in securely?
- **Tools:** Claude Code (implementation), Mermaid (diagrams), pytest (tests).
- **Acceptance criteria:** A new user can register; a registered user can log in and out; passwords are stored hashed; wrong credentials are rejected.

### v0.2.0 - Flight data management (admin)
- **Main question:** How does the admin maintain flights, airports, and aircraft?
- **Tools:** Claude Code, Mermaid (ERD), pytest.
- **Acceptance criteria:** Admin can add, edit, and delete flights, airports, and aircraft; a non-admin user cannot open admin pages.

### v0.3.0 - Flight search
- **Main question:** How does a customer find matching flights quickly?
- **Tools:** Claude Code, Mermaid, pytest.
- **Acceptance criteria:** Search by origin, destination, and date returns matching flights; results can be filtered and sorted by price and time; results appear within 3 seconds.

### v0.4.0 - Seat selection and booking
- **Main question:** How do we let a customer reserve a seat without two customers getting the same one?
- **Tools:** Claude Code, Mermaid (sequence and state diagrams), pytest.
- **Acceptance criteria:** Available seats are listed; selecting a seat creates a pending booking and holds the seat for 10 minutes; a held or booked seat cannot be selected by another customer; the hold expires if payment is not completed.

### v0.5.0 - Simulated payment and e-ticket
- **Main question:** How does a booking become confirmed after payment?
- **Tools:** Claude Code, Mermaid, pytest.
- **Acceptance criteria:** A successful simulated payment confirms the booking and issues an e-ticket; a failed payment releases the seat and does not confirm the booking.

### v0.6.0 - Booking management, cancellation, notifications
- **Main question:** How does a customer manage and cancel bookings, and what refund applies?
- **Tools:** Claude Code, Mermaid (state and activity diagrams), pytest.
- **Acceptance criteria:** Customer can list their bookings; cancelling 14 or more days before departure refunds 50%, later cancellation gives no refund; the seat is released; a simulated confirmation notification is recorded.

### v1.0.0 - Final release
- **Main question:** Does the whole system work end to end and is it documented?
- **Tools:** Claude Code, pytest, GitHub.
- **Acceptance criteria:** All requirements are implemented; all tests pass; traceability matrix is complete; report PDF is finished.