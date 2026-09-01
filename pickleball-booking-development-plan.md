# Pickleball Court Booking Platform
## Senior Software Engineering Development Plan

**Role Perspective:** Senior Software Engineer / Technical Lead  
**Frontend:** Next.js + TypeScript + Tailwind CSS  
**Backend:** Java 21 + Spring Boot 3  
**Database:** PostgreSQL  
**Cache / Hold Optimization:** Redis  
**Messaging:** RabbitMQ / SQS / equivalent when asynchronous workflows are introduced  
**Storage:** S3-compatible object storage  
**Architecture:** Modular Monolith First  
**Primary Goal:** Deliver a production-ready court booking experience with safe concurrency, real-time availability, payments, admin operations, and a clean path for future scale.

---

# 1. Development Objectives

The development plan should deliver the application in a sequence that minimizes risk and creates usable software early.

The implementation should prioritize:

1. Correct court availability
2. Prevention of double booking
3. Fast booking flow
4. Clear pricing
5. Temporary booking holds
6. Reliable payment state handling
7. Customer booking management
8. Staff/admin operations
9. Observability
10. Production readiness

The most critical technical invariant is:

> A court and overlapping time range must never be confirmed for more than one active reservation.

---

# 2. Recommended Delivery Strategy

Use an incremental vertical-slice approach.

Do not build all backend modules first and UI later.

Each milestone should deliver a complete business slice.

Recommended progression:

```text
Foundation
↓
Court Discovery
↓
Availability
↓
Booking Hold
↓
Checkout
↓
Payment
↓
Booking Management
↓
Admin Operations
↓
Notifications
↓
Reporting
↓
Production Hardening
```

Each slice should include:

- Database changes
- Backend logic
- API
- Frontend UI
- Validation
- Tests
- Error states
- Observability

---

# 3. Team Assumption

Recommended small delivery team:

```text
1 Product Manager / Business Analyst
1 Senior / Lead Engineer
1 Backend Engineer
1 Frontend Engineer
1 QA / Test Engineer
1 UI/UX Designer
```

Optional:

```text
DevOps / Cloud Engineer
Security Engineer
Data / Analytics Engineer
```

For a smaller team, one senior full-stack engineer may cover several roles.

---

# 4. Repository Strategy

Recommended monorepo:

```text
pickleball-platform/
│
├── apps/
│   ├── web/
│   │   └── Next.js
│   │
│   └── api/
│       └── Spring Boot
│
├── docs/
│   ├── requirements/
│   ├── ui-ux/
│   ├── architecture/
│   ├── development/
│   └── adr/
│
├── infrastructure/
│   ├── docker/
│   ├── terraform/
│   └── kubernetes/
│
├── scripts/
└── README.md
```

Alternative separate repositories are acceptable, but monorepo is recommended for a small team.

---

# 5. Branching Strategy

Use trunk-based development with short-lived branches.

Recommended:

```text
main
feature/*
fix/*
chore/*
```

Examples:

```text
feature/booking-hold
feature/court-grid
fix/payment-webhook-idempotency
chore/add-testcontainers
```

Rules:

- No long-lived develop branch required.
- Branches should be short.
- Pull requests should be small.
- Main should remain deployable.
- Use feature flags for incomplete production features when needed.

---

# 6. Commit Convention

Recommended Conventional Commits:

```text
feat:
fix:
refactor:
test:
docs:
chore:
perf:
build:
ci:
```

Examples:

```text
feat(booking): add court hold endpoint
fix(payment): handle duplicate webhook events
test(availability): add overlap integration coverage
```

---

# 7. Pull Request Standards

Each pull request should contain:

- Clear summary
- Business context
- Screenshots for UI changes
- API examples for backend changes
- Migration notes
- Test evidence
- Risk notes
- Rollback considerations if relevant

PR size target:

```text
Prefer < 400 changed lines where practical
```

Larger changes should be divided by business capability.

---

# 8. Coding Standards

## Frontend

Use:

```text
TypeScript strict mode
ESLint
Prettier
Next.js conventions
Tailwind utility-first styling
```

Rules:

- No `any` unless justified.
- Avoid large components.
- Extract business logic from visual components.
- Prefer semantic HTML.
- Keep form validation centralized.
- Avoid deeply nested ternaries.
- Use reusable UI primitives.
- Do not hard-code API URLs in components.
- Use accessible labels and focus states.

## Backend

Use:

```text
Java 21
Spring Boot
Checkstyle / Spotless if desired
Sonar / static analysis
```

Rules:

- Avoid fat controllers.
- Controllers map HTTP to application use cases.
- Domain logic must not live in repositories.
- No direct JPA entity exposure.
- Use DTOs.
- Validate inputs.
- Use transactions deliberately.
- Avoid catching generic exceptions without reason.
- Use meaningful domain exceptions.
- Keep module boundaries clean.

---

# 9. Definition of Ready

A story is ready for development when:

- Business intent is understood.
- Acceptance criteria exist.
- UX behavior is known.
- Dependencies are identified.
- API contract is known or can be defined.
- Required data model is understood.
- Error states are defined.
- Security implications are known.

---

# 10. Definition of Done

A story is done when:

- Code is implemented.
- Unit tests pass.
- Integration tests pass where required.
- UI is responsive.
- Accessibility basics are covered.
- API errors are handled.
- Logs/metrics are added where needed.
- Documentation is updated.
- Pull request is reviewed.
- CI passes.
- Staging verification is complete.
- No critical defects remain.

---

# 11. Development Milestone Overview

Recommended milestone sequence:

```text
M0 — Project Foundation
M1 — Venue & Court Discovery
M2 — Availability Engine
M3 — Booking Hold & Concurrency
M4 — Checkout & Pricing
M5 — Payment & Confirmation
M6 — Customer Booking Management
M7 — Staff / Admin Operations
M8 — Notifications
M9 — Reporting & Analytics
M10 — Security, Performance & Production Hardening
M11 — Launch & Post-Launch Stabilization
```

---

# 12. Milestone 0 — Project Foundation

## Goal

Create a reliable development foundation before business functionality.

## Backend Tasks

- Create Spring Boot application.
- Use Java 21.
- Add PostgreSQL.
- Add Flyway.
- Add Redis client.
- Add actuator.
- Add validation.
- Add OpenAPI.
- Configure profiles:

```text
local
test
staging
production
```

- Create module package structure.
- Add centralized exception handling.
- Add API error response model.
- Add correlation ID support.
- Add database Testcontainers.

## Frontend Tasks

- Create Next.js App Router project.
- Enable TypeScript strict mode.
- Configure Tailwind CSS.
- Create design tokens.
- Create base layout.
- Create shared UI components:

```text
Button
Badge
Card
Input
Select
Dialog
Skeleton
EmptyState
```

- Add responsive header.
- Configure API client.
- Add environment configuration.

## Infrastructure Tasks

Create Docker Compose for:

```text
PostgreSQL
Redis
Mail test service
```

Optional early queue:

```text
RabbitMQ
```

## CI Tasks

Pipeline should run:

```text
Frontend lint
Frontend typecheck
Frontend tests
Backend compile
Backend unit tests
Backend integration tests
Build artifacts
```

## Acceptance Criteria

- Both apps run locally.
- Database migrations execute automatically.
- CI passes.
- Local developer setup documented.
- Health endpoint works.
- Frontend can call backend health API.

---

# 13. Milestone 1 — Venue & Court Discovery

## Goal

Users can browse branches and visually view court information.

## Backend

Implement modules:

```text
venue
court
```

Database:

```text
branch
branch_operating_hours
court
court_amenity
court_image
court_layout_position
```

APIs:

```http
GET /api/v1/branches
GET /api/v1/branches/{id}
GET /api/v1/branches/{id}/courts
GET /api/v1/courts/{id}
```

## Frontend

Build:

```text
/book
BookingHero
BookingSearch
CourtFilter
CourtGrid
CourtCard
CourtLayoutView
CourtDetailsDialog
```

Initial court view may use seeded database data.

## Tests

- Court list API.
- Branch not found.
- Inactive court filtering.
- Responsive card layout.
- Keyboard-selectable available court cards.

## Acceptance Criteria

User can:

- Choose branch.
- View courts.
- View court type.
- View price.
- View surface.
- View amenities.
- Switch between card and visual layout view.

---

# 14. Milestone 2 — Availability Engine

## Goal

Display valid available time ranges for a selected date/time.

## Backend

Implement:

```text
availability
```

Data:

```text
branch_operating_hours
branch_holiday
court_reservation
```

Support reservation types:

```text
BOOKING
HOLD
MAINTENANCE
EVENT
ADMIN_BLOCK
```

Implement:

```http
GET /api/v1/availability
```

Rules:

- Venue operating hours.
- Court active status.
- Maintenance.
- Existing reservations.
- Expired holds ignored.
- Minimum booking duration.
- Maximum duration.
- Advance booking rules.
- Buffers.

## Frontend

Build:

```text
TimeSlotGrid
AvailabilityStatus
AvailabilityLoadingState
NoAvailabilityState
```

Search parameters should be stored in URL.

## Tests

Unit:

- Operating hours.
- Slot generation.
- Buffer handling.
- Back-to-back booking semantics.
- Expired hold ignored.

Integration:

- Reservation blocks availability.
- Maintenance blocks availability.
- Event blocks availability.

## Acceptance Criteria

User can select:

```text
branch
date
time
duration
```

and receive correct available courts.

---

# 15. Milestone 3 — Booking Hold & Concurrency

## Goal

Secure court inventory safely during checkout.

This is the most critical engineering milestone.

## Backend

Implement:

```text
booking
court_reservation
```

Booking states:

```text
DRAFT
HELD
PENDING_PAYMENT
CONFIRMED
EXPIRED
CANCELLED
```

Endpoint:

```http
POST /api/v1/booking-holds
```

Required behavior:

1. Validate booking request.
2. Resolve venue timezone.
3. Convert booking period to UTC.
4. Recalculate availability.
5. Calculate quote.
6. Insert reservation.
7. Fail if time overlaps.
8. Create booking.
9. Return expiration.

## Database

Implement PostgreSQL overlap protection.

Recommended:

```text
tstzrange
GiST exclusion constraint
```

Do not rely on Java locking alone.

## Redis

Optional:

- Hold metadata.
- Availability cache.
- Rate limiting.

PostgreSQL remains source of truth.

## Frontend

When user clicks:

```text
Continue
```

call hold API.

Possible UI states:

```text
CREATING_HOLD
HELD
CONFLICT
ERROR
```

On 409:

```text
This court was just booked.
Availability has been refreshed.
```

## Required Concurrency Test

Simulate:

```text
100 concurrent hold attempts
same court
same time
```

Expected:

```text
1 successful
99 conflicts
```

## Acceptance Criteria

Double booking is impossible at database level.

---

# 16. Milestone 4 — Pricing & Checkout

## Goal

User sees a reliable final price and completes booking details.

## Backend

Implement pricing module.

Inputs:

```text
branch
court
date
time
duration
membership
promotion
add-ons
```

Output:

```text
base amount
adjustments
discount
fees
tax
total
currency
```

Persist price snapshot.

APIs:

```http
POST /api/v1/pricing/quote
GET /api/v1/bookings/{id}
```

## Frontend

Build:

```text
/checkout
CustomerDetailsForm
BookingSummary
AddOnSelector
PromoCode
CancellationPolicy
HoldCountdown
```

Requirements:

- Display hold expiration.
- Show final price.
- Preserve booking ID.
- Prevent submission after expiration.
- Handle price changes gracefully.

## Tests

- Peak rate.
- Weekend rate.
- Promotion.
- Invalid promo.
- Duration pricing.
- Price snapshot consistency.

## Acceptance Criteria

Checkout displays a server-generated total.

---

# 17. Milestone 5 — Payment & Booking Confirmation

## Goal

Complete paid reservations safely.

## Backend

Create:

```text
payment
```

Port:

```java
PaymentGateway
```

Implement:

```text
MockPaymentGateway
```

for development.

Production provider added behind adapter.

Endpoints:

```http
POST /api/v1/bookings/{id}/payment-intent
POST /api/v1/payments/webhooks/{provider}
```

Payment states:

```text
PENDING
PAID
FAILED
REFUNDED
PARTIALLY_REFUNDED
```

## Required Engineering Features

- Idempotency key support.
- Verified webhooks.
- Unique provider event IDs.
- Payment reconciliation.
- Durable payment records.
- No raw card storage.

## Booking Confirmation

When payment succeeds:

```text
PENDING_PAYMENT
→ CONFIRMED
```

Reservation changes:

```text
HOLD
→ BOOKING
```

Create outbox event:

```text
BookingConfirmed
```

## Frontend

Build:

```text
PaymentMethodSelector
PaymentPending
PaymentFailed
BookingConfirmation
```

Confirmation route:

```text
/bookings/{bookingReference}
```

## Tests

- Payment success.
- Payment failure.
- Duplicate webhook.
- Delayed webhook.
- Payment succeeded before callback response.
- Reconciliation recovery.
- Expired hold during payment.

## Acceptance Criteria

Successful payment creates one confirmed booking only.

---

# 18. Milestone 6 — Customer Booking Management

## Goal

Customers can manage reservations after booking.

## Backend

Implement:

```http
GET /api/v1/bookings
GET /api/v1/bookings/{id}
POST /api/v1/bookings/{id}/cancel
POST /api/v1/bookings/{id}/reschedule
```

Features:

- Upcoming bookings.
- Booking history.
- Cancellation.
- Refund calculation.
- Rescheduling.
- Audit history.

## Rescheduling Rule

Safe order:

```text
Secure new reservation first
↓
Handle price difference
↓
Update booking
↓
Release old reservation
```

Do not release old court before new reservation is secured.

## Frontend

Build:

```text
/bookings
BookingList
BookingDetails
CancelBookingDialog
RescheduleBookingFlow
```

## Tests

- Cancellation window.
- Refund amount.
- Reschedule collision.
- More expensive new court.
- Cheaper new court.
- Unauthorized booking access.

## Acceptance Criteria

Customers can manage only their own bookings.

---

# 19. Milestone 7 — Staff & Admin Operations

## Goal

Venue operations can run through the application.

## Backend

Implement roles:

```text
RECEPTIONIST
COURT_MANAGER
FINANCE
ADMIN
OWNER
```

Admin APIs:

```http
GET /api/v1/admin/bookings
POST /api/v1/admin/bookings
GET /api/v1/admin/courts
PUT /api/v1/admin/courts/{id}
POST /api/v1/admin/courts/{id}/blocks
POST /api/v1/admin/courts/{id}/maintenance
POST /api/v1/admin/bookings/{id}/check-in
POST /api/v1/admin/refunds
```

## Frontend

Build:

```text
/admin
AdminLayout
AdminSidebar
DashboardMetrics
BookingCalendar
CourtManagement
MaintenanceForm
BookingSearch
WalkInBooking
CheckIn
```

## Key Operational Flows

- Staff creates walk-in booking.
- Staff checks in customer.
- Manager blocks court.
- Manager adds maintenance.
- Finance processes refund.
- Admin changes pricing.

## Audit

All sensitive actions create audit records.

## Acceptance Criteria

Staff cannot access permissions outside their role.

---

# 20. Milestone 8 — Notifications

## Goal

Send reliable customer communications without blocking bookings.

## Backend

Implement transactional outbox.

Events:

```text
BookingConfirmed
BookingCancelled
BookingRescheduled
PaymentSucceeded
RefundCompleted
BookingReminderRequested
```

Notification channels:

```text
Email
SMS optional
Push future
```

Do not send emails inside booking transaction.

## Worker

Flow:

```text
Outbox
↓
Publisher
↓
Queue
↓
Notification Consumer
↓
Provider
```

For a small MVP, outbox publisher and consumer may run in the same Spring Boot deployment.

## Templates

Create:

```text
Booking confirmation
Cancellation
Reschedule
Payment receipt
Reminder
Refund
```

## Tests

- Outbox retry.
- Duplicate event handling.
- Email provider failure.
- Booking remains successful if notification fails.

---

# 21. Milestone 9 — Reporting & Analytics

## Goal

Provide operational visibility.

## Backend

Initial reporting can use PostgreSQL.

Endpoints:

```http
GET /api/v1/admin/reports/revenue
GET /api/v1/admin/reports/utilization
GET /api/v1/admin/reports/bookings
GET /api/v1/admin/reports/peak-hours
```

Metrics:

```text
Revenue
Bookings
Court utilization
Cancellation rate
No-show rate
Average booking duration
Top courts
Peak hours
```

## Frontend

Build:

```text
RevenueCards
UtilizationTable
BookingTrend
PeakHours
ExportButton
```

Avoid expensive dashboard queries on the transactional path.

Add reporting projections later if required.

---

# 22. Milestone 10 — Production Hardening

## Goal

Meet launch-level reliability, security, and performance expectations.

## Security

Implement:

- HTTPS.
- Secure headers.
- RBAC.
- Rate limiting.
- Secret management.
- PII-safe logging.
- Dependency scanning.
- Audit logs.
- Input validation.
- CSRF strategy where applicable.
- Session/token security.

## Performance

Measure:

```text
Availability p95
Hold creation p95
Database query times
Frontend Web Vitals
```

Targets:

```text
Availability backend p95 < 500ms
Create hold p95 < 750ms
LCP < 2.5s
INP < 200ms
CLS < 0.1
```

## Resilience

Test:

- Redis unavailable.
- Queue unavailable.
- Email provider unavailable.
- Payment timeout.
- Duplicate webhook.
- Database failover behavior.
- Hold cleanup worker failure.

## Observability

Add:

```text
Structured logs
Micrometer metrics
OpenTelemetry traces
Dashboards
Alerts
```

---

# 23. Milestone 11 — Launch & Stabilization

## Pre-Launch

Run:

- Production smoke tests.
- End-to-end booking.
- Refund test.
- Admin override test.
- Concurrency test.
- Backup restore validation.
- Load test.
- Security review.
- Mobile/browser testing.

## Soft Launch

Recommended:

```text
1 branch
limited users
controlled marketing
```

Monitor:

```text
Booking conflicts
Payment failure
API 5xx
Availability latency
No-show workflow
Admin operational issues
```

## Post Launch

Prioritize fixes for:

```text
P0 — Booking/payment corruption
P1 — Booking unavailable or wrong
P2 — Significant UX degradation
P3 — Minor bug
```

---

# 24. Suggested Sprint Plan

If using two-week sprints, a possible sequence is:

## Sprint 1

```text
Foundation
Repository
CI
Database
Design system
Branch/Court entities
```

## Sprint 2

```text
Court discovery
Court UI
Court details
Court layout view
```

## Sprint 3

```text
Availability engine
Time slots
Operating hours
Maintenance
```

## Sprint 4

```text
Court reservation table
Booking hold
Concurrency protection
409 conflict UX
```

## Sprint 5

```text
Pricing
Checkout
Price snapshot
Hold countdown
```

## Sprint 6

```text
Payment adapter
Mock gateway
Payment webhook
Booking confirmation
```

## Sprint 7

```text
Real payment gateway
Reconciliation
Customer bookings
Cancellation
```

## Sprint 8

```text
Rescheduling
Refund flow
Booking details
```

## Sprint 9

```text
Admin dashboard
Booking calendar
Court management
Maintenance
```

## Sprint 10

```text
Walk-in booking
Check-in
RBAC
Audit logging
```

## Sprint 11

```text
Outbox
Notifications
Emails
Reminders
```

## Sprint 12

```text
Reporting
Analytics
Security hardening
Performance
Launch prep
```

This sequence is illustrative and should be adjusted to team capacity.

---

# 25. Epic Structure

Recommended backlog epics:

```text
EPIC-001 Platform Foundation
EPIC-002 Venue & Court Management
EPIC-003 Availability
EPIC-004 Booking Holds
EPIC-005 Pricing
EPIC-006 Checkout
EPIC-007 Payments
EPIC-008 Customer Booking Management
EPIC-009 Staff Operations
EPIC-010 Admin Management
EPIC-011 Notifications
EPIC-012 Reporting
EPIC-013 Security
EPIC-014 Observability
EPIC-015 Production Readiness
```

---

# 26. Sample Engineering Stories

## Story: View Available Courts

**As a customer,**  
I want to view courts available for my selected time,  
so that I can choose a valid court.

### Backend

- Add availability API.
- Query operating hours.
- Query active reservations.
- Exclude blocked courts.

### Frontend

- Display available state.
- Display unavailable state.
- Show loading state.
- Show empty state.

### Acceptance Criteria

- Correct courts returned.
- Unavailable courts cannot be selected.
- Search refreshes after parameter change.

---

# 27. Sample Engineering Story — Create Hold

**As a customer,**  
I want the selected court temporarily reserved during checkout,  
so another user cannot take it while I pay.

### Acceptance Criteria

- Hold lasts configurable period.
- Overlapping hold is rejected.
- Expired hold does not block availability.
- Conflict returns HTTP 409.
- Client shows conflict state.
- Only one concurrent request succeeds.

---

# 28. Sample Engineering Story — Payment Idempotency

**As the platform,**  
I need duplicate payment callbacks to be harmless,  
so a provider retry cannot create duplicate booking state.

### Acceptance Criteria

- Provider event ID is unique.
- Same event can be received multiple times.
- Booking confirmation executes once.
- Endpoint returns successful acknowledgement for duplicate processed event.

---

# 29. Technical Spike Backlog

Use spikes for uncertain integration work.

Potential spikes:

```text
SPIKE-001 PostgreSQL exclusion constraint
SPIKE-002 Payment provider integration
SPIKE-003 Auth provider selection
SPIKE-004 Court layout data model
SPIKE-005 QR check-in
SPIKE-006 Notification provider
SPIKE-007 Load testing threshold
```

Spikes should produce a decision, not production code by default.

---

# 30. Database Migration Plan

Use Flyway.

Naming:

```text
V001__create_branch.sql
V002__create_court.sql
V003__create_operating_hours.sql
V004__create_court_reservation.sql
V005__create_booking.sql
```

Rules:

- Never edit an applied production migration.
- Add new migration instead.
- Add indexes intentionally.
- Avoid destructive schema changes without staged rollout.
- Use backward-compatible deployment where possible.

---

# 31. Seed Data

Local and staging environments should have realistic seed data.

Create:

```text
2 branches
6–12 courts
operating hours
pricing
maintenance
sample users
sample bookings
```

Do not seed production automatically.

---

# 32. API Development Standards

Base:

```text
/api/v1
```

Response rules:

- Consistent JSON.
- ISO-8601 timestamps.
- UTC persistence.
- Explicit currency.
- Explicit status enums.
- Never expose stack trace.
- Include trace ID in errors.

Example error:

```json
{
  "status": 409,
  "code": "COURT_NO_LONGER_AVAILABLE",
  "message": "The selected court is no longer available.",
  "traceId": "abc123"
}
```

---

# 33. API Documentation

Use OpenAPI.

Every endpoint should document:

- Authentication.
- Request.
- Response.
- Error codes.
- Idempotency requirement.
- Pagination.
- Example payload.

Keep API docs synchronized with implementation.

---

# 34. Frontend API Layer

Do not call `fetch` directly throughout components.

Create:

```text
src/lib/api/
```

Example:

```text
branches.ts
courts.ts
availability.ts
bookings.ts
payments.ts
admin.ts
```

Centralize:

- Base URL.
- Headers.
- Authentication.
- Error mapping.
- Correlation ID.
- JSON parsing.

---

# 35. Frontend Error Mapping

Create a friendly error mapper.

Example:

```text
COURT_NO_LONGER_AVAILABLE
→ This court was just booked. Choose another available court.

HOLD_EXPIRED
→ Your booking hold expired. Select the court again.

PAYMENT_FAILED
→ Payment could not be completed. Please try again.

PROMO_INVALID
→ This promotion cannot be applied.
```

Never render raw exception messages.

---

# 36. Frontend State Rules

URL:

```text
branch
date
time
duration
players
filters
```

Local React state:

```text
selected court
dialog open
selected tab
temporary form state
```

Backend state:

```text
availability
booking
payment
price
```

Do not create duplicated sources of truth.

---

# 37. Test Pyramid

Recommended balance:

```text
Many unit tests
Moderate integration tests
Focused E2E tests
```

Do not attempt to cover all behavior through E2E tests.

---

# 38. Backend Unit Tests

Focus on:

```text
Availability rules
Pricing rules
Booking state transitions
Cancellation policy
Refund calculation
Promotion rules
Authorization logic
```

---

# 39. Backend Integration Tests

Use Testcontainers for PostgreSQL.

Required:

```text
Repository behavior
Flyway migrations
Overlap constraint
Transactions
Webhook idempotency
Outbox
Reschedule transaction
```

Do not use H2 as the only database test for PostgreSQL-specific behavior.

---

# 40. Frontend Component Tests

Test:

```text
Court status
Court selection
Time slot selection
Booking summary calculation display
Error state
Loading state
Filter behavior
```

---

# 41. End-to-End Tests

Use Playwright.

Critical E2E:

```text
Search → Select Court → Hold → Checkout → Confirm
```

Additional:

```text
Conflict after selecting court
Payment failure
Cancel booking
Reschedule booking
Admin creates maintenance block
Walk-in booking
```

---

# 42. Accessibility Testing

Automate where possible.

Verify:

- Keyboard navigation.
- Focus order.
- Accessible names.
- Form labels.
- Dialog behavior.
- Contrast.
- Disabled state meaning.
- Status not color-only.

Manual accessibility checks remain necessary.

---

# 43. Load Testing

Recommended tool:

```text
k6
Gatling
JMeter
```

Critical scenarios:

## Availability

```text
high read concurrency
```

## Hold

```text
same court/time contention
```

## Payment Webhook

```text
duplicate/retry burst
```

## Admin

```text
large booking list
```

---

# 44. Required Concurrency Test Gate

Before production launch:

```text
100+ simultaneous hold attempts
same court
same time
```

Expected:

```text
exactly one active reservation
```

Validate the database directly after the test.

This is a release gate.

---

# 45. CI Pipeline

Recommended pull request pipeline:

```text
Checkout
↓
Frontend install
↓
Frontend lint
↓
Frontend typecheck
↓
Frontend unit tests
↓
Backend compile
↓
Backend unit tests
↓
Backend integration tests
↓
Migration test
↓
Build
↓
Security/dependency scan
```

---

# 46. CD Pipeline

Recommended:

```text
Merge to main
↓
Build immutable artifacts
↓
Container scan
↓
Deploy staging
↓
Migration
↓
Smoke tests
↓
E2E tests
↓
Manual or automated promotion
↓
Production
↓
Post-deploy smoke test
```

---

# 47. Deployment Versioning

Use immutable version identifiers.

Example:

```text
web:1.4.2
api:1.4.2
```

or:

```text
git SHA
```

Never deploy `latest` as the only production reference if rollback matters.

---

# 48. Feature Flags

Candidates:

```text
online_payment
waitlist
membership
promo_codes
recurring_booking
dynamic_pricing
sms_notifications
```

Flags should allow features to be deployed safely before activation.

---

# 49. Logging Standards

Structured JSON logs.

Include:

```text
traceId
userId
bookingId
courtId
branchId
paymentId
event
```

Never log:

```text
password
authorization token
CVV
full card number
sensitive payment payload
```

---

# 50. Business Metrics

Instrument:

```text
availability_search_total
booking_hold_created_total
booking_hold_conflict_total
booking_confirmed_total
booking_cancelled_total
booking_rescheduled_total
payment_success_total
payment_failure_total
refund_total
```

---

# 51. Technical Metrics

Monitor:

```text
HTTP p50/p95/p99
5xx rate
DB connection pool
DB slow query count
Redis errors
queue lag
JVM heap
CPU
GC
frontend web vitals
```

---

# 52. Alert Priorities

## P0

```text
Confirmed duplicate booking
Payment charged but booking missing
Database unavailable
```

## P1

```text
High payment failure
High 5xx
Hold creation failure
Webhook backlog
```

## P2

```text
Email failures
Reporting delays
Slow admin dashboard
```

---

# 53. Security Development Checklist

For each feature:

- [ ] Authentication requirement defined
- [ ] Authorization checked server-side
- [ ] Inputs validated
- [ ] Sensitive data classification considered
- [ ] Logs reviewed
- [ ] Rate limit considered
- [ ] Audit requirement considered
- [ ] OWASP risk considered
- [ ] Error response safe

---

# 54. Dependency Policy

Before adding a dependency:

Ask:

1. Is it necessary?
2. Is native framework support enough?
3. Is it actively maintained?
4. Does it have known vulnerabilities?
5. Does it materially reduce complexity?
6. Is the bundle/runtime cost acceptable?

Avoid dependency-heavy architecture.

---

# 55. Code Review Checklist — Backend

Review:

- Correct transaction boundary?
- Domain invariant preserved?
- Race conditions?
- Database constraint needed?
- Idempotency needed?
- Authorization correct?
- Error response stable?
- Sensitive log?
- Unit/integration tests present?
- Module boundary respected?

---

# 56. Code Review Checklist — Frontend

Review:

- Responsive?
- Accessible?
- Loading state?
- Empty state?
- Error state?
- Keyboard usable?
- Business state derived from server correctly?
- No duplicate state?
- Component too large?
- Reusable logic extracted?
- Mobile CTA usable?

---

# 57. Refactoring Policy

Refactor when:

```text
Duplication appears repeatedly
Business logic is hard to test
Component exceeds clear responsibility
Module boundary is being violated
Performance measurement proves need
```

Do not refactor only to introduce patterns without value.

---

# 58. Technical Debt Tracking

Create backlog category:

```text
TECH-DEBT
```

Each item should include:

- Current problem.
- Risk.
- Impact.
- Proposed fix.
- Priority.
- Trigger for action.

Avoid invisible technical debt.

---

# 59. Environment Configuration

Frontend:

```text
NEXT_PUBLIC_API_BASE_URL
```

Backend:

```text
DB_URL
DB_USERNAME
DB_PASSWORD
REDIS_URL
PAYMENT_PROVIDER_KEY
PAYMENT_WEBHOOK_SECRET
EMAIL_PROVIDER_KEY
OBJECT_STORAGE_*
```

Secrets must not be committed.

---

# 60. Local Developer Experience

Target setup:

```text
git clone
docker compose up -d
run api
run web
```

Documentation should cover:

- Prerequisites.
- Ports.
- Environment variables.
- Database migration.
- Seed data.
- Running tests.
- Debugging.
- Resetting local DB.

---

# 61. Recommended Local Ports

Example:

```text
Next.js        3000
Spring Boot    8080
PostgreSQL     5432
Redis          6379
RabbitMQ       5672
RabbitMQ UI    15672
Mail UI        8025
```

---

# 62. Developer Tooling

Recommended:

Backend:

```text
IntelliJ IDEA
Maven or Gradle
Docker
Postman / Bruno
```

Frontend:

```text
VS Code / WebStorm
Node.js LTS
npm / pnpm
```

Shared:

```text
Git
Docker
OpenAPI
Playwright
```

---

# 63. Documentation Requirements

Maintain:

```text
README.md
docs/requirements/
docs/ui-ux/
docs/architecture/
docs/development/
docs/adr/
```

Developer docs should include:

- Setup.
- Architecture overview.
- Module ownership.
- API.
- Booking state machine.
- Payment flow.
- Database constraints.
- Deployment.

---

# 64. Architecture Decision Records

Recommended early ADRs:

```text
ADR-001 Modular Monolith
ADR-002 PostgreSQL
ADR-003 DB-Level Booking Collision Protection
ADR-004 Redis Is Not Source of Truth
ADR-005 REST API
ADR-006 Payment Gateway Abstraction
ADR-007 Transactional Outbox
ADR-008 UTC Persistence
```

---

# 65. Risk Register

## Risk: Double Booking

Mitigation:

```text
PostgreSQL exclusion constraint
Concurrency testing
Backend revalidation
```

## Risk: Payment/Booking State Mismatch

Mitigation:

```text
Webhook idempotency
Reconciliation
Persistent payment state
```

## Risk: Overengineering

Mitigation:

```text
Modular monolith
Avoid premature microservices
Simple infrastructure first
```

## Risk: Slow Availability

Mitigation:

```text
Indexes
Query optimization
Redis cache
Performance tests
```

## Risk: Poor Mobile UX

Mitigation:

```text
Mobile-first development
Responsive test matrix
Sticky booking CTA
```

---

# 66. Release Strategy

Recommended:

```text
Internal QA
↓
Staging
↓
Pilot branch
↓
Soft launch
↓
General launch
```

Do not launch all branches simultaneously if avoidable.

---

# 67. Rollback Strategy

Each release should support rollback.

Application:

```text
redeploy previous container/image
```

Database:

Prefer backward-compatible migrations.

Avoid relying on database rollback scripts for every migration.

Use:

```text
expand
deploy
migrate data
contract later
```

for risky schema evolution.

---

# 68. Production Smoke Tests

After deployment:

1. Health endpoint.
2. Login.
3. Branch list.
4. Availability search.
5. Create test hold.
6. Release/cancel test hold.
7. Payment sandbox flow where permitted.
8. Admin court list.
9. Notification pipeline.
10. Observability dashboards receiving data.

---

# 69. Launch Acceptance Criteria

Launch only if:

- [ ] Double-booking protection proven
- [ ] Payment webhook idempotency proven
- [ ] Reconciliation tested
- [ ] Cancellation tested
- [ ] Backup restore tested
- [ ] Load tests acceptable
- [ ] Security review completed
- [ ] Mobile flow tested
- [ ] Monitoring active
- [ ] Alerts configured
- [ ] Admin operational workflow verified
- [ ] Production support ownership assigned

---

# 70. Post-Launch Engineering Priorities

First 30 days:

```text
Bug stabilization
Performance tuning
Operational feedback
Payment failure analysis
Booking conflict monitoring
UX friction analysis
```

Do not rush major new features before stability is established.

---

# 71. Future Development Roadmap

After MVP stability:

## Phase 2

```text
QR check-in
Waitlist
Promo codes
Equipment rental
Membership
Loyalty
Push notifications
```

## Phase 3

```text
Recurring bookings
Coaching
Tournament management
League features
Dynamic pricing
Corporate bookings
```

## Phase 4

Potential:

```text
Multi-tenant SaaS
Mobile applications
Recommendation engine
Advanced analytics
Service extraction
```

---

# 72. Codex Implementation Plan

The following instructions can be provided directly to Codex.

---

# 73. CODEX MASTER DEVELOPMENT INSTRUCTION

Implement the Pickleball Court Booking Platform incrementally.

Required stack:

```text
Frontend:
Next.js
TypeScript
Tailwind CSS

Backend:
Java 21
Spring Boot 3

Infrastructure:
PostgreSQL
Redis
```

Use a modular monolith.

Do not begin with microservices.

Implement vertical slices and keep the application runnable after each milestone.

---

# 74. Codex Rule — Do Not Skip Foundation

Before business features:

- Set up strict TypeScript.
- Add backend validation.
- Configure Flyway.
- Configure PostgreSQL Testcontainers.
- Add global error handling.
- Add logging correlation.
- Add CI.
- Document local setup.

Do not proceed with booking implementation until migrations and integration tests work.

---

# 75. Codex Rule — Court Reservation Is Highest Priority

When implementing reservation:

Do not rely solely on:

```text
frontend availability
Redis
Java synchronized
application locks
```

Create a PostgreSQL-level overlap guarantee.

Write an integration test that proves it.

---

# 76. Codex Rule — Keep Page Components Small

Next.js pages should compose components.

Do not build the whole booking screen inside:

```text
page.tsx
```

Use:

```text
BookingSearch
CourtGrid
CourtCard
CourtLayoutView
TimeSlotGrid
BookingSummary
```

---

# 77. Codex Rule — Use DTOs

Spring controllers must not expose JPA entities.

Use:

```text
Request DTO
Response DTO
Application command
Domain model
Repository entity if needed
```

Keep HTTP concerns away from domain logic.

---

# 78. Codex Rule — Add Tests With Every Business Rule

When implementing:

```text
booking overlap
hold expiry
pricing
promo
cancellation
refund
reschedule
payment
```

add tests in the same change.

Do not defer all tests to the end.

---

# 79. Codex Rule — Create Explicit State Machines

Do not update booking status arbitrarily.

Create allowed transitions.

Example:

```text
HELD → PENDING_PAYMENT
PENDING_PAYMENT → CONFIRMED
HELD → EXPIRED
CONFIRMED → CANCELLED
```

Reject illegal transitions.

---

# 80. Codex Rule — Centralize Time Handling

Use venue timezone.

Persist UTC.

Create shared time utilities.

Do not let individual controllers calculate timezone conversion independently.

---

# 81. Codex Rule — Centralize Pricing

Create:

```text
PricingService
PriceQuote
PriceSnapshot
```

Frontend never calculates authoritative price.

Frontend may display estimates only when clearly marked.

---

# 82. Codex Rule — Payment Must Be Retry Safe

All webhook handlers must:

- Verify authenticity.
- Check provider event ID.
- Be idempotent.
- Persist result.
- Handle duplicate delivery.
- Return successful response for already processed valid event.

---

# 83. Codex Rule — Use Transactional Outbox

When a business state update requires a future event:

```text
booking state
+
outbox event
```

must commit in the same DB transaction.

Do not publish directly and assume success.

---

# 84. Codex Rule — Add Observability Early

For critical operations log:

```text
bookingId
courtId
branchId
traceId
paymentId
```

Create metrics for:

```text
booking conflicts
hold creation
payment success/failure
```

---

# 85. Codex Rule — Build Empty/Error States

Every major UI must include:

```text
loading
empty
error
success
disabled
```

Do not create happy-path-only screens.

---

# 86. Codex Rule — Responsive Quality Gate

Before marking a frontend story complete, verify:

```text
320px
375px
768px
1024px
1440px
```

No page-level horizontal overflow.

---

# 87. Codex Rule — Security

Do not:

- Store raw card data.
- Log secrets.
- Expose stack traces.
- Trust frontend role checks.
- Commit credentials.
- Use weak password storage.

---

# 88. Codex Recommended Build Order

Implement in this order:

```text
1. Project foundation
2. Branch
3. Court
4. Court UI
5. Operating hours
6. Court reservation
7. Availability
8. Booking hold
9. Concurrency protection
10. Pricing
11. Checkout
12. Payment abstraction
13. Mock payment
14. Production payment adapter
15. Confirmation
16. My bookings
17. Cancellation
18. Rescheduling
19. Admin booking calendar
20. Court maintenance
21. Walk-in booking
22. Check-in
23. RBAC
24. Audit
25. Outbox
26. Notifications
27. Reporting
28. Production hardening
```

---

# 89. Development Definition of Success

The development program is successful when a customer can:

```text
Open the app
↓
Choose branch
↓
Choose date/time
↓
See available courts
↓
Select a court
↓
Create a temporary hold
↓
Review server-generated price
↓
Pay
↓
Receive confirmation
↓
View booking
↓
Cancel/reschedule according to policy
```

and staff can:

```text
View schedule
Create walk-in booking
Block court
Schedule maintenance
Check customer in
Process allowed refunds
```

while the system guarantees:

```text
No confirmed double booking
Retry-safe payments
Auditable administrative actions
Recoverable failures
```

---

# 90. Final Engineering Recommendation

The project should optimize for:

```text
Correctness
Simplicity
Testability
Operational reliability
```

before optimizing for architectural novelty.

The recommended engineering approach is:

> **Build a well-tested modular monolith, enforce court reservation safety in PostgreSQL, use Redis only as an optimization, isolate payment integrations behind ports, implement retry-safe workflows, and deliver the product through vertical slices.**

This approach provides fast delivery for the MVP while maintaining production-grade foundations for future scale.

---

## End of Senior Software Engineering Development Plan
