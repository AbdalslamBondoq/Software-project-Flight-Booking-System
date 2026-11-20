# C4 Level 1 - System Context

## Flight Booking System (Group 17)

This diagram shows the Flight Booking System as a black box, its users, and their interactions with the system.

```mermaid
flowchart TD
    Customer["«Person»<br/><b>Customer</b><br/>Searches flights, books seats, makes payments and manages bookings."]
    Admin["«Person»<br/><b>Airline Administrator</b><br/>Manages flights, airports and aircraft."]
    Manager["«Person»<br/><b>System Manager</b><br/>Creates and configures administrator accounts in advance."]
    System["«Software System»<br/><b>Flight Booking System</b><br/>Customers book flights, airline administrators manage flight data, and the system manager creates administrator accounts."]

    Customer -->|Searches, books, pays and manages bookings| System
    Admin -->|Manages flights, airports and aircraft| System
    Manager -->|Creates administrator accounts| System

    classDef person fill:#0b4075,stroke:#082d50,color:#fff
    classDef software fill:#1168bd,stroke:#0b4884,color:#fff
    class Customer,Admin,Manager person
    class System software
```
