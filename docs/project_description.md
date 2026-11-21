Flight Booking System (Group 17)
# Project Description 



## 1. Project Overview

The Flight Booking System is a web application that allows customers to register, log in, search for flights, reserve seats, complete simulated payments, and manage their bookings. Airline administrators manage flights, airports, and aircraft.

The System Manager creates and configures airline administrator accounts in advance. Public registration is available only to customers.





## 2. Project Goal

The goal is to simplify flight booking for customers, give airline administrators a central place to maintain flight information, and keep seat availability accurate throughout the booking process.




## 3. Problem Definition

Booking flights and managing reservations can be time-consuming and may lead to errors. For example, two customers may see the same seat as available and try to reserve it at the same time.

The system must ensure that only one customer can hold or book a given seat on a flight at a time. It must also make the seat available again when a payment fails, a hold expires, or a customer cancels a confirmed booking before departure.




## 4. Stakeholders

### 4.1 Customers

Customers use the system to:

- Register and log in to their accounts.
- Search for flights by origin, destination, and travel date.
- Filter and sort search results by price and time.
- View available seats and select a seat for a flight.
- Create a booking and complete a simulated payment.
- View their bookings, booking confirmations, and e-tickets.
- Cancel their own confirmed bookings before departure according to the cancellation policy.

### 4.2 Airline Administrators

Airline administrators use accounts provided by the System Manager to:

- Log in to the administrative area.
- Add, edit, and delete flights.
- Manage airport information.
- Manage aircraft information.

### 4.3 System Manager

The System Manager creates and configures airline administrator accounts in advance. Only the System Manager can provision these accounts.

### 4.4 System Responsibilities

The system is responsible for:

- Preventing multiple active bookings for the same seat on the same flight.
- Holding the selected seat for 10 minutes when a `PENDING` booking is created.
- Marking the booking as `CONFIRMED` and the seat as `BOOKED` when simulated payment succeeds while the hold is active.
- Issuing an e-ticket and recording a simulated notification after booking confirmation.
- Marking the pending booking as `CANCELLED` and releasing the seat if payment fails while the hold is active.
- Marking the pending booking as `EXPIRED` and releasing the seat if the hold expires before confirmation.
- Releasing the seat and calculating the applicable refund when a customer cancels a confirmed booking before departure.





## 5. Project Scope

### 5.1 In Scope

- Customer registration, login, and logout.
- Creation and configuration of airline administrator accounts by the System Manager.
- Flight search by origin, destination, and travel date.
- Filtering and sorting search results by price and time.
- Seat availability checks, seat selection, and 10-minute seat holds.
- Booking creation and simulated payment processing.
- Booking confirmation, e-ticket generation, and simulated notifications.
- Viewing and cancelling bookings and calculating refunds.
- Management of flights, airports, and aircraft by authorized airline administrators.
- Role-based access control.

### 5.2 Out of Scope

- Real payment processing and integration with payment gateways.
- Delivery of notifications through external email or messaging services.
- Integration with external airline systems.





## 6. Main Engineering Challenge

Two customers may select the same seat before either customer's screen shows an updated seat map. To prevent double booking, the backend checks seat availability, creates the pending booking, and places the hold in one database transaction. Only one request can acquire the seat. If the seat is already held or booked, the other customer is asked to choose another seat.

The 10-minute hold also creates a timing issue during payment. Before confirming the booking, the backend checks that the booking is still pending and that its hold is still active. It confirms the booking and marks the seat as booked in one transaction. A payment result received after the hold expires cannot confirm the expired booking.





## 7. Assumptions

- Airline administrators maintain flight, airport, and aircraft information.
- Customers use the application to search for flights and reserve seats.
- Each flight has a defined set of seats available for reservation.
- Payment and refund processing are simulated.
- Booking confirmation notifications are simulated and may be viewed, printed, or saved.
- Customers may cancel their own confirmed bookings before departure.
- Cancellation at least 14 days before departure results in a refund of 50% of the amount paid.
- Cancellation less than 14 days before departure results in no refund.





## 8. Constraints

- The application will be developed as a web application.
- The interface must support desktop and mobile browsers.
- Search results should appear within 3 seconds.
- The system must store passwords as secure hashes.
- Only authorized airline administrators can manage flights, airports, and aircraft.
- Only the System Manager can create and configure administrator accounts.
- Payment processing and booking notifications must operate without external payment or notification services.
- Development will follow the required incremental development approach.
- The project will use an Agentic AI development workflow.




## 9. Related Documentation

- [System Requirements](requirements.md)
- [Incremental Development Plan](incremental_development_plan.md)
- [System Architecture](architecture.md)
- [UML Diagrams](../uml/)
