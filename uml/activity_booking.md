# Activity Diagram - Flight Booking System

## 1. Overview

This document describes the customer flight booking process, including login, flight search, seat selection, the 10-minute seat hold, simulated payment, booking confirmation, and e-ticket generation.

The diagram uses two swimlanes: **Customer** and **Flight Booking System**. Simulated payment is processed by the payment module inside the Flight Booking System backend. The solid circle is the initial node, the circle with a thick border is the final node, and conditions on decision branches are written as guards in square brackets.

## 2. Activity Diagram

```mermaid
flowchart LR
    subgraph CustomerLane["Customer"]
        Start(("&nbsp;")) --> C1[Open Flight Booking System]
        C1 --> C2[Enter login credentials]
        C3[Enter origin, destination and date]
        C3b[Optionally filter and sort results]
        C4[Select flight]
        C5[Select seat]
        C6[Confirm simulated payment]
    end

    subgraph SystemLane["Flight Booking System"]
        S1{Credentials valid?}
        S2[Display login error]
        S3[Search matching flights]
        S4{Matching flights found?}
        S4n[Display no flights found]
        S4y[Display flight results]
        S5[Display seat availability]
        S6{Seat still available?}
        S7[Display seat unavailable]
        S8[Create PENDING booking and hold seat for 10 minutes]
        S9{Payment confirmed within 10 minutes?}
        P1[Process simulated payment - payment module]
        S10[Mark booking EXPIRED]
        S11[Release held seat]
        S12[Display booking expired]
        S13{Payment successful?}
        S14[Mark booking CANCELLED]
        S15[Release held seat]
        S15b[Display payment failed]
        S16{Seat hold still active?}
        S17[Mark booking CONFIRMED and seat BOOKED]
        S18[Generate e-ticket]
        S19[Record simulated booking confirmation]
        S20[Display confirmation and e-ticket]
        M1{" "}
        End((("&nbsp;")))
    end

    C2 --> S1
    S1 -- "[invalid]" --> S2 --> C2
    S1 -- "[valid]" --> C3
    C3 --> S3 --> S4
    S4 -- "[no]" --> S4n --> C3
    S4 -- "[yes]" --> S4y --> C3b --> C4
    C4 --> S5 --> C5
    C5 --> S6
    S6 -- "[no]" --> S7 --> S5
    S6 -- "[yes]" --> S8 --> S9
    S9 -- "[no: 10 minutes elapsed]" --> S10
    S9 -- "[yes]" --> C6 --> P1 --> S13
    S13 -- "[failed]" --> S14
    S13 -- "[succeeded]" --> S16
    S16 -- "[expired]" --> S10
    S16 -- "[active]" --> S17 --> S18 --> S19 --> S20 --> M1
    S10 --> S11 --> S12 --> M1
    S14 --> S15 --> S15b --> M1
    M1 --> End

    style Start fill:#000,stroke:#000
    style End fill:#000,stroke:#000,stroke-width:4px
```

## 3. Main Activity Descriptions

| Activity | Description |
|---|---|
| Customer Login | The customer enters their email and password to access the system. |
| Search Flights | The customer searches by origin, destination, and travel date. |
| No Flights Found | If no flights match, the system displays a message and the customer can search again. |
| Filter and Sort | The customer can optionally filter and sort the results by price and time (FR-05). |
| Select Flight | The customer selects a suitable flight. |
| Select Seat | The customer chooses a seat, and the system checks its availability. |
| Temporary Seat Hold | The system creates a pending booking and holds the selected seat for 10 minutes. |
| Simulated Payment | The customer submits payment while the seat hold is active. |
| Payment Failure | The system cancels the pending booking, releases the seat, and displays a payment failure message. |
| Hold Expiration | When the hold expires before confirmation, the system marks the pending booking as expired, releases the seat, and displays an expiration message. |
| Booking Confirmation | After successful payment, the system verifies that the hold is still valid, confirms the booking, and marks the seat as booked. |
| Ticket and Notification | The system generates an e-ticket, records a simulated booking confirmation, and displays the confirmation and ticket to the customer. |

## 4. Business Rules

1. Customers must log in before booking a flight.
2. Only an available seat can be reserved. The availability check, pending booking creation, and seat hold must occur in one database transaction to prevent double booking.
3. The seat hold lasts 10 minutes from the creation of the pending booking.
4. When the hold expires, the system marks the pending booking as `EXPIRED` and releases the seat.
5. If payment fails while the hold is active, the system marks the pending booking as `CANCELLED`, releases the seat, and displays a payment failure message.
6. The system confirms a booking only if payment succeeds and the booking still owns an active hold on the seat.
7. The system generates an e-ticket only after confirming the booking.
8. Payment processing and booking notifications are simulated.

## 5. Related Documents

- [Requirements](../docs/requirements.md)
- [Architecture](../docs/architecture.md)
- [Booking Sequence Diagram](sequence_booking.md)
- [Booking State Diagram](state_booking.md)
- [Class Diagram](class_diagram.md)
- [Entity Relationship Diagram](erd.md)
# Activity Diagram - Flight Booking System

## 1. Overview

This document describes the customer flight booking process, including login, flight search, seat selection, the 10-minute seat hold, simulated payment, booking confirmation, and e-ticket generation.

The diagram uses three swimlanes: **Customer**, **Flight Booking System**, and **Payment Service (simulated)**. The solid circle is the initial node, the circle with a thick border is the final node, and conditions on decision branches are written as guards in square brackets.

## 2. Activity Diagram

```mermaid
flowchart LR
    subgraph CustomerLane["Customer"]
        Start(("&nbsp;")) --> C1[Open Flight Booking System]
        C1 --> C2[Enter login credentials]
        C3[Enter origin, destination and date]
        C3b[Optionally filter and sort results]
        C4[Select flight]
        C5[Select seat]
        C6[Confirm simulated payment]
    end

    subgraph SystemLane["Flight Booking System"]
        S1{Credentials valid?}
        S2[Display login error]
        S3[Search matching flights]
        S4{Matching flights found?}
        S4n[Display no flights found]
        S4y[Display flight results]
        S5[Display seat availability]
        S6{Seat still available?}
        S7[Display seat unavailable]
        S8[Create PENDING booking and hold seat for 10 minutes]
        S9{Payment confirmed within 10 minutes?}
        S10[Mark booking EXPIRED]
        S11[Release held seat]
        S12[Display booking expired]
        S13{Payment successful?}
        S14[Mark booking CANCELLED]
        S15[Release held seat]
        S15b[Display payment failed]
        S16{Seat hold still active?}
        S17[Mark booking CONFIRMED and seat BOOKED]
        S18[Generate e-ticket]
        S19[Record simulated booking confirmation]
        S20[Display confirmation and e-ticket]
        M1{" "}
        End((("&nbsp;")))
    end

    subgraph PaymentLane["Payment Service (simulated)"]
        P1[Process simulated payment]
    end

    C2 --> S1
    S1 -- "[invalid]" --> S2 --> C2
    S1 -- "[valid]" --> C3
    C3 --> S3 --> S4
    S4 -- "[no]" --> S4n --> C3
    S4 -- "[yes]" --> S4y --> C3b --> C4
    C4 --> S5 --> C5
    C5 --> S6
    S6 -- "[no]" --> S7 --> S5
    S6 -- "[yes]" --> S8 --> S9
    S9 -- "[no: 10 minutes elapsed]" --> S10
    S9 -- "[yes]" --> C6 --> P1 --> S13
    S13 -- "[failed]" --> S14
    S13 -- "[succeeded]" --> S16
    S16 -- "[expired]" --> S10
    S16 -- "[active]" --> S17 --> S18 --> S19 --> S20 --> M1
    S10 --> S11 --> S12 --> M1
    S14 --> S15 --> S15b --> M1
    M1 --> End

    style Start fill:#000,stroke:#000
    style End fill:#000,stroke:#000,stroke-width:4px
```

## 3. Main Activity Descriptions

| Activity | Description |
|---|---|
| Customer Login | The customer enters their email and password to access the system. |
| Search Flights | The customer searches by origin, destination, and travel date. |
| No Flights Found | If no flights match, the system displays a message and the customer can search again. |
| Filter and Sort | The customer can optionally filter and sort the results by price and time (FR-05). |
| Select Flight | The customer selects a suitable flight. |
| Select Seat | The customer chooses a seat, and the system checks its availability. |
| Temporary Seat Hold | The system creates a pending booking and holds the selected seat for 10 minutes. |
| Simulated Payment | The customer submits payment while the seat hold is active. |
| Payment Failure | The system cancels the pending booking, releases the seat, and displays a payment failure message. |
| Hold Expiration | When the hold expires before confirmation, the system marks the pending booking as expired, releases the seat, and displays an expiration message. |
| Booking Confirmation | After successful payment, the system verifies that the hold is still valid, confirms the booking, and marks the seat as booked. |
| Ticket and Notification | The system generates an e-ticket, records a simulated booking confirmation, and displays the confirmation and ticket to the customer. |

## 4. Business Rules

1. Customers must log in before booking a flight.
2. Only an available seat can be reserved. The availability check, pending booking creation, and seat hold must occur in one database transaction to prevent double booking.
3. The seat hold lasts 10 minutes from the creation of the pending booking.
4. When the hold expires, the system marks the pending booking as `EXPIRED` and releases the seat.
5. If payment fails while the hold is active, the system marks the pending booking as `CANCELLED`, releases the seat, and displays a payment failure message.
6. The system confirms a booking only if payment succeeds and the booking still owns an active hold on the seat.
7. The system generates an e-ticket only after confirming the booking.
8. Payment processing and booking notifications are simulated.

## 5. Related Documents

- [Requirements](../docs/requirements.md)
- [Architecture](../docs/architecture.md)
- [Booking Sequence Diagram](sequence_booking.md)
- [Booking State Diagram](state_booking.md)
- [Class Diagram](class_diagram.md)
- [Entity Relationship Diagram](erd.md)
