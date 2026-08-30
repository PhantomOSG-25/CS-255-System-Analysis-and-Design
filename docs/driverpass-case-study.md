# DriverPass case study

> Portfolio enhancement based on original CS 255 coursework. This document was prepared after the course to present the analysis in an employer-friendly format.

## Executive summary

DriverPass is a proposed cloud-based training platform for learner drivers. Its business objective is to improve preparation for DMV examinations by combining online course material, practice tests, purchasable training packages, and instructor-led driving lessons in one system.

The analysis converts stakeholder statements into structured requirements, identifies the actors and external services, models the highest-risk workflows, and recommends a secure service-oriented design. The most important design challenge is coordinating customers, instructors, vehicles, lesson durations, payments, and policy updates without schedule conflicts or unauthorized access.

## Client and stakeholder needs

The source interview describes several stakeholder groups:

- **Customers** need to register, purchase a package, study, take practice tests, review progress, and schedule or change lessons.
- **Instructors** need to manage availability, view assigned lessons, and record feedback.
- **Office staff** need customer and calendar access for scheduling and support.
- **IT administrators** need account administration, maintenance access, monitoring, and incident response capabilities.
- **The owner** needs operational reporting, package management, and visibility into business activity.
- **External providers** include a payment processor and a source of DMV content updates.

## Analysis approach

### 1. Establish the system boundary

The analysis separates DriverPass responsibilities from external services. DriverPass owns user experience, scheduling, progress, package configuration, reporting, and audit history. A payment provider owns payment authorization and sensitive card handling. A DMV integration supplies content updates but does not directly publish unreviewed changes.

### 2. Convert stakeholder language into testable requirements

Broad requests such as "access from anywhere" become measurable quality requirements for responsive browser access, authentication, availability, and supported platforms. Scheduling requests become rules that validate customer, instructor, vehicle, location, duration, and time-slot availability as one transaction.

### 3. Model behavior before implementation

The corrected diagrams focus on four questions:

- Who interacts with the system?
- What happens during login and account protection?
- How does package purchase cross the payment boundary?
- Which domain concepts and relationships must the data model support?

### 4. Connect requirements to acceptance evidence

Stable requirement identifiers allow each business need to map to a model, proposed component, and acceptance criterion. This makes design review and QA planning possible before code exists.

## Proposed solution

The recommended solution is a responsive web application with the following logical layers:

1. **Web client:** customer, instructor, and administrative experiences with accessible role-specific navigation.
2. **Identity and access:** authentication, password recovery, multi-factor authentication for privileged users, authorization, and session management.
3. **Application services:** scheduling, catalog/package management, learning and assessment, payment orchestration, reporting, and notifications.
4. **Data services:** relational storage for accounts, roles, packages, appointments, vehicle and instructor availability, assessment attempts, and audit events.
5. **External adapters:** payment processing, outbound notifications, and controlled DMV-content synchronization.

## Important design decisions

### Conflict-safe scheduling

An appointment is not valid unless the selected instructor and vehicle are both available for the complete two-hour lesson and the customer has no conflicting appointment. The availability check and reservation write should occur in one transaction to prevent double booking.

### Least-privilege access

Permissions should be assigned to roles rather than hard-coded to individual screens. The owner, IT administrator, office staff, instructor, and customer roles require different data and actions. Sensitive administrative actions should generate audit events.

### Payment isolation

The application should not store full card numbers or card security codes. It should use a compliant processor and retain only a provider token or transaction reference, status, amount, and timestamps required for reconciliation.

### Controlled DMV updates

External content must be treated as untrusted input. Synchronization should validate payloads, log source and version, support retry and rollback, and require approval before materially changing customer-facing learning content.

## Security and quality considerations

- Use TLS for all network traffic and encryption at rest for sensitive records.
- Require strong password handling and multi-factor authentication for privileged accounts.
- Add rate limiting, temporary lockout, and alerting for repeated failed logins.
- Record auditable events for account changes, scheduling changes, package changes, payments, and privileged access.
- Test role boundaries, scheduling concurrency, payment failures, notification retries, and DMV synchronization failures.
- Design for keyboard access, readable contrast, clear validation messages, and responsive layouts.

## What was done well

The original analysis captured a broad set of functional and nonfunctional needs, recognized multiple administrative roles, considered security controls, and identified the importance of remote access, reporting, schedule management, real-time progress, and DMV updates. It also explored process, object, use-case, activity, sequence, and class models rather than relying on a single view of the system.

## What was improved for the portfolio

The reconstruction strengthens the work in four ways:

1. Requirements now have stable identifiers and verifiable acceptance criteria.
2. Models use clearer boundaries, consistent terminology, and more conventional notation.
3. Security and integration decisions distinguish business needs from implementation safeguards.
4. The repository separates original coursework from later enhancements so provenance remains honest.

## Reflection

User needs should drive system design because a technically elegant system can still fail if it does not support real workflows, responsibilities, constraints, and failure conditions. For future projects, the preferred approach is to establish scope and actors first, normalize stakeholder language into testable requirements, model the riskiest workflows, document design tradeoffs, and build a traceability matrix before implementation begins.
