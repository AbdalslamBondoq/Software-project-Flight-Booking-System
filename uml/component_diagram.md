# Component Diagram - Flight Booking System (Group 17)

## 1. Overview

This diagram illustrates the main software components of the Flight Booking System and how they interact.

The system follows a layered architecture consisting of three main layers:

- **Web Application:** Provides interfaces for customers, airline administrators, and the system manager.
- **Backend API:** Handles authentication, flight management, booking operations, seat availability, payments, cancellations, and notifications.
- **Database:** Stores users, flights, airports, aircraft, seats, bookings, payments, tickets, and notifications.

The system also includes simulated external payment and notification services.

## 2. Component Diagram

```mermaid
flowchart LR

    %% ACTORS
    subgraph Actors["System Actors"]
        direction TB
        Customer["Customer"]
        Admin["Airline Administrator"]
        Manager["System Manager"]
    end

    %% WEB APPLICATION
    subgraph Web["Web Application"]
        direction TB
        AuthUI["Authentication Interface"]
        SearchUI["Flight Search Interface"]
        SeatUI["Booking and Seat Selection Interface"]
        BookingUI["My Bookings and Cancellation Interface"]
        PaymentUI["Payment Interface"]
        AdminUI["Administration Interface"]
        AccountUI["Admin Account Management Interface"]
    end

    %% BACKEND API
    subgraph API["Backend API - FastAPI"]
        direction TB

        subgraph Identity["Identity and Access"]
            direction LR
            Auth["Authentication Component"]
            Access["Role-Based Access Control"]
            AdminAccount["Admin Account Management Component"]
        end

        subgraph FlightServices["Flight Services"]
            direction LR
            Search["Flight Search Component"]
            Flight["Flight Management Component"]
        end

        subgraph BookingServices["Booking Services"]
            direction LR
            Seat["Seat Availability and Holding Component"]
            Booking["Booking Management Component"]
            Cancellation["Cancellation and Refund Component"]
        end

        subgraph PaymentServices["Payment and Notifications"]
            direction LR
            Payment["Payment Processing Component"]
            Ticket["E-ticket Generation Component"]
            Notification["Notification Component"]
        end
    end

    %% DATABASE
    subgraph DB["SQLite Database"]
        direction TB
        UsersDB[("Users")]
        FlightsDB[("Flights, Airports and Aircraft")]
        SeatsDB[("Seats")]
        BookingsDB[("Bookings and Seat Holds")]
        PaymentsDB[("Payments, Refunds and Tickets")]
        NotificationsDB[("Notifications")]
    end

    %% EXTERNAL SERVICES
    subgraph External["Simulated External Services"]
        direction TB
        SimPayment["Simulated Payment Service"]
        SimNotification["Simulated Notification Service"]
    end

    %% ACTOR INTERACTIONS
    Customer --> AuthUI
    Customer --> SearchUI
    Customer --> SeatUI
    Customer --> BookingUI
    Customer --> PaymentUI

    Admin --> AuthUI
    Admin --> AdminUI
    Manager --> AccountUI

    %% WEB TO BACKEND
    AuthUI --> Auth
    SearchUI --> Search
    SeatUI --> Seat
    SeatUI --> Booking
    BookingUI --> Booking
    BookingUI --> Cancellation
    PaymentUI --> Payment
    AdminUI --> Access
    AdminUI --> Flight
    AccountUI --> AdminAccount

    %% IDENTITY AND ACCESS
    Auth --> UsersDB
    Access --> UsersDB
    AdminAccount --> UsersDB
    Access --> Flight
    Access --> AdminAccount

    %% FLIGHT SERVICES
    Flight --> FlightsDB
    Search --> FlightsDB
    Search --> SeatsDB

    %% BOOKING SERVICES
    Seat --> SeatsDB
    Seat --> BookingsDB
    Booking --> BookingsDB
    Booking --> SeatsDB
    Booking --> Notification

    %% PAYMENT AND TICKETS
    Payment --> SimPayment
    Payment --> PaymentsDB
    Payment --> BookingsDB
    Payment --> Ticket
    Ticket --> PaymentsDB
    Ticket --> Notification

    %% CANCELLATION AND REFUNDS
    Cancellation --> BookingsDB
    Cancellation --> PaymentsDB
    Cancellation --> SimPayment

    %% NOTIFICATIONS
    Notification --> SimNotification
    Notification --> NotificationsDB

    %% SEAT HOLD EXPIRATION
    HoldRule["10-minute seat hold<br/>Automatic expiration and release"]
    HoldRule -.-> Seat

    %% STYLING
    classDef actor fill:#08427b,stroke:#052e56,color:#fff
    classDef ui fill:#438dd5,stroke:#2e6295,color:#fff
    classDef backend fill:#1168bd,stroke:#0b4884,color:#fff
    classDef database fill:#287a45,stroke:#17552d,color:#fff
    classDef external fill:#999999,stroke:#6b6b6b,color:#fff
    classDef rule fill:#8b6914,stroke:#66500e,color:#fff

    class Customer,Admin,Manager actor
    class AuthUI,SearchUI,SeatUI,BookingUI,PaymentUI,AdminUI,AccountUI ui
    class Auth,Access,AdminAccount,Search,Flight,Seat,Booking,Cancellation,Payment,Ticket,Notification backend
    class UsersDB,FlightsDB,SeatsDB,BookingsDB,PaymentsDB,NotificationsDB database
    class SimPayment,SimNotification external
    class HoldRule rule
```

## 3. Main Components

| Component | Responsibility |
|---|---|
| Authentication | Handles customer registration, login, logout, and administrator authentication. |
| Admin Account Management | Allows the system manager to create and configure administrator accounts in advance. |
| Role-Based Access Control | Restricts administrative functions to authorized administrators. |
| Flight Management | Adds, edits, and deletes flights, airports, and aircraft. |
| Flight Search | Searches and filters available flights. |
| Seat Management | Displays seat availability and manages temporary seat holds. |
| Booking Management | Creates and manages customer bookings. |
| Payment Processing | Processes simulated payments. |
| E-ticket Generation | Generates e-tickets after successful payment. |
| Cancellation and Refund | Cancels bookings and calculates refunds according to the cancellation policy. |
| Notification | Generates simulated booking confirmation notifications. |

## 4. Database Components

| Database Component | Stored Information |
|---|---|
| Users | Customer and administrator account information. |
| Flights, Airports and Aircraft | Flight schedules, airport information, and aircraft information. |
| Seats | Seat numbers, availability, and reservation status. |
| Bookings and Seat Holds | Customer bookings and temporary seat reservations. |
| Payments, Refunds and Tickets | Payment records, refund information, and generated e-tickets. |
| Notifications | Simulated booking confirmation notifications. |

## 5. Important Design Rules

- The Web Application communicates with the Backend API.
- The Backend API handles business logic and database operations.
- The Web Application must not access the database directly.
- Passwords must be stored using secure hashing, not as plain text.
- Administrator accounts are created and configured in advance by the System Manager.
- Public administrator registration is not allowed.
- Only authorized administrators can access administrative management functions.
- Seat holds expire automatically after 10 minutes if payment is not completed.
- The same seat on the same flight cannot be booked by two different customers.
- E-tickets are generated only after successful payment.
- A booking cancelled 14 or more days before departure receives a 50% refund.
- A booking cancelled less than 14 days before departure receives no refund.
- Payment and notification services are simulated and do not use real external services.

## 6. Technology Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript |
| Backend | Python, FastAPI |
| Database | SQLite |
| Testing | pytest |
| Development Workflow | Agentic AI (Claude Code) |
| Version Control | Git and GitHub |

## 7. Related Documentation

- Project description: `docs/project_description.md`
- System requirements: `docs/requirements.md`
- System architecture: `docs/architecture.md`
- C4 Context Diagram: `uml/c4_context.md`
- C4 Container Diagram: `uml/c4_container.md`
- Use Case Diagram: `uml/use_case_diagram.md`
- Class Diagram: `uml/class_diagram.md`
- Sequence Diagram: `uml/sequence_booking.md`
- State Diagram: `uml/state_booking.md`
- Entity Relationship Diagram: `uml/erd.md`
