# Use Case Diagram - Flight Booking System (Group 17)

## 1. Overview

This diagram illustrates the interactions between the Flight Booking System and its main actors.

The system has three main actors:

- **Customer:** Registers, logs in, searches for flights, selects seats, creates bookings, completes simulated payments, and manages reservations.
- **Airline Administrator:** Manages flight, airport, and aircraft information.
- **System Manager:** Creates and configures administrator accounts in advance.

Payment processing and booking notifications are simulated internal system functions. They are not external services and do not require integration with third-party systems.

## 2. Use Case Diagram

```mermaid
flowchart LR

    %% ACTORS
    subgraph Actors["Actors"]
        direction TB
        Customer(["Customer"])
        Admin(["Airline Administrator"])
        Manager(["System Manager"])
    end

    %% SYSTEM BOUNDARY
    subgraph System["Flight Booking System"]
        direction TB

        subgraph CustomerCases["Customer Use Cases"]
            direction TB
            UC01(["UC-01 Register Account"])
            UC02(["UC-02 Log In / Log Out"])
            UC03(["UC-03 Search Flights"])
            UC04(["UC-04 Filter and Sort Results"])
            UC05(["UC-05 View Available Seats"])
            UC06(["UC-06 Select Seat"])
            UC07(["UC-07 Create Booking"])
            UC08(["UC-08 Hold Seat for 10 Minutes"])
            UC09(["UC-09 Complete Simulated Payment"])
            UC19(["UC-19 Confirm Booking"])
            UC10(["UC-10 Generate E-ticket"])
            UC11(["UC-11 Record Booking Confirmation"])
            UC12(["UC-12 View My Bookings"])
            UC13(["UC-13 Cancel Booking"])
            UC14(["UC-14 Calculate Refund"])
        end

        subgraph AdminCases["Administration Use Cases"]
            direction TB
            UC15(["UC-15 Manage Flights"])
            UC16(["UC-16 Manage Airports"])
            UC17(["UC-17 Manage Aircraft"])
            UC18(["UC-18 Create Administrator Accounts"])
        end
    end

    %% CUSTOMER ASSOCIATIONS
    Customer --- UC01
    Customer --- UC02
    Customer --- UC03
    Customer --- UC04
    Customer --- UC05
    Customer --- UC06
    Customer --- UC07
    Customer --- UC09
    Customer --- UC12
    Customer --- UC13

    %% ADMIN ASSOCIATIONS
    Admin --- UC02
    Admin --- UC15
    Admin --- UC16
    Admin --- UC17

    %% SYSTEM MANAGER ASSOCIATION
    Manager --- UC18

    %% INCLUDE RELATIONSHIPS
    UC07 -.->|«include»| UC08
    UC13 -.->|«include»| UC14
    UC19 -.->|«include»| UC10
    UC19 -.->|«include»| UC11

    %% EXTEND RELATIONSHIPS
    UC04 -.->|«extend»| UC03
    UC19 -.->|«extend» payment successful and hold active| UC09

    %% STYLING
    classDef actor fill:#08427b,stroke:#052e56,color:#fff
    classDef usecase fill:#438dd5,stroke:#2e6295,color:#fff

    class Customer,Admin,Manager actor
    class UC01,UC02,UC03,UC04,UC05,UC06,UC07,UC08,UC09,UC19,UC10,UC11,UC12,UC13,UC14,UC15,UC16,UC17,UC18 usecase
```

## 3. Actor Descriptions

| Actor | Description |
|---|---|
| Customer | Registers, logs in, searches for flights, selects seats, creates bookings, completes simulated payments, and manages bookings. |
| Airline Administrator | Logs in and manages flights, airports, and aircraft information. |
| System Manager | Creates and configures administrator accounts in advance. |

## 4. Main Use Cases

| Use Case | Description |
|---|---|
| UC-01 Register Account | Allows customers to create new accounts. |
| UC-02 Log In / Log Out | Allows customers and administrators to access and leave their accounts. |
| UC-18 Create Administrator Accounts | Allows the System Manager to create and configure administrator accounts in advance. |
| UC-03 Search Flights | Searches for flights by origin, destination, and date. |
| UC-04 Filter and Sort Results | Allows customers to filter and sort search results by price and time. |
| UC-05 View Available Seats | Displays the available seats for a selected flight. |
| UC-06 Select Seat | Allows customers to select an available seat. |
| UC-07 Create Booking | Creates a pending booking for the selected flight and seat. |
| UC-08 Hold Seat for 10 Minutes | Temporarily holds the selected seat while payment is pending. |
| UC-09 Complete Simulated Payment | Processes a simulated payment for a pending booking. |
| UC-19 Confirm Booking | Confirms the booking when payment succeeds and the seat hold is still active. |
| UC-10 Generate E-ticket | Generates an e-ticket after successful booking confirmation. |
| UC-11 Record Booking Confirmation | Records a simulated booking confirmation notification. |
| UC-12 View My Bookings | Displays the customer's existing bookings. |
| UC-13 Cancel Booking | Allows customers to cancel their bookings according to the cancellation policy. |
| UC-14 Calculate Refund | Calculates the applicable refund according to the cancellation policy. |
| UC-15 Manage Flights | Allows administrators to add, edit, and delete flights. |
| UC-16 Manage Airports | Allows administrators to manage airport information. |
| UC-17 Manage Aircraft | Allows administrators to manage aircraft information. |

## 5. Use Case Relationships

### 5.1 Include Relationships

The `<<include>>` relationship represents behavior that is always performed as part of the base use case.

- **Create Booking** includes **Hold Seat for 10 Minutes** because a selected seat must be held when a pending booking is created.
- **Cancel Booking** includes **Calculate Refund** because the system must calculate the applicable refund when a booking is cancelled.
- **Confirm Booking** includes **Generate E-ticket** because a confirmed booking must have an e-ticket.
- **Confirm Booking** includes **Record Booking Confirmation** because the system records a simulated confirmation after successful booking confirmation.

### 5.2 Extend Relationships

The `<<extend>>` relationship represents optional or conditional behavior.

- **Filter and Sort Results** extends **Search Flights** because customers may optionally filter or sort the search results.
- **Confirm Booking** extends **Complete Simulated Payment** because booking confirmation occurs only when payment succeeds and the seat hold is still active.

## 6. Business Rules

- Only customers can register through the public registration interface.
- Administrator accounts are created in advance by the System Manager.
- Public administrator registration is not allowed.
- Only authorized administrators can access administrative management functions.
- Customers can search flights by origin, destination, and date.
- Search results can be filtered and sorted by price and time.
- A selected seat is held for 10 minutes.
- If payment is not completed within 10 minutes, the hold expires and the seat is released.
- A held or booked seat cannot be reserved by another customer for the same flight.
- A booking is confirmed only if payment succeeds while the seat hold is still active.
- An e-ticket is generated only after successful booking confirmation.
- Booking confirmation notifications are recorded after successful booking confirmation.
- Cancellations made 14 or more days before departure receive a 50% refund.
- Cancellations made less than 14 days before departure receive no refund.
- Payment processing is simulated and does not use a real payment gateway.
- Booking notifications are simulated and are not sent as real emails.

## 7. Related Documentation

- Project Description: `docs/project_description.md`
- Requirements: `docs/requirements.md`
- Incremental Development Plan: `docs/incremental_development_plan.md`
- Traceability Matrix: `docs/traceability_matrix.md`
- Architecture: `docs/architecture.md`
- C4 Context Diagram: `uml/c4_context.md`
- C4 Container Diagram: `uml/c4_container.md`
- Component Diagram: `uml/component_diagram.md`
- Class Diagram: `uml/class_diagram.md`
- Use Case Description: `uml/use_case_description.md`
- Sequence Diagram: `uml/sequence_booking.md`
- State Diagram: `uml/state_booking.md`
- Entity Relationship Diagram: `uml/erd.md`
