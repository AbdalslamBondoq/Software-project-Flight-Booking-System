# Architecture - Flight Booking System (Group 17)

## Overview
The system is a three-tier web application: a web interface, a backend API that holds
the business logic, and a database. Payment and notifications are simulated services
called by the backend.

## Components
| Component | Responsibility |
|-----------|----------------|
| Web Application | Pages for search, seat selection, booking, payment, e-ticket, "my bookings", and admin screens |
| Backend API | Authentication, flight search, booking rules, seat holding, cancellation and refund logic |
| Database | Stores users, airports, aircraft, flights, seats, bookings, payments, tickets |
| Payment Service (simulated) | Returns success or failure for a payment request |
| Notification Service (simulated) | Records a confirmation message instead of sending a real email |

## Technology Stack (proposed, to be confirmed by the team)
- Backend: Python with FastAPI
- Frontend: HTML, CSS, JavaScript
- Database: SQLite
- Testing: pytest
- Development: Agentic AI (Claude Code), GitHub for version control

## Key Design Decisions
1. **Layered structure:** the web app never touches the database directly; it goes through the API.
   This keeps business rules in one place.
2. **Seat holding:** when a customer selects a seat, the backend marks it as "held" before payment.
   If payment fails or times out, the seat is released. This prevents double booking (FR-07).
3. **Simulated external services:** payment and notifications are separate modules behind a simple
   interface, so they can be replaced by real services later without changing the booking logic.
4. **Role-based access:** admin pages are only available to users with the admin role (NFR-04).

## Diagrams
- Context and containers: `/uml/c4_diagrams.md`
- Use cases: `/uml/use_case_diagram.md`
- Classes: `/uml/class_diagram.md`
- Booking flow: `/uml/sequence_booking.md`
- Booking states: `/uml/state_booking.md`
- Data model: `/uml/erd.md`
