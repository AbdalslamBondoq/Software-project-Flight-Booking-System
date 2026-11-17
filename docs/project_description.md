# Project Description – Flight Booking System (Group 17)

## 1. Project Overview

The Flight Booking System is a web application that allows customers to register, log in, search for flights, reserve seats, complete simulated payments, and manage their bookings. It also allows airline administrators to manage flight information, airports, and aircraft.

## 2. Project Goal

The main goal is to develop a web application that simplifies the flight booking process, provides an organized way to manage flight reservations and airline information, and ensures consistent seat availability.

## 3. Problem Definition

Booking flights and managing reservations can be time-consuming and may lead to errors, especially when multiple customers attempt to reserve the same seat simultaneously.

The system aims to organize flight searching and booking while maintaining consistent seat availability and preventing duplicate seat reservations.

## 4. Stakeholders

### 4.1 Customers

Customers use the system to:
- Register and log in to their accounts.
- Search for available flights by origin, destination, and date.
- Filter and sort flight search results.
- View available seats.
- Select and reserve flight seats.
- Complete simulated payments.
- View and manage their bookings.
- Cancel bookings according to the cancellation policy.
- Receive booking confirmations and e-tickets.

### 4.2 Airline Administrators

Airline administrators are responsible for maintaining the system's flight data. They can:
- Log in to the administrative area.
- Add, edit, and delete flights.
- Manage airport information.
- Manage aircraft information.

Administrative functions are restricted to authorized administrators.

### 4.3 System Responsibilities

The system is responsible for:
- Preventing two customers from booking the same seat on the same flight.
- Holding selected seats for 10 minutes until payment is completed or the hold expires.
- Releasing seats automatically when their reservation hold expires.
- Issuing e-tickets after successful payment.
- Calculating refunds according to the cancellation policy.
- Generating simulated booking confirmation notifications.

## 5. Project Scope

### 5.1 In Scope

- Customer registration and authentication.
- Flight searching and displaying available flights.
- Filtering and sorting flight search results.
- Viewing available seats.
- Seat reservation and temporary seat holding.
- Simulated payment processing.
- E-ticket generation.
- Booking management and cancellation.
- Refund calculation.
- Simulated booking notifications.
- Flight information management.
- Airport management.
- Aircraft management.
- Administrator access control.

### 5.2 Out of Scope

- Real payment gateway integration.
- Real notification delivery services.
- Integration with external airline systems.
- Real-world payment processing.

## 6. Main Engineering Challenge

The main engineering challenge is maintaining consistent seat reservations and preventing double booking.

The system must ensure that the same seat on the same flight cannot be booked by two different customers, including when reservation attempts happen simultaneously.

To achieve this, a selected seat will be held for 10 minutes. If payment is not completed within this period, the hold expires and the seat becomes available again.

## 7. Assumptions

- Flight information is maintained by airline administrators.
- Customers use the application to search for and reserve flights.
- Each flight has defined seats available for reservation.
- Payment processing is simulated, with no real payment gateway.
- Notifications are simulated and may be printed or saved.
- A booking cancelled 14 or more days before departure receives a 50% refund.
- A booking cancelled less than 14 days before departure receives no refund.
- Selected seats are held for 10 minutes until payment is completed or the hold expires.

## 8. Constraints

- The application will be developed as a web application.
- The interface must support desktop and mobile browsers.
- Search results should appear within 3 seconds.
- Passwords must be stored using hashing rather than plain text.
- Only authorized administrators can access flight management pages.
- External payment and notification services will not be integrated.
- Development will follow the required incremental development approach.
- The project will use an Agentic AI development workflow.

## 9. Related Documentation

- System requirements: `requirements.md`
- Incremental development plan: `incremental_development_plan.md`
- System architecture: `architecture.md`
- UML diagrams: `uml/`
