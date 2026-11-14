# Requirements - Flight Booking System (Group 17)

Scope and users are described in `project_description.md`.

## Functional Requirements

| Requirement | Description | Actor |
|-------------|-------------|-------|
| Register | The user can register a new account | Customer |
| Login | The user can log in and log out | Customer, Admin |
| Search flights | The customer can search flights by origin, destination, and date | Customer |
| Filter results | The customer can filter and sort search results (price, time) | Customer |
| View seats | The customer can view available seats for a flight | Customer |
| Book seat | The customer can select a seat and create a booking | Customer |
| Prevent double booking | The system prevents two customers from booking the same seat by holding a selected seat for 10 minutes until payment is completed or the hold expires | System |
| Pay | The customer can pay for a booking (simulated payment) | Customer |
| E-ticket | The system issues an e-ticket after successful payment | System |
| View bookings | The customer can view their bookings | Customer |
| Cancel booking | The customer can cancel a booking | Customer |
| Refund | The system calculates a refund on cancellation (50% if cancelled 14 or more days before departure, no refund otherwise) | System |
| Confirmation | The system sends a booking confirmation notification (simulated) | System |
| Manage flights | The admin can add, edit, and delete flights | Admin |
| Manage airports and aircraft | The admin can manage airports and aircraft | Admin |

## Non-Functional Requirements

| Requirement | Description |
|-------------|-------------|
| Password hashing | Passwords must be stored hashed, not as plain text |
| Search speed | Search results should appear within 3 seconds |
| Responsive UI | The interface should work on desktop and mobile browsers |
| Admin-only access | Only admins can access flight management pages |

## Assumptions

- Payment is simulated, no real payment gateway.
- Notifications are simulated (printed or saved, not real emails).
- Refund policy: a booking cancelled 14 or more days before departure is refunded 50%; a booking cancelled less than 14 days before departure is not refunded.
- Seat hold: a selected seat is held for 10 minutes. If payment is not completed within that time, the hold expires and the seat is released.