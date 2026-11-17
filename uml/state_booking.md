# State Diagram - Booking (Group 17)

## 1. Overview

This state diagram describes the lifecycle of a Booking object in the Flight Booking System.

A booking moves through different states depending on seat availability, payment results, seat hold expiration, customer cancellation, and flight departure.

The system uses a 10-minute temporary seat hold to prevent multiple customers from booking the same seat simultaneously.

## 2. State Diagram

```mermaid
stateDiagram-v2

    [*] --> Pending : selectSeat [seat available] / create booking, hold seat for 10 minutes

    Pending --> Confirmed : paymentSuccess [hold still active] / confirm booking, mark seat as booked, issue e-ticket, send confirmation

    Pending --> Cancelled : paymentFailed / cancel booking, release seat

    Pending --> Expired : holdTimeout [10 minutes elapsed] / expire booking, release seat

    Confirmed --> Cancelled : cancelBooking [before departure] / calculate refund, release seat

    Confirmed --> Completed : flightDeparted

    Cancelled --> [*]
    Expired --> [*]
    Completed --> [*]

    note right of Pending
        Seat is temporarily held.
        Payment must be completed
        within 10 minutes.
    end note

    note right of Confirmed
        Payment succeeded.
        E-ticket has been issued.
        Seat is permanently booked.
    end note

    note right of Cancelled
        Cancellation may occur
        because of payment failure
        or customer cancellation.
        Customer refund depends
        on the cancellation policy.
    end note

    note right of Expired
        The seat hold expired
        before payment completion.
        The seat becomes available again.
    end note

    note right of Completed
        The flight has departed.
        The booking lifecycle is complete.
    end note
```

## 3. Booking States

| State | Meaning |
|---|---|
| Pending | A seat is temporarily held for 10 minutes while waiting for payment. |
| Confirmed | Payment succeeded, the booking is confirmed, and an e-ticket is issued. |
| Cancelled | The booking was cancelled because payment failed or the customer requested cancellation. |
| Expired | The 10-minute seat hold expired before payment was completed. |
| Completed | The flight has departed and the booking lifecycle is complete. |

## 4. State Transition Descriptions

| Current State | Event / Condition | Next State | Action |
|---|---|---|---|
| Initial | Customer selects an available seat | Pending | Create booking and hold seat for 10 minutes. |
| Pending | Payment succeeds and seat hold is still active | Confirmed | Confirm booking, mark seat as booked, generate e-ticket, and send confirmation. |
| Pending | Payment fails | Cancelled | Cancel booking and release seat. |
| Pending | 10-minute hold expires | Expired | Expire booking and release seat. |
| Confirmed | Customer cancels before departure | Cancelled | Calculate refund according to the cancellation policy and release seat. |
| Confirmed | Flight departs | Completed | Mark booking as completed. |

## 5. Business Rules

- A booking starts in the Pending state when a customer selects an available seat.
- A selected
