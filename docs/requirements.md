# Requirements - Flight Booking System (Group 17)

Scope and users are described in `project_description.md`.

## 1. Functional Requirements

| Requirement | Description | Actor |
|---|---|---|
| Register | The customer can register a new account. | Customer |
| Admin account creation | The system manager creates and configures administrator accounts in advance. Public administrator registration is not allowed. | System Manager |
| Login | Customers and administrators can log in and log out using their accounts. | Customer, Admin |
| Search flights | The customer can search for flights by origin, destination, and date. | Customer |
| Filter results | The customer can filter and sort search results by price and time. | Customer |
| View seats | The customer can view available seats for a flight. | Customer |
| Book seat | The customer can select an available seat and create a booking. | Customer |
| Prevent double booking | The system prevents two customers from booking the same seat by holding a selected seat for 10 minutes until payment is completed or the hold expires. | System |
| Pay | The customer can pay for a booking using simulated payment processing. | Customer |
| E-ticket | The system issues an e-ticket after successful payment. | System |
| View bookings | The customer can view their bookings. | Customer |
| Cancel booking | The customer can cancel a booking according to the cancellation policy. | Customer |
| Refund | The system calculates a refund on cancellation: 50% if cancelled 14 or more days before departure, and no refund otherwise. | System |
| Confirmation | The system generates a booking confirmation notification (simulated). | System |
| Manage flights | The admin can add, edit, and delete flights. | Admin |
| Manage airports and aircraft | The admin can manage airport and aircraft information. | Admin |

## 2. Non-Functional Requirements

| Requirement | Description |
|---|---|
| Password hashing | Passwords must be stored using secure hashing, not as plain text. |
| Search speed | Search results should appear within 3 seconds. |
| Responsive UI | The interface should work on desktop and mobile browsers. |
| Admin-only access | Only authorized administrators can access flight, airport, and aircraft management pages. |

## 3. Assumptions

- Flight information is maintained by airline administrators.
- Customers use the application to search for and reserve flights.
- Each flight has defined seats available for reservation.
- Customer accounts are created through the registration process.
- Administrator accounts are created and configured in advance by the system manager. Public administrator registration is not allowed.
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
