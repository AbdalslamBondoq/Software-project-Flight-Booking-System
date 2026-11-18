# Traceability Matrix - Flight Booking System (Group 17)

This document maps each system requirement to its related use cases, design artifacts, planned implementation version, and validation activities.

## 1. Functional Requirements Traceability

| Requirement ID | Requirement | Related Use Case / Design Element | Planned Version | Planned Validation | Status |
|---|---|---|---|---|---|
| FR-01 | Register | Register; User and Customer | v0.1.0-design, v0.1.0 | Registration tests | Design |
| FR-02 | Admin Account Creation | Admin Account Creation; System Manager | v0.1.0-design, v0.1.0 | Admin account creation tests | Design |
| FR-03 | Login and Logout | Login and Logout; Authentication | v0.1.0-design, v0.1.0 | Login and logout tests | Design |
| FR-04 | Search Flights | Search Flights; Flight | v0.3.0-design, v0.3.0 | Flight search tests | Design |
| FR-05 | Filter Results | Filter Results; Search Results | v0.3.0-design, v0.3.0 | Filtering and sorting tests | Design |
| FR-06 | View Seats | View Seats; Seat | v0.4.0-design, v0.4.0 | Seat availability tests | Design |
| FR-07 | Book Seat | Book Seat; Booking | v0.4.0-design, v0.4.0 | Booking creation tests | Design |
| FR-08 | Prevent Double Booking | Seat Hold; Booking and Seat states | v0.4.0-design, v0.4.0 | Concurrent booking and hold expiration tests | Design |
| FR-09 | Pay | Pay; Payment | v0.5.0-design, v0.5.0 | Simulated payment success and failure tests | Design |
| FR-10 | E-ticket | E-ticket Generation; Ticket | v0.5.0-design, v0.5.0 | E-ticket generation tests | Design |
| FR-11 | View Bookings | View Bookings; Booking | v0.6.0-design, v0.6.0 | Booking history tests | Design |
| FR-12 | Cancel Booking | Cancel Booking; Booking | v0.6.0-design, v0.6.0 | Booking cancellation tests | Design |
| FR-13 | Refund | Refund Calculation; Cancellation Policy | v0.6.0-design, v0.6.0 | Refund calculation tests | Design |
| FR-14 | Confirmation | Booking Confirmation; Notification | v0.6.0-design, v0.6.0 | Confirmation generation tests | Design |
| FR-15 | Manage Flights | Manage Flights; Flight Administration | v0.2.0-design, v0.2.0 | Flight management tests | Design |
| FR-16 | Manage Airports and Aircraft | Manage Airports and Aircraft | v0.2.0-design, v0.2.0 | Airport and aircraft management tests | Design |

## 2. Non-Functional Requirements Traceability

| Requirement ID | Requirement | Related Design Element | Planned Version | Planned Validation | Status |
|---|---|---|---|---|---|
| NFR-01 | Password Hashing | Authentication and User Data | v0.1.0-design, v0.1.0 | Verify that passwords are stored using secure hashing | Design |
| NFR-02 | Search Speed | Flight Search and Database Queries | v0.3.0-design, v0.3.0 | Measure search response time; target under 3 seconds | Design |
| NFR-03 | Responsive UI | Web Application Interface | v1.0.0 | Test the interface on desktop and mobile browsers | Design |
| NFR-04 | Admin-only Access | Authentication and Authorization | v0.1.0-design, v0.1.0, v0.2.0-design, v0.2.0 | Verify that unauthorized users cannot access administrative management pages | Design |

## 3. Design Artifact References

| Design Artifact | Related Requirements / Scope |
|---|---|
| `uml/c4_context.md` | System scope and external actors |
| `uml/c4_container.md` | Application containers and interactions |
| `uml/component_diagram.md` | Main software components |
| `uml/use_case_diagram.md` | Functional requirements and actors |
| `uml/use_case_description.md` | Detailed use case scenarios |
| `uml/sequence_booking.md` | Booking, seat hold, payment, and confirmation workflow |
| `uml/activity_booking.md` | Main booking activity workflow |
| `uml/state_booking.md` | Booking lifecycle and state transitions |
| `uml/class_diagram.md` | Main application and domain classes |
| `uml/erd.md` | Database entities and relationships |
| `uml/deployment_diagram.md` | Deployment structure |
| `docs/architecture.md` | System architecture and non-functional requirements |

## 4. Status Definitions

- **Design:** The requirement and its design representation are documented. Implementation and testing have not yet been completed.
- **In Progress:** Implementation or validation is currently underway.
- **Implemented:** The corresponding functionality has been implemented.
- **Tested:** The relevant tests have been executed successfully.
- **Verified:** The requirement has been checked against its acceptance criteria.

## 5. Maintenance

This matrix shall be updated during each development increment.

When a requirement, design artifact, implementation module, or test changes, the corresponding traceability entry must also be updated.

Planned versions and validation activities may be revised as the incremental development plan is reviewed.
