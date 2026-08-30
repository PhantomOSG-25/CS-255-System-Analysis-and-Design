# DriverPass requirements catalog

> Portfolio enhancement derived from the original DriverPass requirements analysis. Identifiers and acceptance criteria were added after the course to improve traceability and QA readiness.

## Functional requirements

| ID | Requirement | Acceptance summary |
| --- | --- | --- |
| FR-01 | The system shall register customers and maintain account profiles. | A customer can create an account, confirm required fields, sign in, and update permitted profile data. |
| FR-02 | The system shall authenticate users and authorize actions by role. | Customers, instructors, office staff, IT administrators, and owners can access only the capabilities assigned to their roles. |
| FR-03 | The system shall support secure password recovery and administrative account control. | Recovery uses a time-limited verification flow; authorized administrators can disable or restore an account and the action is audited. |
| FR-04 | The system shall display configurable training packages. | Active packages show current content and price; authorized staff can add, update, disable, and restore packages. |
| FR-05 | The system shall purchase a package through an external payment provider. | A successful provider response creates an order and entitlement; a failed or abandoned payment creates neither. |
| FR-06 | The system shall schedule, reschedule, and cancel two-hour driving lessons. | A customer can select an available time, instructor, vehicle, and location; all changes produce confirmation and audit records. |
| FR-07 | The system shall prevent scheduling conflicts. | Concurrent requests cannot double-book a customer, instructor, or vehicle for overlapping time periods. |
| FR-08 | The system shall manage instructor and vehicle availability. | Authorized users can update availability, and unavailable resources are excluded from customer options. |
| FR-09 | The system shall deliver practice tests and record attempts. | A customer can complete a test and immediately see score, status, and attempt history. |
| FR-10 | The system shall track course and assessment progress. | Customers and permitted staff can see completion status, time or activity indicators, and assessment outcomes. |
| FR-11 | The system shall allow instructors to record lesson feedback. | Feedback is associated with the correct customer and appointment and is visible only to authorized users. |
| FR-12 | The system shall provide operational reports. | Authorized users can filter and export reports for appointments, cancellations, packages, payments, progress, and account activity. |
| FR-13 | The system shall synchronize approved DMV content updates. | New content is validated, versioned, logged, and published only after the configured review rule passes. |
| FR-14 | The system shall notify users about material account, purchase, and scheduling events. | Confirmations and changes create a notification record and retry transient delivery failures. |
| FR-15 | The system shall record security- and business-relevant audit events. | Each event records actor, action, target, timestamp, outcome, and correlation identifier without storing secrets. |

## Nonfunctional requirements

| ID | Quality attribute | Requirement |
| --- | --- | --- |
| NFR-01 | Security | All external traffic shall use TLS; sensitive stored data shall use encryption appropriate to its classification. |
| NFR-02 | Authentication | Privileged roles shall use multi-factor authentication; repeated failed logins shall trigger rate limiting, temporary lockout, and alerting. |
| NFR-03 | Privacy | The application shall minimize collected personal data and shall not store full payment-card numbers or card security codes. |
| NFR-04 | Availability | Customer scheduling, course access, and administrative operations shall be designed for monitored cloud availability with documented recovery procedures. |
| NFR-05 | Performance | Common authenticated pages should respond promptly under expected load, and availability searches shall return current results without allowing stale reservations. |
| NFR-06 | Concurrency | Scheduling operations shall be atomic so simultaneous requests cannot reserve the same constrained resource. |
| NFR-07 | Accessibility | Core workflows shall support keyboard navigation, programmatic labels, readable contrast, clear errors, and responsive reflow. |
| NFR-08 | Compatibility | The responsive web interface shall support current mainstream desktop and mobile browsers. |
| NFR-09 | Maintainability | Identity, scheduling, learning, payment, reporting, notification, and DMV integration concerns shall have clear module boundaries. |
| NFR-10 | Observability | Services shall emit structured logs, health signals, correlation identifiers, and actionable alerts without exposing secrets. |
| NFR-11 | Recoverability | Data shall have tested backup and recovery procedures with defined recovery objectives before production release. |
| NFR-12 | Auditability | Administrative, scheduling, package, payment, and account changes shall be retained according to an approved policy and protected from ordinary-user modification. |

## Assumptions requiring stakeholder confirmation

- DriverPass will operate in one primary time zone at launch or will explicitly store and display time-zone information.
- A compliant third-party processor will handle payment-card data.
- DMV content is available through a permitted, technically reliable source.
- DriverPass will define cancellation, refund, retention, and instructor-assignment policies.
- Accessibility, privacy, availability, and recovery targets will be approved before implementation.

## Out of scope for the initial design

- Native iOS and Android applications
- Payroll and human-resources management
- Vehicle telematics
- Direct DMV appointment booking unless a supported integration is formally approved
- Automated publication of unreviewed external content
