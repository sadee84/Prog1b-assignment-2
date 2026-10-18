# Prog1b-assignment-2
# Wildlife Rescue Operations System

A console-based Java application for **WildLife SA** that lets staff record and manage animal rescue cases. Built for the PROG6112 practical assignment.

## Features

- **Create** rescue cases of three types: Injured, Orphaned or Endangered Species
- **Search** a case by Rescue Case ID
- **Update status**: Reported → Rescue in Progress → Under Observation → Rescue Completed
- **Display** all rescue cases
- **Report**: totals and cost summary across all cases
- **Validation**: no blank fields, positive numbers only, unique IDs, and a rescue cannot be completed before it has started
- All cases are stored in an `ArrayList<RescueCase>`

## Menu

```
1. Create Rescue Case
2. Search Rescue Case
3. Update Rescue Status
4. Display All Rescue Cases
5. Rescue Report
6. Exit
```

## Rescue types

| Type | Extra details captured | Extra cost | Priority rule |
|---|---|---|---|
| Injured Animal | Injury description, vet cost, surgery (Y/N) | Vet cost + R5 000 if surgery | Surgery = Critical; vet cost over R10 000 = High; else Medium |
| Orphaned Animal | Age (months), feeding cost, foster care (Y/N) | Feeding cost + R2 500 if foster care | ≤ 6 months = High; ≤ 24 months = Medium; older = Low |
| Endangered Species | Classification, security cost, specialist team (Y/N) | Security cost + R8 000 if specialist team | Critically Endangered = Critical; Endangered = High; Vulnerable = Medium |

**Total cost** = (rescue days × daily care cost) + type-specific cost

Example: 5 days × R1 500 = R7 500, plus R8 000 vet cost and R5 000 surgery = **R20 500**.

## Project structure

```
WildlifeRescueSystem/
├── pom.xml                          Maven config (Java 17, JUnit 5)
├── README.md
├── docs/
│   └── CODE_EXPLANATION.md          Step-by-step code walkthrough
└── src/
    ├── main/java/
    │   ├── Main.java                Console menu
    │   ├── RescueManager.java       ArrayList storage, search, report
    │   ├── RescueCase.java          Abstract parent class
    │   ├── InjuredAnimalRescue.java
    │   ├── OrphanedAnimalRescue.java
    │   ├── EndangeredSpeciesRescue.java
    │   ├── RescueOperations.java    Interface: start, complete, summary
    │   ├── Assessable.java          Interface: cost, priority
    │   ├── InputHelper.java         Input reading and validation
    │   ├── Money.java               Currency formatting
    │   ├── RescueStatus.java        Enum
    │   ├── RescuePriority.java      Enum
    │   └── ConservationClassification.java  Enum
    └── test/java/
        └── RescueSystemTest.java    21 JUnit tests
```

## OOP concepts demonstrated

| Concept | Where |
|---|---|
| Inheritance | Three rescue classes extend `RescueCase` |
| Abstraction | `RescueCase` is abstract with abstract methods each subclass must implement |
| Interfaces | `RescueOperations` and `Assessable`, implemented by `RescueCase` |
| Encapsulation | Private fields, getters, and controlled status changes |
| Method overriding | Subclasses override cost, priority and detail methods |
| Polymorphism | `RescueManager` calls methods on `RescueCase` references and the correct subclass version runs |

See [`docs/CODE_EXPLANATION.md`](docs/CODE_EXPLANATION.md) for details.

## Requirements

- JDK 17 or newer
- Maven 3.6+ (optional if using NetBeans)

## How to run

**NetBeans**
1. File → Open Project → select the `WildlifeRescueSystem` folder
2. Right-click `Main.java` → Run File
3. Right-click the project → Test to run the JUnit tests

**Terminal**
```bash
mvn compile exec:java    # run the application
mvn test                 # run the 21 unit tests
```

## Testing

`RescueSystemTest` covers cost calculations, priority rules, status transitions (including the invalid "complete before start" case), searching, and duplicate ID rejection.

## Code attribution and AI-use declaration

Claude (Anthropic, 2026), a large language model, was used to generate and structure the code in this project. The code was compiled, run and tested (21 JUnit tests passing). The submitting student must read, understand and be able to explain all code, and must follow The IIE's policy on the use of AI tools, including declaring this use where required.

## References (Harvard)

Anthropic (2026) *Claude* [Large language model]. Available at: https://claude.ai (Accessed: 12 October 2026).

JUnit Team (2024) *JUnit 5 User Guide*. Available at: https://junit.org/junit5/docs/current/user-guide/ (Accessed: 12 October 2026).

Oracle (2024) *Java Platform, Standard Edition 21 API Specification*. Available at: https://docs.oracle.com/en/java/javase/21/docs/api/ (Accessed: 12 October 2026).
