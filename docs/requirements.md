# Requirements - Flight Booking System (Group 17)

## Functional Requirements (شو بيعمل النظام)

| ID | Requirement | Actor |
|----|-------------|-------|
| FR-01 | The user can register a new account | Customer |
| FR-02 | The user can log in and log out | Customer, Admin |
| FR-03 | The customer can search flights by origin, destination, and date | Customer |
| FR-04 | The customer can filter and sort search results (price, time) | Customer |
| FR-05 | The customer can view available seats for a flight | Customer |
| FR-06 | The customer can select a seat and create a booking | Customer |
| FR-07 | The system prevents two customers from booking the same seat | System |
| FR-08 | The customer can pay for a booking (simulated payment) | Customer |
| FR-09 | The system issues an e-ticket after successful payment | System |
| FR-10 | The customer can view their bookings | Customer |
| FR-11 | The customer can cancel a booking | Customer |
| FR-12 | The system calculates a refund on cancellation | System |
| FR-13 | The system sends a booking confirmation notification (simulated) | System |
| FR-14 | The admin can add, edit, and delete flights | Admin |
| FR-15 | The admin can manage airports and aircraft | Admin |

## Non-Functional Requirements (كيف بيشتغل النظام)

| ID | Requirement |
|----|-------------|
| NFR-01 | Passwords must be stored hashed, not as plain text |
| NFR-02 | Search results should appear within 3 seconds |
| NFR-03 | The interface should work on desktop and mobile browsers |
| NFR-04 | Only admins can access flight management pages |

## Assumptions (افتراضاتنا)

- Payment is simulated, no real payment gateway.
- Notifications are simulated (printed or saved, not real emails).
- Refund policy (example): full refund if cancelled 48+ hours before departure, 50% otherwise.
