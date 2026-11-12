# C4 Diagrams - Flight Booking System (Group 17)

Follows the C4 model . Level 1 shows the system as a black box with its
users and external systems. Level 2 shows the containers and their technology choices.

## Level 1: System Context

```mermaid
flowchart TB
    customer["<i>«person»</i><br/><b>Customer</b><br/><br/>Searches flights, books seats,<br/>pays and manages bookings."]
    admin["<i>«person»</i><br/><b>Admin</b><br/><br/>Manages flights, airports<br/>and aircraft."]
    fbs["<i>«system»</i><br/><b>Flight Booking System</b><br/><br/>Online flight booking platform."]
    payment["<i>«external_system»</i><br/><b>Payment Service</b><br/><br/>Processes payments and<br/>refunds (simulated)."]
    notify["<i>«external_system»</i><br/><b>Notification Service</b><br/><br/>Delivers booking confirmations<br/>(simulated)."]

    customer -->|"<b>Searches, books, pays,<br/>cancels</b>"| fbs
    admin -->|"<b>Manages flights,<br/>airports, aircraft</b>"| fbs
    fbs -->|"<b>Sends payment and<br/>refund requests</b>"| payment
    fbs -->|"<b>Sends booking<br/>confirmations</b>"| notify

    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef sys fill:#1168bd,stroke:#0b4884,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class customer,admin person
    class fbs sys
    class payment,notify ext
```

## Level 2: Containers


```mermaid
flowchart LR
    customer["<i>«person»</i><br/><b>Customer</b><br/><br/>Searches flights, books seats,<br/>pays and manages bookings."]
    admin["<i>«person»</i><br/><b>Admin</b><br/><br/>Manages flights, airports<br/>and aircraft."]

    subgraph boundary["Flight Booking System  «system»"]
        direction TB
        web["<i>«container»</i><br/><b>Web App</b><br/><i>[HTML / CSS / JavaScript]</i><br/><br/>Customer and admin<br/>user interface."]
        api["<i>«container»</i><br/><b>Backend API</b><br/><i>[Python / FastAPI]</i><br/><br/>Booking logic, seat holding,<br/>cancellation and refunds."]
        db[("<i>«container»</i><br/><b>Database</b><br/><i>[SQLite]</i><br/><br/>Users, flights, seats,<br/>bookings, payments, tickets.")]
    end

    payment["<i>«external_system»</i><br/><b>Payment Service</b><br/><br/>Processes payments<br/>(simulated)."]
    notify["<i>«external_system»</i><br/><b>Notification Service</b><br/><br/>Sends confirmations<br/>(simulated)."]

    customer -->|"<b>Uses</b><br/><i>[HTTPS]</i>"| web
    admin -->|"<b>Uses</b><br/><i>[HTTPS]</i>"| web
    web -->|"<b>Calls</b><br/><i>[HTTPS / JSON]</i>"| api
    api -->|"<b>Reads / Writes</b><br/><i>[SQL]</i>"| db
    api -->|"<b>Processes payments via</b>"| payment
    api -->|"<b>Sends confirmations via</b>"| notify

    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef cont fill:#438dd5,stroke:#2e6295,color:#fff
    classDef ext fill:#999999,stroke:#6b6b6b,color:#fff
    class customer,admin person
    class web,api,db cont
    class payment,notify ext
    style boundary fill:#ffffff,stroke:#444444,stroke-dasharray: 6 4, color:#08427b
```

