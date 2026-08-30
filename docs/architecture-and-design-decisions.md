# Architecture and design decisions

## Decision 1: Responsive web application first

**Status:** Recommended

**Context:** Stakeholders need access from desktop and mobile devices without maintaining separate native applications.

**Decision:** Use a responsive browser-based client backed by cloud-hosted application services.

**Tradeoff:** A web-first release reduces platform duplication but must be rigorously tested for mobile usability, accessibility, and browser compatibility.

## Decision 2: Central identity with role-based authorization

**Status:** Recommended

**Context:** Customers, instructors, office staff, IT administrators, and the owner require different capabilities.

**Decision:** Centralize authentication and define permissions through roles and policies enforced by application services, not only by interface visibility.

**Tradeoff:** Central policy management adds design effort but prevents inconsistent authorization rules and simplifies audit review.

## Decision 3: Transactional scheduling boundary

**Status:** Recommended

**Context:** A lesson consumes a customer time slot, an instructor time slot, and a vehicle time slot for a fixed duration.

**Decision:** Validate and reserve all constrained resources in one transactional scheduling operation with conflict detection.

**Tradeoff:** Strong consistency is more complex than separate calendar updates, but it prevents the business-critical failure of double booking.

## Decision 4: Externalize payment-card handling

**Status:** Recommended

**Context:** The source requirements mention payment details, including card-security data.

**Decision:** Use hosted fields or an equivalent compliant processor flow. Store only provider references, transaction status, amount, and reconciliation data.

**Tradeoff:** DriverPass depends on the processor's availability and API but substantially reduces sensitive-data exposure and compliance scope.

## Decision 5: Version and approve DMV content

**Status:** Recommended

**Context:** DriverPass wants current law, policy, and practice-question updates from the DMV.

**Decision:** Import external data into a staged version, validate its schema and provenance, and require the configured approval step before publication.

**Tradeoff:** Updates are not instant, but the system avoids silently publishing malformed or inappropriate external content.

## Decision 6: Separate audit events from operational records

**Status:** Recommended

**Context:** The owner and administrators need tracking for account, appointment, package, and payment activity.

**Decision:** Record immutable-style audit events containing actor, action, target, timestamp, outcome, and correlation identifier while keeping business records optimized for current operations.

**Tradeoff:** This creates another data stream and retention responsibility but improves supportability, security investigations, and reporting confidence.

## Logical component view

- **Web client:** responsive role-specific experiences
- **Identity service:** authentication, MFA, recovery, sessions, authorization context
- **Catalog service:** packages, prices, status, and entitlements
- **Scheduling service:** appointments, availability, conflicts, cancellations
- **Learning service:** course progress, assessments, attempts, scores, feedback
- **Payment adapter:** provider requests, callbacks, idempotency, reconciliation
- **Notification service:** email/SMS request handling and retries
- **Reporting service:** authorized operational views and exports
- **DMV adapter:** controlled synchronization, validation, versioning, approval
- **Audit and observability:** audit events, logs, metrics, traces, and alerts
