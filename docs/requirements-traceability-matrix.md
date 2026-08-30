# Requirements traceability matrix

This matrix demonstrates how the portfolio requirements can drive design review and QA planning. The evidence column describes planned acceptance evidence, not completed production testing.

| Requirement | Primary model | Proposed component | Acceptance evidence |
| --- | --- | --- | --- |
| FR-01, FR-03 | Use-case and domain models | Identity and profile service | Registration, validation, recovery-expiry, and profile-authorization tests |
| FR-02, NFR-02 | Use-case and login activity models | Identity provider and authorization policy | Role matrix tests, MFA tests, lockout tests, unauthorized-access tests |
| FR-04 | Use-case and domain models | Package catalog service | Package lifecycle and visibility tests |
| FR-05, NFR-03 | Purchase sequence model | Payment orchestration adapter | Success, decline, timeout, duplicate-callback, and data-minimization tests |
| FR-06, FR-07, NFR-06 | Use-case and domain models | Scheduling service | Create/change/cancel tests plus simultaneous-booking concurrency test |
| FR-08 | Domain model | Availability service | Instructor and vehicle availability rule tests |
| FR-09, FR-10 | Use-case and domain models | Learning and assessment service | Score, status, attempt-history, and progress-permission tests |
| FR-11 | Use-case and domain models | Instructor workflow | Appointment linkage and feedback-visibility tests |
| FR-12, NFR-12 | Use-case model | Reporting and audit services | Filter, permission, export, completeness, and tamper-resistance tests |
| FR-13 | System context model | DMV synchronization adapter | Schema validation, retry, version, approval, and rollback tests |
| FR-14 | System context model | Notification service | Event generation, preference, retry, and failure-observability tests |
| FR-15, NFR-10 | All models | Audit and observability services | Required-field, correlation, redaction, and alert-routing tests |
| NFR-01 | System context model | Web gateway and data platform | TLS configuration, encryption, and secret-management review |
| NFR-04, NFR-11 | System context model | Cloud platform | Health-check, backup, restore, and failure-recovery exercises |
| NFR-05 | Critical workflows | Web and application services | Response-time and capacity tests using approved targets |
| NFR-07, NFR-08 | Customer workflows | Responsive web client | Keyboard, screen-reader, contrast, zoom, reflow, and browser tests |
| NFR-09 | System context and domain models | Modular application services | Architecture review and dependency-boundary checks |
