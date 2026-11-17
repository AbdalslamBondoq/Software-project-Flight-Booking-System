# Activity Diagram - Flight Booking System

## 1. Overview

This document describes the activity flow for the Flight Booking System, focusing on the customer flight booking process.

The diagram covers customer authentication, flight search, seat selection, temporary seat reservation, simulated payment, booking confirmation, and ticket generation.

## 2. Activity Diagram

```mermaid
flowchart TD
    A([Start]) --> B[Open Flight Booking System]
    B --> C[Enter Login Credentials]
    C --> D{Credentials Valid?}

    D -- No --> E[Display Login Error]
    E --> C

    D -- Yes --> F[Search Flights]
    F --> G[Enter Origin, Destination and Date]
    G --> H[Display Available Flights]
    H --> I{Suitable Flight Found?}

    I -- No --> J[Display No Flights Found]
    J --> F

    I -- Yes --> K[Select Flight]
    K --> L[Display Available Seats]
    L --> M[Select Seat]
    M --> N{Seat Available?}

    N -- No --> O[Display Seat Unavailable]
    O --> L

    N -- Yes --> P[Create Pending Booking]
    P --> Q[Hold Seat for 10 Minutes]
    Q --> R[Proceed to Simulated Payment]

    R --> S{Payment Completed Within 10 Minutes?}

    S -- No --> T[Expire Pending Booking]
    T --> U[Release Held Seat]
    U --> V[Display Booking Expired]
    V --> Z([End])

    S -- Yes --> W{Payment Successful?}

    W -- No --> X[Cancel Pending Booking]
    X --> U

    W -- Yes --> Y{Seat Hold Still Valid?}

    Y -- No --> T

    Y -- Yes --> AA[Confirm Booking]
    AA --> AB[Mark Seat as Booked]
    AB --> AC[Generate E-Ticket]
    AC --> AD[Send Simulated Confirmation]
    AD --> AE[Display Booking Confirmation]
    AE --> Z

```

## 3. Main Activity Descriptions

| Activity | Description |
|---|---|
| Customer Login | The customer enters their email and password to access the system. |
| Search Flights | The customer searches using origin, destination, and travel date. |
| Select Flight | The customer selects a suitable available flight. |
| Select Seat | The customer chooses an available seat. |
| Temporary Seat Hold | The system holds the selected seat for 10 minutes. |
| Simulated Payment | The customer completes a simulated payment transaction. |
| Booking Confirmation | The system confirms the booking only after successful payment and valid seat hold. |
| Ticket Generation | The system generates an electronic ticket after successful confirmation. |
| Seat Release | The system releases the seat if payment fails or the temporary hold expires. |

## 4. Business Rules

1. Customers must log in before booking a flight.
2. Customers can only select available seats.
3. A selected seat is temporarily held for 10 minutes.
4. A pending booking expires if payment is not completed within 10 minutes.
5. A failed payment cancels the pending booking and releases the seat.
6. The system must validate the seat hold before confirming the booking.
7. An electronic ticket is generated only after successful payment.
8. Payment and booking confirmation notifications are simulated.

## 5. Related Documents

- `requirements.md`
- `architecture.md`
- `sequence_booking.md`
- `state_booking.md`
- `class_diagram.md`
- `erd.md`
