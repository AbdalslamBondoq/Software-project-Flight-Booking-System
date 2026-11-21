# Requirements - Flight Booking System (Group 17)

The system scope and users are described in [`project_description.md`](project_description.md).

## 1. Functional Requirements

| ID | Requirement | Description | Actor |
|---|---|---|---|
| FR-01 | Register | The customer can register a new account. | Customer |
| FR-02 | Admin Account Creation | The System Manager creates and configures administrator accounts in advance. Public administrator registration is not allowed. | System Manager |
| FR-03 | Login and Logout | Customers, administrators, and the System Manager can log in and log out using their accounts. | Customer, Admin, System Manager |
| FR-04 | Search Flights | The customer can search for flights by origin, destination, and date. | Customer |
| FR-05 | Filter Results | The customer can filter and sort search results by price and time. | Customer |
| FR-06 | View Seats | The customer can view available seats for a flight. | Customer |
| FR-07 | Book Seat | A logged-in customer can select an available seat on a flight and create a PENDING booking. | Customer |
| FR-08 | Prevent Double Booking | When a pending booking is created, the system holds the seat for 10 minutes. Only one booking can hold or reserve the same seat on the same flight at a time. If the hold expires before confirmation, the system marks the pending booking as EXPIRED and releases the seat. | System |
| FR-09 | Pay | The customer can make a simulated payment for a pending booking. If payment succeeds while the seat hold is active, the system marks the booking as CONFIRMED and the seat as BOOKED. If payment fails while the hold is active, the system marks the booking as CANCELLED and releases the seat. | Customer |
| FR-10 | E-ticket | The system issues an e-ticket only after successful payment and booking confirmation. | System |
| FR-11 | View Bookings | The customer can view their own bookings and the current status of each booking. | Customer |
| FR-12 | Cancel Booking | The customer can cancel their own confirmed booking before departure. The system marks the booking as CANCELLED and releases the seat. | Customer |
| FR-13 | Refund | For a customer cancellation at least 14 days before departure, the system records a refund of 50% of the amount paid. For a cancellation less than 14 days before departure, the refund is zero. | System |
| FR-14 | Confirmation | After confirming a booking, the system records a simulated confirmation notification that the customer can view. | System |
| FR-15 | Manage Flights | The admin can add, edit, and delete flights. When a flight is added, the system creates its seats based on the aircraft capacity. | Admin |
| FR-16 | Manage Airports and Aircraft | The admin can manage airport and aircraft information. | Admin |

## 2. Non-Functional Requirements

| ID | Requirement | Description |
|---|---|---|
| NFR-01 | Password Hashing | Passwords must be stored using secure hashing, not as plain text. |
| NFR-02 | Search Speed | Search results should appear within 3 seconds, measured from submitting the search until the results are displayed, with up to 1,000 flights in the database. |
| NFR-03 | Responsive UI | All pages are usable at screen widths from 360 px (mobile) to 1920 px (desktop) without horizontal scrolling, and a customer can complete a booking on both a mobile and a desktop browser. |
| NFR-04 | Admin-only Access | Only authorized administrators can access flight, airport, and aircraft management pages. |

## 3. Assumptions

- Flight information is maintained by airline administrators.
- Customers use the application to search for and reserve flights.
- Each flight has defined seats available for reservation.
- Customer accounts are created through the registration process.
- Administrator accounts are created and configured in advance by the System Manager. Public administrator registration is not allowed.
- The System Manager account is created when the system is set up. It cannot be created through public registration.
- Payment is simulated, with no real payment gateway.
- Notifications are simulated and may be printed or saved, not sent as real emails.
- A booking cancelled 14 or more days before departure receives a 50% refund.
- A booking cancelled less than 14 days before departure receives no refund.
- A selected seat is held for 10 minutes. If payment is not completed within that time, the hold expires and the seat is released.

## 4. Constraints

- The application will be developed as a web application.
- The interface must support desktop and mobile browsers.
- Search results should appear within 3 seconds.
- Passwords must be stored using hashing rather than plain text.
- Only authorized airline administrators can manage flights, airports, and aircraft. Only the System Manager can create and configure administrator accounts.
- External payment and notification services will not be integrated.
- Development will follow the required incremental development approach.
- The project will use an Agentic AI development workflow.

## 5. Requirement ID Convention

- `FR` identifies a Functional Requirement.
- `NFR` identifies a Non-Functional Requirement.
- Each requirement has a unique and stable ID.
- These IDs are used in the architecture, incremental development plan, traceability matrix, and testing documentation.
