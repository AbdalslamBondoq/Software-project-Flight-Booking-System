# Deployment Diagram - Flight Booking System

## 1. Overview

This document describes the physical deployment architecture of the Flight Booking System, including the hardware nodes, software components, and communication between them.

The system uses a web-based three-tier architecture consisting of a client layer, an application layer, and a database layer.

## 2. Deployment Diagram

```mermaid
flowchart TB
    subgraph Client["Client Device"]
        Browser["Web Browser"]
        UI["Flight Booking Web Interface<br/>HTML, CSS, JavaScript"]
        Browser --> UI
    end

    subgraph Server["Application Server"]
        FastAPI["FastAPI Backend Application<br/>API Routes"]

        Auth["Authentication"]
        Access["Role-Based Access Control"]
        Accounts["Admin Account Management"]
        Search["Flight Search"]
        FlightAdmin["Flight Management"]
        Booking["Booking Management"]
        Seats["Seat Availability and Holding"]
        Cancellation["Cancellation and Refund Calculation"]
        Payment["Simulated Payment Processing"]
        Ticket["E-ticket Generation"]
        Notification["Simulated Booking Confirmation"]

        FastAPI --> Auth
        FastAPI --> Access
        FastAPI --> Search
        Access --> Accounts
        Access --> FlightAdmin
        Access --> Booking
        Booking --> Seats
        Booking --> Payment
        Booking --> Ticket
        Booking --> Notification
        Booking --> Cancellation
        Cancellation --> Payment
        Cancellation --> Seats

        DB[("SQLite database file<br/>flight_booking.db")]
    end

    UI <-->|HTTPS Requests and Responses| FastAPI
    FastAPI <-->|SQL queries through the Python SQLite driver| DB
```

## 3. Deployment Nodes

| Node | Description |
|---|---|
| Client Device | The user's computer or mobile device used to access the system. |
| Web Browser | Runs the web application interface. |
| Web Interface | Built using HTML, CSS, and JavaScript. |
| Application Server | Hosts and runs the Python FastAPI backend. |
| FastAPI Backend | Handles requests, business logic, authentication, and communication with the database. |
| SQLite database file | A single database file stored on the application server and accessed by the backend. Stores users, airports, aircraft, flights, seats, bookings, payments, tickets, and notifications. |

## 4. Software Components

The modules below are the components of the [Component Diagram](component_diagram.md), all deployed inside the FastAPI backend on the application server.

- **Authentication:** Registers customers, hashes passwords, validates login credentials, and ends user sessions on logout.
- **Role-Based Access Control:** Checks the authenticated user's role before allowing a protected operation.
- **Admin Account Management:** Allows the System Manager to create and configure administrator accounts.
- **Flight Search:** Finds flights by origin, destination, and date, and supports filtering and sorting by price and time.
- **Flight Management:** Allows airline administrators to manage flights, schedules, airports, and aircraft.
- **Booking Management:** Creates pending bookings, retrieves the customer's own bookings, and coordinates payment, confirmation, ticket issuance, and cancellation.
- **Seat Availability and Holding:** Displays seat availability, manages 10-minute holds, and releases seats when a hold expires or a booking is cancelled.
- **Cancellation and Refund Calculation:** Checks booking ownership and cancellation eligibility, calculates the refund, and coordinates seat release.
- **Simulated Payment Processing:** Produces a simulated payment result, records the transaction, and processes eligible simulated refunds.
- **E-ticket Generation:** Generates a unique e-ticket for a confirmed booking and stores it in the database.
- **Simulated Booking Confirmation:** Records a confirmation message after the booking is confirmed.

## 5. Communication Between Nodes

1. The customer accesses the system through a web browser.
2. The web interface sends requests to the FastAPI backend through HTTPS.
3. The backend processes requests and applies the required business rules.
4. The backend communicates with the SQLite database to retrieve or update information.
5. The Simulated Payment Processing component processes payment requests internally.
6. The Simulated Booking Confirmation component records the booking confirmation.
7. The backend returns the appropriate response to the web interface.

## 6. Deployment Considerations

- The system follows a three-tier architecture.
- The frontend communicates with the backend through HTTPS in the deployment environment.
- HTTP may be used during local development.
- The frontend does not access the database directly.
- The backend is responsible for all business logic and database access.
- SQLite stores the system's persistent data in a single file on the application server. SQLite is an embedded database, so it does not run on a separate database server.
- Passwords must be stored as secure hashes.
- Seat reservations expire automatically after 10 minutes if payment is not completed.
- Payment and notification services are simulated internal modules.
- No real external payment gateway or email service is required.

## 7. Related Documents

- `architecture.md`
- `project_description.md`
- `requirements.md`
- `component_diagram.md`
- `sequence_booking.md`
- `class_diagram.md`
- `erd.md`
