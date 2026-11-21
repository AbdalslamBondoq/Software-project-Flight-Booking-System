
# C4 Level 2 - Container Diagram
## Flight Booking System (Group 17)

This diagram shows the main containers inside the
Flight Booking System and how they communicate.

```mermaid
flowchart TB

    customer["«Person»<br/><b>Customer</b>"]
    admin["«Person»<br/><b>Airline Administrator</b>"]
    manager["«Person»<br/><b>System Manager</b>"]

    subgraph boundary["Flight Booking System «Software System»"]

        web["«Container»<br/><b>Web Application</b><br/>[HTML / CSS / JavaScript]<br/><br/>Customer interface,<br/>admin dashboard and account provisioning."]

        api["«Container»<br/><b>Backend API</b><br/>[Python / FastAPI]<br/><br/>Authentication, authorization,<br/>flight search, booking logic,<br/>seat holding, payment simulation,<br/>notifications and refunds."]

        db[("«Container: Database»<br/><b>Database</b><br/>[SQLite]<br/><br/>Users, roles, airports,<br/>aircraft, flights, seats,<br/>bookings, payments,<br/>tickets and notifications.")]

    end

    customer -->|"HTTPS"| web
    admin -->|"HTTPS"| web
    manager -->|"Creates administrator accounts<br/>[HTTPS]"| web

    web -->|"HTTPS / JSON"| api

    api -->|"SQL / Database transactions"| db

    classDef person fill:#08427b,stroke:#052e56,color:#fff
    classDef container fill:#438dd5,stroke:#2e6295,color:#fff
    classDef database fill:#1168bd,stroke:#0b4884,color:#fff

    class customer,admin,manager person
    class web,api container
    class db database

    style boundary fill:#ffffff,stroke:#444444,stroke-dasharray:6 4,color:#08427b
```
