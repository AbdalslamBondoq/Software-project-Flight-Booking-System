# Sequence Diagram - Book a Flight (UC-06 to UC-11, UC-19)
## 1. Overview

This sequence diagram illustrates the process of booking a flight, selecting a seat, holding the seat temporarily, completing simulated payment, and generating an e-ticket.

It describes the interactions between the Customer and the components of the [Component Diagram](component_diagram.md): Customer Interface, API Routes, Booking Management, Seat Availability and Holding, Simulated Payment Processing, E-ticket Generation, Simulated Booking Confirmation, the SQLite Database, and the Hold Expiration Task.

The system uses a 10-minute temporary seat hold to prevent multiple customers from booking the same seat simultaneously.

## 2. Sequence Diagram

```mermaid
sequenceDiagram
    actor C as Customer
    participant UI as Customer Interface
    participant API as API Routes
    participant BM as Booking Management
    participant SH as Seat Availability and Holding
    participant PP as Simulated Payment Processing
    participant T as E-ticket Generation
    participant N as Simulated Booking Confirmation
    participant D as SQLite Database
    participant E as Hold Expiration Task

    %% SEAT SELECTION AND HOLD
    C->>UI: Select flight and seat
    UI->>API: POST /bookings (flightId, seatId)
    API->>BM: Create booking request
    BM->>SH: Acquire seat hold
    SH->>D: In one transaction: check seat, hold seat, create PENDING booking

    alt Seat is available
        D-->>SH: Booking ID and hold expiration time
        Note over SH,D: Hold expires after 10 minutes (expiresAt)
        SH-->>BM: Hold acquired
        BM-->>API: Booking PENDING + expiration time
        API-->>UI: Booking PENDING + expiration time
        UI-->>C: Display booking details and payment countdown

        par Customer payment attempt
            C->>UI: Confirm payment
            UI->>API: POST /payments (bookingId)
            API->>BM: Pay for booking
            BM->>SH: Verify booking is PENDING and hold is active
            SH->>D: Read booking and hold status
            D-->>SH: Booking and hold status
            SH-->>BM: Hold status

            alt Hold is still active
                BM->>PP: Process simulated payment
                PP->>D: Save payment with status SUCCESSFUL or FAILED
                PP-->>BM: Payment result

                alt Payment successful and hold is still valid
                    BM->>SH: Confirm hold
                    SH->>D: In one transaction: booking CONFIRMED, seat BOOKED
                    BM->>T: Generate e-ticket
                    T->>D: Save ticket
                    BM->>N: Record booking confirmation
                    N->>D: Save notification
                    BM-->>API: Booking confirmed + e-ticket
                    API-->>UI: Booking confirmed + e-ticket
                    UI-->>C: Display booking confirmation and e-ticket

                else Payment failed
                    BM->>SH: Release seat
                    SH->>D: Mark booking CANCELLED and release seat
                    BM-->>API: Payment failed
                    API-->>UI: Payment failed
                    UI-->>C: Display payment failure message

                else Hold expired during payment processing
                    BM->>SH: Expire booking
                    SH->>D: Mark booking EXPIRED and release seat
                    BM-->>API: Booking expired
                    API-->>UI: Booking expired
                    UI-->>C: Display expiration message
                end

            else Hold expired before payment
                BM->>SH: Expire booking
                SH->>D: Mark booking EXPIRED and release seat
                BM-->>API: Booking expired
                API-->>UI: Booking expired
                UI-->>C: Ask customer to select another seat
            end

        and Automatic seat hold expiration
            E->>SH: Expire holds past their expiration time
            SH->>D: In one transaction: expire PENDING bookings and release seats
            D-->>SH: Expired bookings updated and seats released
        end

    else Seat is already taken
        D-->>SH: Seat not available
        SH-->>BM: Hold refused
        BM-->>API: Seat not available
        API-->>UI: Seat not available
        UI-->>C: Ask customer to choose another seat
    end
```

## 3. Main Process Description

| Step | Description |
|---|---|
| 1. Select Flight | The customer selects a flight and an available seat. |
| 2. Check Availability | The backend checks whether the selected seat is available. |
| 3. Create Booking | The backend creates a pending booking and temporarily holds the seat. |
| 4. Start Seat Hold | The system holds the seat for 10 minutes and records its expiration time. |
| 5. Payment | The customer confirms payment through the simulated payment service. |
| 6. Payment Verification | The backend verifies the payment result and checks that the seat hold is still valid. |
| 7. Confirm Booking | If payment succeeds within the hold period, the backend confirms the booking and marks the seat as booked. |
| 8. Generate E-ticket | The system generates an e-ticket after successful payment and booking confirmation. |
| 9. Notification | The system records a simulated booking confirmation notification. |
| 10. Release Seat | If payment fails or the hold expires, the system releases the seat. |

## 4. Alternative Scenarios

### 4.1 Seat Already Taken

- The backend detects that the selected seat is unavailable.
- The booking is not created.
- The customer is asked to select another seat.

### 4.2 Payment Failure

- The simulated payment service returns a failure result.
- The payment record is saved with status FAILED.
- The booking is marked as cancelled.
- The temporary seat hold is released.
- The customer receives a payment failure message.

### 4.3 Seat Hold Expiration

- The customer has 10 minutes to complete payment.
- A background expiration task checks expired pending bookings.
- If payment has not been completed, the booking is marked as expired.
- The seat is released and becomes available to other customers.

### 4.4 Payment Processing During Expiration

- The backend checks the seat hold again before confirming the booking.
- If the hold has expired, the booking cannot be confirmed.
- No e-ticket is generated for an expired booking.

## 5. Important Business Rules

- A seat can only be held if it is available.
- A selected seat is held for 10 minutes.
- The expiration time is recorded when the booking is created.
- Only one customer can hold or book a specific seat on a specific flight at a time.
- Seat availability checks and seat holding must be performed atomically to prevent double booking.
- Payment processing is simulated.
- A booking is confirmed only after successful payment and verification of the active seat hold.
- An e-ticket is generated only after successful payment and booking confirmation.
- Failed payments result in booking cancellation and seat release.
- Expired seat holds are automatically released.
- Booking confirmation notifications are simulated and recorded by the system.

## 6. Related Documentation

- Project Description: `docs/project_description.md`
- Requirements: `docs/requirements.md`
- Architecture: `docs/architecture.md`
- Component Diagram: `uml/component_diagram.md`
- Use Case Diagram: `uml/use_case_diagram.md`
- State Diagram: `uml/state_booking.md`
- Class Diagram: `uml/class_diagram.md`
- Entity Relationship Diagram: `uml/erd.md`
