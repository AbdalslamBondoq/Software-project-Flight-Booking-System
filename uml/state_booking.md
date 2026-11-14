# State Diagram - Booking

Object: **Booking**

```mermaid
stateDiagram-v2
    [*] --> Pending : selectSeat [seat available] / hold seat
    Pending --> Confirmed : paymentSuccess / issue e-ticket, send confirmation
    Pending --> Cancelled : paymentFailed / release seat
    Pending --> Expired : holdTimeout [hold time elapsed] / release seat
    Confirmed --> Cancelled : cancelBooking [before departure] / calculate refund, release seat
    Confirmed --> Completed : flightDeparted
    Cancelled --> [*]
    Expired --> [*]
    Completed --> [*]
```

## States
| State | Meaning |
|-------|---------|
| Pending | Seat is held, waiting for payment |
| Confirmed | Payment succeeded, e-ticket issued |
| Cancelled | Booking cancelled (payment failed or customer cancelled) |
| Expired | Hold time ran out before payment |
| Completed | Flight has departed |