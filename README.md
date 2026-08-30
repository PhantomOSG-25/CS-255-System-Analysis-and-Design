# DriverPass System Analysis and Design

DriverPass is a systems-analysis case study for a cloud-based driver-training platform. The project translates stakeholder needs into requirements, process models, interaction models, a domain design, security controls, and implementation-ready acceptance criteria.

This repository combines selected CS 255 coursework with a later portfolio reconstruction. The reconstruction improves organization, traceability, accessibility, privacy, and UML clarity without representing the new material as part of the original graded submission.

## Business problem

DriverPass wants to help learner drivers prepare for DMV examinations through online instruction, practice assessments, and scheduled driving lessons. The system must support customers, instructors, office staff, IT administration, and the business owner while coordinating accounts, packages, appointments, vehicles, assessments, payments, and DMV content updates.

## What this project demonstrates

- Stakeholder and business-requirements analysis
- Functional and nonfunctional requirements
- Role-based access and security design
- Use-case, activity, sequence, and domain modeling
- Requirements traceability and acceptance criteria
- Cloud-platform and integration decisions
- Clear communication for technical and nontechnical audiences

## Portfolio deliverables

| Deliverable | Purpose |
| --- | --- |
| [Case study](docs/driverpass-case-study.md) | Explains the client problem, analysis approach, design response, and lessons learned |
| [Requirements catalog](docs/requirements-catalog.md) | Organizes the functional and quality requirements with stable identifiers |
| [Traceability matrix](docs/requirements-traceability-matrix.md) | Connects requirements to models, components, and acceptance evidence |
| [Architecture decisions](docs/architecture-and-design-decisions.md) | Records the major design choices and tradeoffs |
| [Security and quality](docs/security-and-quality-considerations.md) | Defines risks, controls, validation priorities, and operational considerations |
| [Corrected diagrams](diagrams/README.md) | Provides readable, portfolio-focused system models |
| [Client briefing](presentation/driverpass-client-briefing.pptx) | Summarizes the recommended system for a stakeholder audience |
| [Selected coursework](docs/original-coursework/README.md) | Preserves sanitized source assignments and clearly labels their provenance |

## System at a glance

The proposed platform uses a responsive web interface backed by authenticated application services and a relational data store. Role-based access separates customer, instructor, office, IT-administrator, and owner capabilities. External integrations are isolated behind service boundaries for payment processing and DMV content synchronization.

Key workflows include:

1. Account registration, authentication, password recovery, and account administration.
2. Package discovery, purchase, and payment confirmation.
3. Lesson scheduling with instructor and vehicle conflict prevention.
4. Practice-test delivery, scoring, progress tracking, and instructor feedback.
5. Administrative reporting, package management, and audit review.

## Design highlights

- Scheduling is treated as a concurrency problem: instructor, vehicle, customer, and time-slot availability must be validated together.
- Payment-card data should remain with a compliant payment provider; DriverPass stores only transaction references and status.
- Authentication, authorization, and audit logging are separate concerns.
- DMV synchronization should be monitored, retryable, and unable to overwrite approved content without validation.
- Requirements are written so QA can derive acceptance tests before implementation begins.

## Repository map

```text
.
|-- README.md
|-- RIGHTS.md
|-- docs/
|   |-- driverpass-case-study.md
|   |-- requirements-catalog.md
|   |-- requirements-traceability-matrix.md
|   |-- architecture-and-design-decisions.md
|   |-- security-and-quality-considerations.md
|   `-- original-coursework/
|-- diagrams/
`-- presentation/
```

## Provenance and privacy

The original work was completed by Michael B. Wood for CS 255. Portfolio-enhancement documents and corrected diagrams were produced later from the original analysis and are identified as such. Personal email addresses, local computer paths, revision identifiers, template-author metadata, and unlicensed stock persona photographs are intentionally excluded.

See [RIGHTS.md](RIGHTS.md) for reuse limitations.
