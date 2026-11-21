# Architecture - Flight Booking System (Group 17)

## Overview

The Flight Booking System is a three-tier web application. Customers, airline administrators, and the system manager use the web interface. The Backend API enforces access permissions and booking rules. The database stores the records used by the application.

The backend includes two internal modules for simulated payments and booking notifications.

## Components

| Component | Responsibility |
|-----------|----------------|
| Web Application | Provides pages for registration, login, flight search, seat selection, payment, e-tickets, and My Bookings. Provides management screens according to the user's role. |
| Backend API | Authenticates users, checks permissions, searches flights, and manages seat holds, bookings, cancellations, refunds, and ticket issuance. |
| Database | Stores users, airports, aircraft, flights, seats, bookings, payments, and tickets. |
| Payment Service (simulated) | Processes simulated payment requests, returns success or failure, and processes simulated refunds. |
| Notification Service (simulated) | Records a booking confirmation that the customer can view after the booking is confirmed. |

## Technology Stack

The team reviewed the alternatives and selected the following technologies.

| Area | Technology |
|------|---------------------|
| Backend | Python with FastAPI |
| Frontend | HTML, CSS, JavaScript |
| Database | SQLite |
| Testing | pytest |
| Development tools | Claude Code and GitHub |

## Key Design Decisions

### 1. Access to the database

The web application sends requests to the Backend API. The API validates each request, applies the business rules, and reads or updates the database.

### 2. Seat holds and booking outcomes

When a customer requests a booking, the backend checks that the seat belongs to the selected flight and is available. In one database transaction, it creates a `PENDING` booking, marks the seat as `HELD`, and records a hold expiry time 10 minutes later. This prevents two customers from reserving the same seat on the same flight.

| Outcome | Backend action |
|---------|----------------|
| Payment succeeds while the hold is active | Recheck the hold and update the booking to `CONFIRMED` and the seat to `BOOKED` in one transaction. Then issue the e-ticket and record the simulated confirmation. |
| Payment fails while the hold is active | Mark the pending booking as `CANCELLED` and release its seat. |
| The hold expires before confirmation | Mark the pending booking as `EXPIRED` and release its seat. A late payment result cannot confirm the expired booking. |

FR-07 covers seat selection and booking creation. FR-08 covers the 10-minute hold that prevents double booking. See [Requirements](requirements.md).

### 3. Simulated payments and notifications

The backend calls the Payment Service and Notification Service as internal modules. Payment processing, refunds, and confirmation messages are simulated within the application.

### 4. Role-based access

The Backend API checks the user's role before allowing a protected operation.

| Role | Permissions |
|------|-------------|
| Customer | Registers through the public interface, searches flights, selects seats, pays for bookings, and views or cancels their own eligible bookings. |
| Airline Administrator | Manages flights, airports, and aircraft. |
| System Manager | Creates and configures airline administrator accounts. |

Public registration creates customer accounts only.

FR-02 assigns administrator account creation to the System Manager. NFR-04 restricts flight, airport, and aircraft management to authorized airline administrators. See [Requirements](requirements.md).

### 5. Cancellations and refunds

A customer can cancel a confirmed booking before departure. The backend cancels the booking, releases the seat, and records the refund amount. A cancellation at least 14 days before departure receives a 50% refund. A cancellation less than 14 days before departure receives no refund.

## Diagrams

- [C4 System Context Diagram](../uml/c4_context.md)
- [C4 Container Diagram](../uml/c4_container.md)
- [Component Diagram](../uml/component_diagram.md)
- [Deployment Diagram](../uml/deployment_diagram.md)
- [Use Case Diagram](../uml/use_case_diagram.md)
- [Use Case Descriptions](../uml/use_case_description.md)
- [Class Diagram](../uml/class_diagram.md)
- [Booking Activity Diagram](../uml/activity_booking.md)
- [Booking Sequence Diagram](../uml/sequence_booking.md)
- [Booking State Diagram](../uml/state_booking.md)
- [Entity Relationship Diagram](../uml/erd.md)
