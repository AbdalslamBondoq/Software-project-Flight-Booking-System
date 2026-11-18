# Incremental Development Plan - Flight Booking System (Group 17)

## 1. Incremental Development Overview

Each capability has two planned versions. The `-design` version defines the expected behavior through diagrams and specifications. The working version implements that behavior and provides code, AI-run test results, and a demonstration. The acceptance criteria below describe what each version must demonstrate before it is considered complete.

| Design version | Working version | Capability | Requirements | Design references |
|---|---|---|---|---|
| v0.1.0-design | v0.1.0 | User accounts, authentication, and administrator account creation | FR-01, FR-02, FR-03, NFR-01, NFR-04 | [Use case descriptions](../uml/use_case_description.md), [Class diagram](../uml/class_diagram.md) |
| v0.2.0-design | v0.2.0 | Administration of flights, airports, and aircraft | FR-15, FR-16, NFR-04 | [ERD](../uml/erd.md), [Use case descriptions](../uml/use_case_description.md) |
| v0.3.0-design | v0.3.0 | Flight search, filtering, and sorting | FR-04, FR-05, NFR-02 | [Use case diagram](../uml/use_case_diagram.md), [Use case descriptions](../uml/use_case_description.md) |
| v0.4.0-design | v0.4.0 | Seat availability, pending bookings, and 10-minute holds | FR-06, FR-07, FR-08 | [Booking sequence](../uml/sequence_booking.md), [Booking states](../uml/state_booking.md), [ERD](../uml/erd.md) |
| v0.5.0-design | v0.5.0 | Simulated payment, booking confirmation, and e-ticket issuance | FR-09, FR-10 | [Booking sequence](../uml/sequence_booking.md), [Booking activity](../uml/activity_booking.md) |
| v0.6.0-design | v0.6.0 | My Bookings, cancellations, refunds, and simulated confirmation notifications | FR-11, FR-12, FR-13, FR-14 | [Booking states](../uml/state_booking.md), [Use case descriptions](../uml/use_case_description.md) |
| — | v1.0.0 | Final integration, responsive UI, and documentation | All functional and non-functional requirements, including NFR-03 | [Architecture](architecture.md), [Traceability matrix](traceability_matrix.md) |

## 2. Increment Details

### v0.1.0 - User Accounts and Authentication

**Main question.** How do customers register and log in, and who can create administrator accounts?

**Design acceptance criteria**

- The use cases distinguish public customer registration from administrator account creation by the System Manager.
- The account model identifies the Customer, Airline Administrator, and System Manager roles and specifies storage of password hashes.
- The login flow describes successful authentication, rejection of invalid credentials, and logout.

**Working acceptance criteria**

- A customer can register through the public interface. Public registration creates only customer accounts.
- The System Manager can create and configure an administrator account. Other roles cannot perform this operation.
- Customers and administrators can log in and out. The system rejects incorrect credentials and stores passwords as secure hashes.

### v0.2.0 - Flight Data Management

**Main question.** How does an airline administrator maintain flight data while preserving valid airport and aircraft references?

**Design acceptance criteria**

- The ERD shows that each flight has one origin airport, one destination airport, and one assigned aircraft.
- The administration use cases identify who can manage flights, airports, and aircraft and describe how the system handles invalid data.

**Working acceptance criteria**

- An authorized airline administrator can add, edit, and delete flights, airports, and aircraft, subject to referential integrity.
- The system prevents deletion of an airport or aircraft referenced by an existing flight.
- The backend rejects flight, airport, and aircraft management requests from users without the airline administrator role.

### v0.3.0 - Flight Search

**Main question.** How does a customer find flights that match their travel plans?

**Design acceptance criteria**

- The search use case identifies origin, destination, and travel date as inputs and describes both matching results and the no-results case.
- The specification describes filtering and sorting by price and time and records the three-second search target from NFR-02.

**Working acceptance criteria**

- A search returns flights matching the origin, destination, and travel date. A search with no matches displays an appropriate message.
- Customers can filter and sort results by price and time.
- Search results appear within three seconds in the documented test scenario.

### v0.4.0 - Seat Selection and Booking

**Main question.** What happens when two customers request the same seat on the same flight?

**Design acceptance criteria**

- The booking sequence shows that checking availability, creating a pending booking, and holding the seat occur in one database transaction.
- The state diagram distinguishes the `PENDING` booking from the `HELD` seat and shows how an expired hold releases the seat.

**Working acceptance criteria**

- A customer can view seat availability for a selected flight. A logged-in customer can request an available seat.
- A successful request creates a `PENDING` booking, marks the seat as `HELD`, and records an expiry time 10 minutes later.
- If two customers request the same available seat simultaneously, only one obtains the hold. The other is informed that the seat is unavailable.
- When the hold expires before confirmation, the booking becomes `EXPIRED` and the seat becomes available again.

### v0.5.0 - Simulated Payment and E-ticket

**Main question.** Under what conditions can a pending booking be confirmed and an e-ticket issued?

**Design acceptance criteria**

- The booking sequence and activity diagram distinguish successful payment, failed payment, and hold expiry during payment.
- The confirmation flow checks that the booking is still pending and its hold is still active before marking the seat as booked.

**Working acceptance criteria**

- Successful simulated payment during an active hold changes the booking to `CONFIRMED`, marks the seat as `BOOKED`, and produces an e-ticket with a unique ticket number.
- Failed payment during an active hold changes the booking to `CANCELLED`, releases the seat, and produces no ticket.
- If the hold expires before confirmation, a late payment result cannot confirm the expired booking or generate a ticket.

### v0.6.0 - Booking Management, Cancellation, and Notifications

**Main question.** How does a customer view or cancel a reservation, and which refund applies?

**Design acceptance criteria**

- The use cases show that customers can view their own bookings and cancel their own confirmed bookings before departure.
- The cancellation policy specifies the refund on both sides of the 14-day cutoff, including cancellation exactly 14 days before departure.
- The notification flow identifies successful booking confirmation as the event that triggers a simulated notification.

**Working acceptance criteria**

- My Bookings displays only the logged-in customer's bookings and their statuses.
- Cancelling an eligible confirmed booking before departure changes its status to `CANCELLED` and releases the seat.
- Cancellation exactly 14 days or more before departure records a refund of 50% of the amount paid. Cancellation less than 14 days before departure records a refund of zero.
- The system rejects customer cancellation once the flight has departed.
- A confirmed booking has a simulated confirmation notification that the customer can view.

### v1.0.0 - Final Release

**Main question.** Does the integrated application meet its requirements across the complete booking workflow?

**Acceptance criteria**

- A customer can search for a flight, reserve a seat, complete simulated payment, and view the resulting booking, e-ticket, and confirmation.
- The main customer workflow is usable on desktop and mobile browsers as required by NFR-03.
- All functional and non-functional requirements have corresponding evidence in the traceability matrix.
- The test suite passes, the demonstrations are documented, and the final report PDF is complete.

## 3. Development and Evidence Guidelines

- Complete the design version of each capability before its working version.
- For a design version, link the relevant diagrams and specifications and check them against the design acceptance criteria.
- For a working version, provide the implementation, AI-run test results, and a demonstration of the working acceptance criteria.
- Use Mermaid for diagrams, Claude Code for the planned AI-assisted development workflow, pytest for tests, and GitHub for version control and pull requests.
- Record AI-assisted development work in the AI development log.
- Keep requirement IDs consistent with [Requirements](requirements.md). Update the [Traceability Matrix](traceability_matrix.md) with the actual source paths, tests, and evidence as they become available.
- Use a dedicated branch and pull request for each increment's changes.