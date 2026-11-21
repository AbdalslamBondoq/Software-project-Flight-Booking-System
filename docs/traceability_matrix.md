# Traceability Matrix - Flight Booking System (Group 17)

This matrix maps the 16 functional requirements and 4 non-functional requirements in [Requirements](requirements.md) to their use cases, design artifacts, planned versions, and validation activities. Version assignments and planned implementation modules follow the [Incremental Development Plan](incremental_development_plan.md). The module and test entries are marked (planned) until the code and tests exist.

For versions v0.1.0 through v0.6.0, each version has a corresponding design version with the `-design` suffix. For example, a row assigned to v0.4.0 is designed in v0.4.0-design and implemented in v0.4.0. The final integration release is v1.0.0.

## 1. Functional Requirements Traceability

Use case IDs refer to the [Use Case Descriptions](../uml/use_case_description.md). The design column links to the artifact that explains the relevant behavior or data.

| ID | Requirement | Related use cases | Design | Planned version | Implementation module(s) | Test(s) | Planned validation | Status |
|---|---|---|---|---|---|---|---|---|
| FR-01 | Register | UC-01 Register Account | [Use cases](../uml/use_case_description.md), [Class diagram](../uml/class_diagram.md) | v0.1.0 | `src/auth` (planned) | `tests/` (planned) | Register a customer with a new email. Verify that a duplicate email is rejected and public registration creates only customer accounts. | Design |
| FR-02 | Admin Account Creation | UC-18 Create Administrator Accounts | [Use cases](../uml/use_case_description.md), [Architecture](architecture.md) | v0.1.0 | `src/auth` (planned) | `tests/` (planned) | Verify that the System Manager can create and configure an administrator account and that other roles cannot provision one. | Design |
| FR-03 | Login and Logout | UC-02 Log In / Log Out | [Use cases](../uml/use_case_description.md) | v0.1.0 | `src/auth` (planned) | `tests/` (planned) | Log in as a customer, as an administrator, and as the System Manager. Verify that incorrect credentials are rejected and logout ends the session. | Design |
| FR-04 | Search Flights | UC-03 Search Flights | [Use cases](../uml/use_case_description.md) | v0.3.0 | `src/search` (planned) | `tests/` (planned) | Search by origin, destination, and travel date. Check both matching flights and a search with no matches. | Design |
| FR-05 | Filter Results | UC-04 Filter and Sort Results | [Use cases](../uml/use_case_description.md) | v0.3.0 | `src/search` (planned) | `tests/` (planned) | Apply price and time filters and check the returned flights. Sort the results and check their order. | Design |
| FR-06 | View Seats | UC-05 View Available Seats | [Use cases](../uml/use_case_description.md), [Class diagram](../uml/class_diagram.md) | v0.4.0 | `src/booking` (planned) | `tests/` (planned) | Open a flight with available, held, and booked seats. Verify that the seat map shows each seat's current status for that flight. | Design |
| FR-07 | Book Seat | UC-06 Select Seat, UC-07 Create Booking | [Booking activity](../uml/activity_booking.md), [Booking sequence](../uml/sequence_booking.md) | v0.4.0 | `src/booking` (planned) | `tests/` (planned) | As a logged-in customer, select an available seat and submit the booking request. Verify that a PENDING booking references the correct customer, flight, and seat. | Design |
| FR-08 | Prevent Double Booking | UC-07 Create Booking, UC-08 Hold Seat for 10 Minutes | [Booking sequence](../uml/sequence_booking.md), [Booking states](../uml/state_booking.md), [ERD](../uml/erd.md) | v0.4.0 | `src/booking` (planned) | `tests/` (planned) | Submit two simultaneous requests for the same flight seat. Verify that only one obtains the hold. Let the 10-minute hold expire and verify that the pending booking becomes EXPIRED and the seat becomes available again. | Design |
| FR-09 | Pay | UC-09 Complete Simulated Payment, UC-19 Confirm Booking | [Booking sequence](../uml/sequence_booking.md), [Booking states](../uml/state_booking.md) | v0.5.0 | `src/payment` (planned) | `tests/` (planned) | With an active hold, verify that successful payment confirms the booking and marks the seat as BOOKED. Verify that failed payment cancels the booking and releases the seat. A late payment result must leave an expired booking unconfirmed. | Design |
| FR-10 | E-ticket | UC-10 Generate E-ticket | [Booking sequence](../uml/sequence_booking.md), [ERD](../uml/erd.md) | v0.5.0 | `src/payment` (planned) | `tests/` (planned) | Verify that a confirmed booking has an e-ticket with a unique ticket number. Verify that failed payment and hold expiry produce no ticket. | Design |
| FR-11 | View Bookings | UC-12 View My Bookings | [Use cases](../uml/use_case_description.md) | v0.6.0 | `src/bookings_mgmt` (planned) | `tests/` (planned) | Use two customer accounts. Verify that each sees only their own bookings and the current status of each booking. | Design |
| FR-12 | Cancel Booking | UC-13 Cancel Booking | [Booking states](../uml/state_booking.md), [Use cases](../uml/use_case_description.md) | v0.6.0 | `src/bookings_mgmt` (planned) | `tests/` (planned) | Cancel an owned, confirmed booking before departure and verify that the seat is released. Verify that another customer's booking and a departed flight's booking cannot be cancelled by the customer. | Design |
| FR-13 | Refund | UC-14 Calculate Refund | [Use cases](../uml/use_case_description.md), [ERD](../uml/erd.md) | v0.6.0 | `src/bookings_mgmt` (planned) | `tests/` (planned) | Cancel more than 14 days before departure, exactly 14 days before, and just under 14 days before. Verify recorded refunds of 50%, 50%, and zero respectively. | Design |
| FR-14 | Confirmation | UC-11 Record Booking Confirmation | [Booking sequence](../uml/sequence_booking.md), [Class diagram](../uml/class_diagram.md), [ERD](../uml/erd.md), [Architecture](architecture.md) | v0.6.0 | `src/notifications` (planned) | `tests/` (planned) | Verify that successful booking confirmation creates a simulated notification that the customer can view. Check that an expired booking or failed payment produces no confirmation notification. | Design |
| FR-15 | Manage Flights | UC-15 Manage Flights | [Use cases](../uml/use_case_description.md), [ERD](../uml/erd.md) | v0.2.0 | `src/flights` (planned) | `tests/` (planned) | As an airline administrator, add, edit, and delete a flight. Verify that invalid flight details are rejected and that adding a flight creates its seats, as many as the aircraft capacity, all AVAILABLE. | Design |
| FR-16 | Manage Airports and Aircraft | UC-16 Manage Airports, UC-17 Manage Aircraft | [Use cases](../uml/use_case_description.md), [ERD](../uml/erd.md) | v0.2.0 | `src/flights` (planned) | `tests/` (planned) | As an airline administrator, add, edit, and delete airport and aircraft records. Verify that records referenced by existing flights cannot be deleted. | Design |

## 2. Non-Functional Requirements Traceability

| ID | Requirement | Related use cases or scope | Design | Planned version | Implementation module(s) | Test(s) | Planned validation | Status |
|---|---|---|---|---|---|---|---|---|
| NFR-01 | Password Hashing | UC-01 Register Account, UC-02 Log In / Log Out, UC-18 Create Administrator Accounts | [Class diagram](../uml/class_diagram.md), [ERD](../uml/erd.md) | v0.1.0 | `src/auth` (planned) | `tests/` (planned) | Create a customer and an administrator account. Review the password storage logic and verify that both records contain password hashes and that both users can authenticate. | Design |
| NFR-02 | Search Speed | UC-03 Search Flights | [Use cases](../uml/use_case_description.md), [Incremental plan](incremental_development_plan.md) | v0.3.0 | `src/search` (planned) | `tests/` (planned) | With 1,000 flights in the database, measure the time from search submission until results appear and verify that it is within 3 seconds. | Design |
| NFR-03 | Responsive UI | Customer-facing and administrative web pages | [C4 container](../uml/c4_container.md), [Incremental plan](incremental_development_plan.md) | v1.0.0 | Web application pages (planned) | `tests/` (planned) | At screen widths of 360 px and 1920 px, complete the booking workflow and open the relevant administrative screens. Verify that there is no horizontal scrolling and that controls and results remain usable. | Design |
| NFR-04 | Admin-only Access | UC-02 Log In / Log Out, UC-15 Manage Flights, UC-16 Manage Airports, UC-17 Manage Aircraft | [Use cases](../uml/use_case_description.md), [Architecture](architecture.md) | v0.1.0 and v0.2.0 | `src/auth`, `src/flights` (planned) | `tests/` (planned) | Verify role assignment at login in v0.1.0. In v0.2.0, verify that airline administrators can manage flight, airport, and aircraft data and that the backend rejects these requests from other roles. | Design |

## 3. Design Artifact References

| Artifact | Scope |
|---|---|
| [C4 System Context Diagram](../uml/c4_context.md) | System boundary and the Customer, Airline Administrator, and System Manager roles |
| [C4 Container Diagram](../uml/c4_container.md) | Web application, Backend API, database, and their interactions |
| [Component Diagram](../uml/component_diagram.md) | Software components and their responsibilities |
| [Use Case Diagram](../uml/use_case_diagram.md) | Actors, use cases, and their relationships |
| [Use Case Descriptions](../uml/use_case_description.md) | Use case IDs, preconditions, main flows, and alternative outcomes |
| [Booking Sequence Diagram](../uml/sequence_booking.md) | Order of interactions during seat holding, payment, and confirmation |
| [Booking Activity Diagram](../uml/activity_booking.md) | Customer booking workflow and alternative payment outcomes |
| [Booking State Diagram](../uml/state_booking.md) | Booking states and the conditions for each transition |
| [Class Diagram](../uml/class_diagram.md) | Domain classes, responsibilities, and relationships |
| [Entity Relationship Diagram](../uml/erd.md) | Stored entities, relationships, and database constraints |
| [Deployment Diagram](../uml/deployment_diagram.md) | Deployment structure |
| [Architecture](architecture.md) | Application layers, access control, simulated services, and booking rules |

## 4. Status Definitions

| Status | Meaning |
|---|---|
| Design | The requirement and its design representation are documented. Implementation and validation are pending. |
| In Progress | Implementation or validation is underway. |
| Implemented | The functionality has been implemented. |
| Tested | The relevant tests have run successfully and the results are recorded. |
| Verified | The evidence has been reviewed against the requirement's acceptance criteria. |

## 5. Maintenance

Update the affected rows whenever a requirement, use case, diagram, or planned version changes. During implementation, add links to the actual source files, tests, and recorded results. Update a requirement's status when the corresponding evidence is available.
