# State Diagram - Booking

```mermaid
stateDiagram-v2
    [*] --> Pending : Customer selects seat
    Pending --> Confirmed : Payment successful
    Pending --> Cancelled : Payment failed
    Pending --> Expired : Hold time ran out
    Confirmed --> Cancelled : Customer cancels
    Confirmed --> Completed : Flight departed
    Cancelled --> [*]
    Expired --> [*]
    Completed --> [*]
```
