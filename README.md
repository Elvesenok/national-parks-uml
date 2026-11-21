# National Parks UML

UML class diagram for a national park system.

```mermaid
classDiagram
    direction LR

    class User {
        <<abstract>>
        +String name
        +String contactInfo
        +enterPark(Park, EntryPass) boolean
    }

    class Ranger {
        +String rangerId
        +String assignedZone
        +patrol(Park) void
    }

    class Visitor {
        +String visitorId
    }

    class Park {
        +String parkId
        +String name
        +String location
        +getAvailableTickets() Ticket[*]
        +getVisitors() Visitor[*]
    }

    class Lodge {
        +String lodgeId
        +String name
        +int capacity
        +boolean hasAvailability
    }

    class EntryPass {
        <<abstract>>
        +String passId
        +Date validFrom
        +Date validUntil
        +isValid() boolean
    }

    class Ticket {
        +Date visitDate
        +Decimal price
    }

    class AnnualPass {
        +int year
        +Decimal price
    }

    User <|-- Ranger
    User <|-- Visitor
    Ranger "1..*" --> "1" Park : works at
    Visitor "0..*" --> "0..*" Park : visits
    Park "1" *-- "0..*" Lodge : contains
    EntryPass <|-- Ticket
    EntryPass <|-- AnnualPass
    Visitor "1" --> "0..*" EntryPass : owns
    Ticket "1" --> "1" Park : admits to
    AnnualPass "1" --> "1..*" Park : admits to
```

## Design decisions

- `User` is the common base class for `Ranger` and `Visitor`.
- `Ranger` represents park staff; each ranger is assigned to a park.
- `Visitor` can enter a park with one of two entry-pass types:
  - `Ticket` grants entry to one park for a specific visit date.
  - `AnnualPass` grants entry to one or more parks during a year.
- `Park` contains lodges and keeps track of visitors and available tickets.

## Source

The diagram source is maintained in this README as Mermaid and can be edited in Mermaid-compatible UML tools or in GitHub.

Public project: https://github.com/Elvesenok/national-parks-uml
