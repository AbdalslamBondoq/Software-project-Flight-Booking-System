# Project Description – Flight Booking System (Group 17)

## 1. Project Overview

The Flight Booking System is a web application that allows customers to search for flights, reserve seats, and manage their bookings. It also allows airline staff to maintain flight information, airports, and aircraft.

## 2. Project Goal

The main goal is to develop a web application that simplifies the flight booking process and provides an organized way to manage flight reservations and airline information.

## 3. Problem Definition

Booking flights and managing reservations can be time-consuming and may lead to errors, especially when multiple customers attempt to reserve the same seat.

The system aims to organize flight searching and booking while maintaining consistent seat availability and preventing duplicate seat reservations.

## 4. Stakeholders

### 4.1 Customers
Customers use the system to:
- Search for available flights.
- Reserve flight seats.
- Manage their bookings.

### 4.2 Airline Staff / Administrators
Airline staff use the system to:
- Maintain flight information.
- Manage airport information.
- Maintain aircraft information.

## 5. Project Scope

### 5.1 In Scope
- Flight searching.
- Displaying available flights.
- Seat reservation.
- Booking management.
- Flight information management.
- Airport management.
- Aircraft management.
- Simulated payment processing.
- Simulated notifications.

### 5.2 Out of Scope
- Real payment gateway integration.
- Real notification delivery services.
- Integration with external airline systems.
- Real-world payment processing.

## 6. Main Engineering Challenge

The main engineering challenge is maintaining consistent seat reservations.

The system must prevent the same seat on the same flight from being reserved by two different customers, including when reservation attempts happen simultaneously.

## 7. Assumptions

- Flight information is maintained by airline staff.
- Customers use the application to search for and reserve flights.
- Payment processing is simulated.
- Notifications are simulated.
- Each flight has defined seats available for reservation.

## 8. Constraints

- The application will be developed as a web application.
- External payment and notification services will not be integrated.
- Development will follow the required incremental development approach.
- The project will use an Agentic AI development workflow.

## 9. Related Documentation

- System requirements: `requirements.md`
- Incremental development plan: `incremental_development_plan.md`
- System architecture: `architecture.md`
- UML diagrams: `uml/`
