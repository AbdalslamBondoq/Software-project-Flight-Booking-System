# Source Code

This folder contains the application source code. The code is produced and maintained through the Agentic AI workflow described in `docs/ai_development_log.md`, and each module is linked to its requirements in `docs/traceability_matrix.md`.

Planned modules (see `docs/incremental_development_plan.md`):

| Module | Increment | Responsibility |
|---|---|---|
| `auth` | v0.1.0 | Registration, login/logout, password hashing, roles |
| `flights` | v0.2.0 | Flight, airport, and aircraft administration |
| `search` | v0.3.0 | Flight search, filtering, and sorting |
| `booking` | v0.4.0 | Seat availability, pending bookings, and 10-minute seat holds |
| `payment` | v0.5.0 | Simulated payment, booking confirmation, and e-tickets |
| `bookings_mgmt`, `notifications` | v0.6.0 | My Bookings, cancellation, refunds, and confirmation notifications |
