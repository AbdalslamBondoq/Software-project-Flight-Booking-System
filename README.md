# Flight Booking System - Group 17

## 1. Group Information

| Item | Details |
|---|---|
| Group number | 17 |
| Case study | Flight Booking System |
| Course | Software Engineering (CS13477), Fall 2026 |
| Instructor | Dr. Samer El Kababji |

| Student name | Student ID | GitHub account |
|---|---|---|
| Abdullah Jaber | 20230748 | [@abdjaber](https://github.com/abdjaber) |
| Ahmad Ababneh | 20230161 | [@ahmadababneh8256-ux](https://github.com/ahmadababneh8256-ux) |
| Abdusalam Bondoq | 20230948 | [@AbdalslamBondoq](https://github.com/AbdalslamBondoq) |

## 2. Project Overview

**System purpose.** A web application in which customers search for flights, select seats, pay through a simulated payment service, and manage or cancel their bookings. Airline administrators manage flights, airports, and aircraft. A System Manager creates administrator accounts. A 10-minute seat hold prevents two customers from booking the same seat.

**Expected final outcome.** A functional web application with flight search, seat selection and booking, simulated payment, e-ticket and booking confirmation, booking management and cancellation with refunds, and flight administration.

**Main technology and tools.** Python with FastAPI (backend), HTML/CSS/JavaScript (frontend), SQLite (database), pytest (testing), Mermaid (diagrams), Claude Code (Agentic AI implementation), GitHub (version control and pull requests).

## 3. Architecture and Diagrams

| Diagram | Description |
|---|---|
| [C4 System Context](uml/c4_context.md) | The system as a black box with the Customer, Airline Administrator, and System Manager. |
| [C4 Container](uml/c4_container.md) | Web application, Backend API, and SQLite database and how they communicate. |
| [Component Diagram](uml/component_diagram.md) | Components inside the web application and the Backend API. |
| [Deployment Diagram](uml/deployment_diagram.md) | Client device and application server on which the system runs. |
| [Use Case Diagram](uml/use_case_diagram.md) | Actors, use cases, and include/extend relationships. |
| [Use Case Descriptions](uml/use_case_description.md) | Preconditions, main flows, and alternative flows of each use case. |
| [Class Diagram](uml/class_diagram.md) | Main domain classes, attributes, operations, and relationships. |
| [Booking Sequence Diagram](uml/sequence_booking.md) | Seat hold, simulated payment, confirmation, and hold expiry. |
| [Booking Activity Diagram](uml/activity_booking.md) | Customer booking workflow and alternative payment outcomes. |
| [Booking State Diagram](uml/state_booking.md) | Booking lifecycle: Pending, Confirmed, Cancelled, Expired, Completed. |
| [Entity Relationship Diagram](uml/erd.md) | Database tables, keys, and relationships. |

The architecture is explained in [docs/architecture.md](docs/architecture.md).

## 4. Repository Structure

| Folder | Contents |
|---|---|
| `docs/` | Project description, requirements, incremental plan, architecture, AI development log, traceability matrix, testing, and report |
| `uml/` | Editable Mermaid diagram sources; `uml/rendered/` holds exported images |
| `src/` | Application source code produced through the Agentic AI workflow |
| `tests/` | Unit, integration, and system tests |
| `prompts/` | Markdown records of the tasks and prompts given to the coding agent |
| `data/` | Small sample or seed data |
| `config/` | Configuration files |

## 5. Incremental Development

| Version | Capability introduced | Status |
|---|---|---|
| v0.1.0-design / v0.1.0 | User accounts, authentication, administrator account creation | Design |
| v0.2.0-design / v0.2.0 | Flight, airport, and aircraft administration | Planned |
| v0.3.0-design / v0.3.0 | Flight search, filtering, and sorting | Planned |
| v0.4.0-design / v0.4.0 | Seat availability, pending bookings, and 10-minute seat holds | Planned |
| v0.5.0-design / v0.5.0 | Simulated payment, booking confirmation, and e-tickets | Planned |
| v0.6.0-design / v0.6.0 | My Bookings, cancellation, refunds, and confirmation notifications | Planned |
| v1.0.0 | Final integrated release | Planned |

Details are in [docs/incremental_development_plan.md](docs/incremental_development_plan.md).

## 6. Contributions

| Team member | Main responsibility | Commits |
|---|---|---|
| Abdullah Jaber | Project description, requirement IDs, component and deployment diagrams, traceability matrix, use case descriptions | 70 |
| Ahmad Ababneh | State, class, ER, activity, and sequence diagrams; design consistency reviews | 55 |
| Abdusalam Bondoq | Repository setup, initial requirements, C4 diagrams, incremental plan | 69 |

Commit counts are the commits on the `main` branch, including merge commits, as of 21 November 2026 (after PR #55). They are taken from `git shortlog -sne main`, with each member's GitHub account and local Git names added together, and are updated at each tagged release. Commit count alone does not measure the quality of a contribution.
