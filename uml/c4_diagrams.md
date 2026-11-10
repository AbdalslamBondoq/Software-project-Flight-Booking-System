@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

Person(customer, "Customer", "Searches for flights, books seats, and manages bookings.")
Person(admin, "Admin", "Manages flight schedules, airports, and aircraft information.")

System(flightSystem, "Flight Booking System", "Allows customers to search and book flights, and admins to manage flight schedules.")

System_Ext(paymentService, "Simulated Payment Service", "Processes card payments and transaction verification.")
System_Ext(notificationService, "Simulated Notification Service", "Sends booking confirmations and e-tickets via email/SMS.")

Rel(customer, flightSystem, "Searches flights, books seats, makes payments", "HTTPS")
Rel(admin, flightSystem, "Manages schedules, airports, and aircraft", "HTTPS")

Rel(flightSystem, paymentService, "Sends payment requests to", "HTTPS/JSON")
Rel(flightSystem, notificationService, "Sends notifications via", "HTTPS/JSON")
@enduml
