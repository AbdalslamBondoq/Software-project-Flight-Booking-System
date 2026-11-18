# Requirements - Flight Booking System (Group 17)

The system scope and users are described in [`project_description.md`](project_description.md).

## 1. Functional Requirements

| ID | Requirement | Description | Actor |
|---|---|---|---|
| FR-01 | Register | The customer can register a new account. | Customer |
| FR-02 | Admin Account Creation | The System Manager creates and configures administrator accounts in advance. Public administrator registration is not allowed. | System Manager |
| FR-03 | Login and Logout | Customers and administrators can log in and log out using their accounts. | Customer, Admin |
| FR-04 | Search Flights | The customer can search for flights by origin, destination, and date. | Customer |
| FR-05 | Filter Results | The customer can filter and sort search results by price and time. | Customer |
| FR-06 | View Seats | The customer can view available seats for a flight. | Customer |
| FR-07 | Book Seat | The customer can select an available seat and create a booking. | Customer |
| FR-08 | Prevent Double Booking | The system prevents two customers from booking the same seat by holding a selected seat for 10 minutes until payment is completed or the hold expires. | System |
| FR-09 | Pay | The customer can pay for a booking using simulated payment processing. | Customer |
| FR-10 | E-ticket | The system issues an e-ticket after successful payment. | System |
| FR-11 | View Bookings | The customer can view their bookings. | Customer |
| FR-12 | Cancel Booking | The customer can cancel a booking according to the cancellation policy. | Customer |
| FR-13 | Refund | The system calculates a refund on cancellation: 50% if cancelled 14 or more days before departure, and no refund otherwise. | System |
| FR-14 | Confirmation | The system generates a booking confirmation notification (simulated). | System |
| FR-15 | Manage Flights | The admin can add, edit, and delete flights. | Admin |
| FR-16 | Manage Airports and Aircraft | The admin can manage airport and aircraft information. | Admin |

## 2. Non-Functional Requirements

| ID | Requirement | Description |
|---|---|---|
| NFR-01 | Password Hashing | Passwords must be stored using secure hashing, not as plain text. |
| NFR-02 | Search Speed | Search results should appear within 3 seconds. |
| NFR-03 | Responsive UI | The interface should work on desktop and mobile browsers. |
| NFR-04 | Admin-only Access | Only authorized administrators can access flight, airport, and aircraft management pages. |

## 3. Assumptions

- Flight information is maintained by airline administrators.
- Customers use the application to search for and reserve flights.
- Each flight has defined seats available for reservation.
- Customer accounts are created through the registration process.
- Administrator accounts are created and configured in advance by the System Manager. Public administrator registration is not allowed.
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
- Only authorized administrators can access administrative management pages.
- External payment and notification services will not be integrated.
- Development will follow the required incremental development approach.
- The project will use an Agentic AI development workflow.

## 5. Requirement ID Convention

- `FR` identifies a Functional Requirement.
- `NFR` identifies a Non-Functional Requirement.
- Each requirement has a unique and stable ID.
- These IDs are used in the architecture, incremental development plan, traceability matrix, and testing documentation.
