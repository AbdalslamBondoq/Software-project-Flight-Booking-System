# Use Case Descriptions - Flight Booking System (Group 17)

## 1. Introduction

This document provides detailed descriptions of the main use cases of the Flight Booking System. It explains how customers, airline administrators, and system managers interact with the system.

The descriptions are based on the Use Case Diagram and the functional requirements of the project.

## 2. Actors

| Actor | Description |
|---|---|
| Customer | Registers, logs in, searches for flights, selects seats, creates bookings, completes simulated payments, and manages reservations. |
| Airline Administrator | Manages flights, airports, and aircraft information. |
| System Manager | Creates and configures administrator accounts in advance. |

## 3. Use Case Descriptions

### UC-01: Register Account

| Field | Description |
|---|---|
| Use Case ID | UC-01 |
| Use Case Name | Register Account |
| Primary Actor | Customer |
| Description | Allows a new customer to create an account in the system. |
| Preconditions | The customer does not already have an account. |
| Trigger | The customer selects the registration option. |
| Main Flow | 1. The customer opens the registration page. 2. The customer enters the required information. 3. The system validates the submitted information. 4. The system checks whether the account already exists. 5. The system securely hashes the password. 6. The system creates the customer account. 7. The system displays a registration success message. |
| Alternative Flow | If required information is missing or invalid, the system displays an error message. If the account already exists, the system asks the customer to use another email address. |
| Postconditions | A new customer account is stored successfully. |

### UC-02: Log In / Log Out

| Field | Description |
|---|---|
| Use Case ID | UC-02 |
| Use Case Name | Log In / Log Out |
| Primary Actor | Customer, Airline Administrator, System Manager |
| Description | Allows registered customers, authorized administrators, and the System Manager to access or leave their accounts. |
| Preconditions | The user has an existing account. |
| Trigger | The user selects the login or logout option. |
| Main Flow | 1. The user opens the login page. 2. The user enters their email and password. 3. The system validates the credentials. 4. The system identifies the user's role. 5. The system grants access to the appropriate pages. 6. When logging out, the user selects the logout option. 7. The system ends the session. |
| Alternative Flow | If the credentials are incorrect, the system displays an error message and denies access. |
| Postconditions | The user is logged in or their session is terminated. |

### UC-03: Search Flights

| Field | Description |
|---|---|
| Use Case ID | UC-03 |
| Use Case Name | Search Flights |
| Primary Actor | Customer |
| Description | Allows customers to find flights using their travel details. |
| Preconditions | The flight search functionality is available. |
| Trigger | The customer submits a flight search. |
| Main Flow | 1. The customer opens the flight search page. 2. The customer enters the origin, destination, and travel date. 3. The system validates the search information. 4. The system searches available flights. 5. The system displays matching results. |
| Alternative Flow | If no flights match the search criteria, the system displays a message indicating that no flights were found. |
| Postconditions | Matching flights are displayed to the customer. |

### UC-04: Filter and Sort Results

| Field | Description |
|---|---|
| Use Case ID | UC-04 |
| Use Case Name | Filter and Sort Results |
| Primary Actor | Customer |
| Description | Allows customers to filter and sort flight search results by price and time. |
| Preconditions | Flight search results are available. |
| Trigger | The customer selects a filter or sorting option. |
| Main Flow | 1. The customer views the search results. 2. The customer selects a filtering or sorting option. 3. The system applies the selected option. 4. The system displays the updated results. |
| Alternative Flow | If no flights match the selected filter, the system displays an appropriate message. |
| Postconditions | Flight results are displayed according to the selected criteria. |

### UC-05: View Available Seats

| Field | Description |
|---|---|
| Use Case ID | UC-05 |
| Use Case Name | View Available Seats |
| Primary Actor | Customer |
| Description | Allows customers to view the available seats for a selected flight. |
| Preconditions | The customer has selected a flight. |
| Trigger | The customer opens the seat selection page. |
| Main Flow | 1. The customer selects a flight. 2. The system retrieves the seats associated with that flight. 3. The system checks their current availability. 4. The system displays available, held, and booked seats. |
| Alternative Flow | If seat information cannot be retrieved, the system displays an error message. |
| Postconditions | The customer can view the current seat availability. |

### UC-06: Select Seat

| Field | Description |
|---|---|
| Use Case ID | UC-06 |
| Use Case Name | Select Seat |
| Primary Actor | Customer |
| Description | Allows a customer to select an available seat on a chosen flight. |
| Preconditions | The customer has selected a flight and available seats are displayed. |
| Trigger | The customer selects a seat. |
| Main Flow | 1. The customer views available seats. 2. The customer selects a seat. 3. The system checks the seat's current availability. 4. The system allows the customer to proceed with booking. |
| Alternative Flow | If the seat is no longer available, the system displays a message and asks the customer to select another seat. |
| Postconditions | A valid seat is selected for the booking process. |

### UC-07: Create Booking

| Field | Description |
|---|---|
| Use Case ID | UC-07 |
| Use Case Name | Create Booking |
| Primary Actor | Customer |
| Description | Creates a pending booking for a selected flight and seat. |
| Preconditions | The customer is logged in and has selected an available seat. |
| Trigger | The customer confirms the booking request. |
| Main Flow | 1. The customer confirms the selected flight and seat. 2. The system verifies that the seat is still available. 3. The system creates a pending booking. 4. The system records the booking details. 5. The system holds the selected seat for 10 minutes. 6. The system displays the booking status and payment option. |
| Alternative Flow | If the seat is unavailable, the system rejects the booking request and asks the customer to select another seat. |
| Postconditions | A pending booking is created and the selected seat is temporarily held. |

### UC-08: Hold Seat for 10 Minutes

| Field | Description |
|---|---|
| Use Case ID | UC-08 |
| Use Case Name | Hold Seat for 10 Minutes |
| Primary Actor | Flight Booking System |
| Description | Temporarily reserves a selected seat while the customer completes payment. |
| Preconditions | A valid pending booking has been created and the seat is available. |
| Trigger | The system creates a pending booking. |
| Main Flow | 1. The system marks the selected seat as held. 2. The system records the hold expiration time. 3. The system allows the customer to complete payment within 10 minutes. 4. If payment is completed successfully while the hold is active, the booking can be confirmed. |
| Alternative Flow | If the 10-minute period expires before successful payment, the system expires the pending booking and releases the seat. |
| Postconditions | The seat remains held until payment succeeds or the hold expires. |

### UC-09: Complete Simulated Payment

| Field | Description |
|---|---|
| Use Case ID | UC-09 |
| Use Case Name | Complete Simulated Payment |
| Primary Actor | Customer |
| Description | The customer pays for a pending booking through simulated payment processing. |
| Preconditions | The customer is logged in, owns the pending booking, and has an active seat hold for that booking. |
| Trigger | The customer confirms the simulated payment for the displayed booking amount. |
| Main Flow | 1. The system verifies that the booking is pending and still holds the selected seat. 2. The system processes the simulated payment. 3. When payment succeeds, the system checks the hold again. 4. If the hold is still active and belongs to this booking, the system confirms the booking and marks the seat as booked in one transaction. 5. The system generates the e-ticket (UC-10) and records the simulated booking confirmation (UC-11). |
| Alternative Flow — Payment Failure | If payment fails while the hold is active, the system marks the booking as CANCELLED, releases its seat, and displays a payment failure message. |
| Alternative Flow — Hold Expiration | If the hold expires before or during payment processing, the booking becomes EXPIRED and its seat hold is released. The system displays an expiration message and does not issue an e-ticket. |
| Postconditions | On success, the booking is CONFIRMED and the seat is BOOKED. On payment failure, the booking is CANCELLED. On timeout, the booking is EXPIRED. |
| Related Use Cases | In the use case diagram, **Confirm Booking** extends **Complete Simulated Payment** when payment succeeds and the hold is still active. **Confirm Booking** includes **Generate E-ticket** (UC-10) and **Record Booking Confirmation** (UC-11). |

### UC-10: Generate E-ticket

| Field | Description |
|---|---|
| Use Case ID | UC-10 |
| Use Case Name | Generate E-ticket |
| Primary Actor | Flight Booking System |
| Description | Generates an electronic ticket for a successfully confirmed booking. |
| Preconditions | The booking is confirmed after successful simulated payment. |
| Trigger | The system successfully confirms a booking. |
| Main Flow | 1. The system retrieves the confirmed booking details. 2. The system generates a unique ticket. 3. The system stores the ticket information. 4. The system makes the e-ticket available to the customer. |
| Alternative Flow | If ticket generation fails, the system records the error for handling and does not display an invalid ticket. |
| Postconditions | An e-ticket is stored and associated with the confirmed booking. |

### UC-11: Record Booking Confirmation

| Field | Description |
|---|---|
| Use Case ID | UC-11 |
| Use Case Name | Record Booking Confirmation |
| Primary Actor | Flight Booking System |
| Description | Records a simulated booking confirmation after successful payment. |
| Preconditions | The booking has been successfully confirmed. |
| Trigger | The system confirms a booking. |
| Main Flow | 1. The system retrieves the booking details. 2. The system creates a confirmation notification. 3. The system records the notification. 4. The confirmation can be viewed or saved by the customer. |
| Alternative Flow | If the notification cannot be recorded, the system logs the error without changing the confirmed booking status. |
| Postconditions | A simulated booking confirmation is recorded. |

### UC-12: View My Bookings

| Field | Description |
|---|---|
| Use Case ID | UC-12 |
| Use Case Name | View My Bookings |
| Primary Actor | Customer |
| Description | Allows customers to view their existing bookings. |
| Preconditions | The customer is logged in. |
| Trigger | The customer opens the bookings page. |
| Main Flow | 1. The customer opens My Bookings. 2. The system retrieves bookings belonging to the logged-in customer. 3. The system displays booking details and statuses. |
| Alternative Flow | If the customer has no bookings, the system displays an appropriate message. |
| Postconditions | The customer's bookings are displayed. |

### UC-13: Cancel Booking

| Field | Description |
|---|---|
| Use Case ID | UC-13 |
| Use Case Name | Cancel Booking |
| Primary Actor | Customer |
| Description | Allows customers to cancel an eligible confirmed booking according to the cancellation policy. |
| Preconditions | The customer is logged in and owns the booking. The booking is eligible for cancellation. |
| Trigger | The customer selects the cancellation option. |
| Main Flow | 1. The customer opens My Bookings. 2. The customer selects a booking. 3. The system displays the booking details and cancellation information. 4. The customer confirms cancellation. 5. The system checks the cancellation policy. 6. The system updates the booking status to cancelled. 7. The system releases the seat. 8. The system processes the applicable refund calculation. |
| Alternative Flow | If the booking cannot be cancelled, the system displays a message explaining that cancellation is unavailable. |
| Postconditions | The booking is cancelled and the seat is released. The applicable refund amount is determined. |

### UC-14: Calculate Refund

| Field | Description |
|---|---|
| Use Case ID | UC-14 |
| Use Case Name | Calculate Refund |
| Primary Actor | Flight Booking System |
| Description | Calculates the refund amount according to the booking cancellation policy. |
| Preconditions | A valid booking cancellation request has been accepted. |
| Trigger | The system processes a booking cancellation. |
| Main Flow | 1. The system retrieves the booking amount and flight departure date. 2. The system calculates the time remaining until departure. 3. If cancellation occurs 14 or more days before departure, the system calculates a 50% refund. 4. If cancellation occurs less than 14 days before departure, the refund is zero. 5. The system records the calculated refund amount. |
| Alternative Flow | If booking or departure information is unavailable, the system cannot calculate the refund and records an error. |
| Postconditions | The refund amount is calculated and stored. |

### UC-15: Manage Flights

| Field | Description |
|---|---|
| Use Case ID | UC-15 |
| Use Case Name | Manage Flights |
| Primary Actor | Airline Administrator |
| Description | Allows authorized administrators to add, edit, and delete flight information. |
| Preconditions | The administrator is logged in and authorized. |
| Trigger | The administrator opens flight management. |
| Main Flow | 1. The administrator opens the flight management page. 2. The system displays existing flights. 3. The administrator selects an operation. 4. The administrator enters or updates flight information. 5. The system validates the information. 6. The system saves the changes. |
| Alternative Flow | If the information is invalid, the system displays validation errors. Unauthorized users are denied access. |
| Postconditions | Flight information is updated successfully. |

### UC-16: Manage Airports

| Field | Description |
|---|---|
| Use Case ID | UC-16 |
| Use Case Name | Manage Airports |
| Primary Actor | Airline Administrator |
| Description | Allows authorized administrators to manage airport information. |
| Preconditions | The administrator is logged in and authorized. |
| Trigger | The administrator opens airport management. |
| Main Flow | 1. The administrator opens airport management. 2. The system displays existing airports. 3. The administrator adds, edits, or deletes airport information. 4. The system validates the submitted information. 5. The system saves the changes. |
| Alternative Flow | If the information is invalid or an airport cannot be deleted because it is referenced by existing flights, the system displays an appropriate message. |
| Postconditions | Airport information is updated successfully. |

### UC-17: Manage Aircraft

| Field | Description |
|---|---|
| Use Case ID | UC-17 |
| Use Case Name | Manage Aircraft |
| Primary Actor | Airline Administrator |
| Description | Allows authorized administrators to manage aircraft information. |
| Preconditions | The administrator is logged in and authorized. |
| Trigger | The administrator opens aircraft management. |
| Main Flow | 1. The administrator opens aircraft management. 2. The system displays existing aircraft. 3. The administrator adds, edits, or deletes aircraft information. 4. The system validates the submitted information. 5. The system saves the changes. |
| Alternative Flow | If the information is invalid or an aircraft is referenced by existing flights, the system displays an appropriate message. |
| Postconditions | Aircraft information is updated successfully. |

### UC-18: Create Administrator Accounts

| Field | Description |
|---|---|
| Use Case ID | UC-18 |
| Use Case Name | Create Administrator Accounts |
| Primary Actor | System Manager |
| Description | Allows the System Manager to create and configure administrator accounts in advance. |
| Preconditions | The System Manager has authorized access to the account provisioning function. |
| Trigger | The System Manager requests creation of an administrator account. |
| Main Flow | 1. The System Manager opens the administrator account provisioning function. 2. The System Manager enters the required administrator information. 3. The system validates the information. 4. The system checks whether the account already exists. 5. The system creates the administrator account and securely stores the password hash. 6. The system confirms successful account creation. |
| Alternative Flow | If the information is invalid or the account already exists, the system displays an error message. |
| Postconditions | A new administrator account is created and can be used to access authorized administrative functions. |

### UC-19: Confirm Booking

| Field | Description |
|---|---|
| Use Case ID | UC-19 |
| Use Case Name | Confirm Booking |
| Primary Actor | System |
| Description | Confirms a pending booking after a successful simulated payment while the seat hold is still active. |
| Preconditions | A PENDING booking exists, the simulated payment for it succeeded, and the booking still owns an active seat hold. |
| Trigger | The simulated payment in UC-09 returns a successful result. |
| Main Flow | 1. The system checks that the booking is still PENDING and that its seat hold has not expired. 2. In one database transaction, the system marks the booking as CONFIRMED and the seat as BOOKED. 3. The system generates the e-ticket (UC-10). 4. The system records the simulated booking confirmation (UC-11). 5. The system displays the confirmation and e-ticket to the customer. |
| Alternative Flow | If the seat hold has expired, the booking becomes EXPIRED, the seat is released, and no e-ticket or confirmation is created. |
| Postconditions | The booking is CONFIRMED, the seat is BOOKED, and the e-ticket and confirmation notification are stored. |
| Related Use Cases | Extends UC-09 Complete Simulated Payment when payment succeeds and the hold is active. Includes UC-10 Generate E-ticket and UC-11 Record Booking Confirmation. |

## 4. General Business Rules

1. Only customers can register through the public registration interface.
2. Administrator accounts are created in advance by the System Manager.
3. Public administrator registration is not allowed.
4. Only authorized administrators can access administrative management functions.
5. Customers search for flights using origin, destination, and travel date.
6. A selected seat is held for 10 minutes.
7. A held or booked seat cannot be selected by another customer.
8. A pending booking is confirmed only after successful payment while the seat hold is active.
9. If payment fails or the hold expires, the pending booking is not confirmed and the seat is released.
10. An e-ticket is generated only after successful booking confirmation.
11. Booking confirmation notifications are simulated and recorded by the system.
12. Cancellations made 14 or more days before departure receive a 50% refund.
13. Cancellations made less than 14 days before departure receive no refund.
14. Payment processing is simulated and does not use a real payment gateway.
15. Booking confirmations are simulated and are not sent as real emails.

## 5. Related Documentation

- Project Description: `docs/project_description.md`
- Requirements: `docs/requirements.md`
- Architecture: `docs/architecture.md`
- Incremental Development Plan: `docs/incremental_development_plan.md`
- Traceability Matrix: `docs/traceability_matrix.md`
- Use Case Diagram: `uml/use_case_diagram.md`
- C4 Context Diagram: `uml/c4_context.md`
- C4 Container Diagram: `uml/c4_container.md`
- Component Diagram: `uml/component_diagram.md`
- Class Diagram: `uml/class_diagram.md`
- Sequence Diagram: `uml/sequence_booking.md`
- State Diagram: `uml/state_booking.md`
- Activity Diagram: `uml/activity_booking.md`
- Entity Relationship Diagram: `uml/erd.md`
