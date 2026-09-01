# Pickleball Court Booking Platform
## Product Requirements & Requirements Gathering Document

### 1. Product Vision

Build a digital platform that allows players to quickly discover pickleball courts, visually inspect each court, see real-time availability, reserve a time slot, pay, receive confirmation, and manage their bookings.

Venue administrators should be able to manage courts, operating hours, pricing, maintenance schedules, promotions, bookings, payments, customers, and business reports from one system.

---

## 2. Primary Business Objectives

The platform should:

- Increase court utilization.
- Reduce manual reservations through calls, Facebook messages, or walk-ins.
- Prevent double booking.
- Allow customers to understand exactly which court they are reserving.
- Give customers a visual representation of available courts.
- Provide real-time slot availability.
- Automate reservation confirmation.
- Collect payments or deposits online.
- Reduce administrative workload.
- Track revenue and occupancy.
- Improve customer retention.
- Allow management to make pricing decisions based on usage.
- Support expansion into multiple branches in the future.

### Key Success Metrics

Track:

- Court occupancy/utilization %
- Booking conversion rate
- Revenue per court
- Revenue per available court-hour
- Bookings per day/week/month
- Average booking duration
- Average booking value
- Cancellation rate
- No-show rate
- Repeat customer rate
- Peak/off-peak utilization
- Online vs walk-in bookings
- Payment success rate
- Promotion usage
- Customer acquisition source
- Customer satisfaction/NPS

---

## 3. User Types

### 3.1 Guest

Can:

- View venue information
- View courts
- View photos
- Check availability
- See prices
- View amenities
- Start a booking
- Register/login

Whether guest checkout is allowed should be confirmed.

### 3.2 Registered Player

Can:

- Maintain profile
- Search courts
- View real-time availability
- Book courts
- Pay online
- Add other players
- Apply promotions
- Receive confirmations
- Cancel/reschedule
- View booking history
- Download receipts
- Join waitlists
- Save favorite courts

### 3.3 Staff / Receptionist

Can:

- Create walk-in bookings
- Search customers
- Check players in
- Accept manual payments
- Extend bookings
- Transfer bookings between courts
- Mark no-shows
- View today's schedule

Permissions should be restricted from sensitive financial/administrative settings.

### 3.4 Court Manager

Can:

- Manage courts
- Manage operating schedules
- Block courts
- Schedule maintenance
- Override bookings
- Configure pricing
- Manage promotions
- Review occupancy
- Resolve booking conflicts

### 3.5 Administrator / Owner

Has complete access including:

- Branch management
- User management
- Financial reports
- Refund management
- Pricing
- Promotions
- Permissions
- Audit logs
- Configuration
- Analytics

---

## 4. Court Information Requirements

Every physical court should exist as an individually configurable resource.

Example:

- Court 01
- Court 02
- Court 03
- Court 04
- Court 05
- Court 06

Each court should contain:

- Court ID
- Court number
- Court name
- Branch/location
- Court type
- Indoor/outdoor
- Playing surface
- Court dimensions
- Maximum players
- Lighting availability
- Air conditioning/fans
- Roof/covered status
- Accessibility information
- Equipment availability
- Net type
- Seating availability
- Locker availability
- Shower availability
- Nearby parking
- Hourly rate
- Peak-hour rate
- Off-peak rate
- Weekend rate
- Holiday rate
- Minimum booking duration
- Maximum booking duration
- Advance booking limit
- Cancellation policy
- Court photographs
- Court thumbnail
- Court location inside the facility
- Court status

Possible court statuses:

- Available
- Reserved
- Occupied
- Maintenance
- Temporarily unavailable
- Event reserved
- Closed

---

## 5. Visual Court Representation

A major requirement should be a visual representation of the venue.

Example:

```text
[ Court 1 ] [ Court 2 ] [ Court 3 ]

[ Court 4 ] [ Court 5 ] [ Court 6 ]
```

Each court should visibly show:

- Court number
- Court name
- Court image
- Indoor/outdoor indicator
- Price
- Selected time
- Availability status
- Next available time
- Amenities
- Surface type

Recommended visual statuses:

- AVAILABLE — clickable
- BOOKED — unavailable
- SELECTED — customer's currently selected court
- MAINTENANCE — blocked by staff
- EVENT — reserved for tournament/private event

Do not depend exclusively on color. Include text/icon labels for accessibility.

Clicking a court should open:

- Court photos
- Description
- Amenities
- Price
- Schedule
- Availability
- Rules
- Capacity
- **Book this Court**

---

## 6. Main Customer Booking Journey

### Step 1 — Choose Location

If multiple venues exist, select:

- City
- Branch
- Nearby venue

Future enhancement: use map-based venue discovery.

### Step 2 — Select Date

Examples:

- Today
- Tomorrow
- Calendar date

Rules must account for:

- Operating hours
- Holidays
- Maintenance
- Special events
- Advance reservation limits

### Step 3 — Select Time

Customer chooses:

- Start time
- Duration

Example durations:

- 30 minutes
- 60 minutes
- 90 minutes
- 120 minutes

Administrators determine which durations are allowed.

### Step 4 — Display Available Courts

The system queries the availability engine.

Example:

- Court 1 — Available — ₱500/hr
- Court 2 — Booked
- Court 3 — Available — ₱600/hr
- Court 4 — Maintenance
- Court 5 — Available — ₱700/hr

Customer can switch between:

- Visual court layout
- Court cards
- Schedule/timeline view

---

## 7. Availability Engine

The availability engine is one of the most important parts of the system.

Availability must consider:

```text
Court operating schedule
+ Existing bookings
+ Maintenance blocks
+ Private events
+ Tournament schedules
+ Staff-created blocks
+ Holiday schedules
+ Booking buffer
= Available booking slots
```

The system must prevent overlapping reservations.

Example:

Existing reservation:

```text
10:00 AM – 11:30 AM
```

Another customer attempting:

```text
11:00 AM – 12:00 PM
```

must receive:

> Selected court is no longer available.

---

## 8. Booking Lock / Concurrency Requirement

Two customers may attempt to reserve the same court simultaneously.

The system should temporarily lock a court slot during checkout.

Example:

```text
Customer A selects:
Court 3
7:00 PM–8:00 PM
```

System places approximately a 5–10 minute temporary reservation.

Customer B should see:

> Temporarily held

If Customer A fails to complete checkout, the slot automatically becomes available again.

The exact hold duration must be configurable.

---

## 9. Booking Details

A reservation should contain:

- Booking reference number
- Customer
- Branch
- Court
- Booking date
- Start time
- End time
- Duration
- Number of players
- Player names if required
- Base price
- Add-ons
- Discounts
- Taxes
- Fees
- Deposit
- Amount paid
- Outstanding balance
- Payment status
- Booking status
- Creation date
- Booking source
- Promo code
- Notes

Booking source examples:

- Mobile
- Web
- Reception
- Walk-in
- Admin
- Partner

---

## 10. Booking Statuses

Recommended booking lifecycle:

```text
DRAFT
→ HELD
→ PENDING_PAYMENT
→ CONFIRMED
→ CHECKED_IN
→ IN_PROGRESS
→ COMPLETED
```

Other possible states:

- CANCELLED
- EXPIRED
- NO_SHOW
- REFUNDED
- PARTIALLY_REFUNDED
- RESCHEDULED

Status changes should be recorded in an audit trail.

---

## 11. Pricing Engine

Pricing should not simply be stored as one court price.

The platform should eventually support pricing rules.

Examples:

```text
Weekday rate
₱500/hour

Weekend rate
₱650/hour

Peak time
6 PM–10 PM
₱750/hour

Off-peak promotion
10 AM–3 PM
₱400/hour
```

Possible pricing variables:

- Court
- Branch
- Day
- Time
- Duration
- Customer membership
- Holiday
- Event
- Promotion
- Number of players

Management should be able to configure pricing without code changes.

---

## 12. Add-On Services

Potential add-ons:

- Paddle rental
- Ball rental/purchase
- Locker rental
- Towel
- Drinking water
- Sports drinks
- Coaching
- Ball machine
- Referee
- Tournament package
- Function room
- Equipment package

Each add-on should support:

- Name
- Description
- Price
- Inventory
- Maximum quantity
- Applicable courts
- Availability

---

## 13. Checkout

Booking summary should display:

```text
COURT 3

September 10
6:00 PM – 8:00 PM

2 hours

Court fee: ₱1,200
Paddle rental: ₱200
Discount: -₱100
Service fee: ₱50

TOTAL: ₱1,350
```

Customer should explicitly confirm:

- Court
- Date
- Time
- Price
- Cancellation policy

before payment.

---

## 14. Payment Requirements

Determine whether the business will accept:

- Full payment
- Deposit
- Pay at venue
- Membership credits
- Wallet balance

Potential payment methods depending on market:

- Credit/debit card
- E-wallet
- Bank transfer
- QR payment
- Cash
- POS payment

Payment statuses:

- Unpaid
- Pending
- Paid
- Failed
- Partially paid
- Refunded
- Partially refunded

Required payment records:

- Transaction ID
- Gateway reference
- Customer
- Booking
- Amount
- Payment method
- Date
- Status
- Refund information

Never store raw card information in the application.

---

## 15. Booking Confirmation

Upon successful reservation, customer receives:

- Booking reference
- QR code
- Court
- Date
- Time
- Duration
- Venue address
- Payment status
- Rules
- Cancellation information

Possible notification channels:

- Email
- SMS
- Push notification
- Messaging application

---

## 16. QR Check-In

Optional but strongly recommended.

Each confirmed booking generates a QR code.

At venue:

```text
Customer presents QR code
→ Staff scans
→ System displays booking
→ Staff selects CHECK IN
```

System example:

```text
BOOKING VERIFIED

Court 5
7:00 PM–8:30 PM
4 Players
PAID
```

---

## 17. Cancellation Requirements

Requirements to confirm:

How long before a reservation can be cancelled?

Example:

- 24+ hours — 100% refund
- 6–24 hours — 50% refund
- <6 hours — non-refundable

Administrators should configure:

- Cancellation window
- Cancellation fee
- Refund percentage
- Store credit option
- No-show penalty

---

## 18. Rescheduling

Customers may be allowed to change:

- Date
- Time
- Court

The system must recheck availability before completing rescheduling.

If the new court costs more, collect additional payment.

If cheaper, provide refund/store credit depending on business policy.

---

## 19. Waitlist

If a court/time is unavailable, users may select:

> Notify me if this slot becomes available.

The system stores:

- Customer
- Court preference
- Date
- Preferred time
- Duration

If cancellation occurs, eligible customers can be notified.

Advanced version could provide the slot to the first waitlisted customer for a limited time.

---

## 20. Recurring Reservations

Useful for clubs, teams, coaches and leagues.

Example:

```text
Every Tuesday
7 PM–9 PM
Court 2
Next 8 weeks
```

System should check every requested occurrence.

Any conflict should be clearly displayed before confirmation.

---

## 21. Membership Support

Future requirement.

Membership examples:

- Regular
- Premium
- Club
- Corporate

Benefits could include:

- Discounted rates
- Priority booking
- Longer advance reservation
- Free equipment rental
- Reward points
- Monthly court credits

---

## 22. Promotions

Admin can create:

- Promo code
- First booking discount
- Birthday promotion
- Off-peak promotion
- Membership discount
- Buy X hours/get Y hours
- Referral discount

Promotion fields:

- Code
- Type
- Value
- Start date
- Expiration
- Usage limit
- Per-user limit
- Applicable branches
- Applicable courts
- Minimum amount

---

## 23. Admin Court Management

Administrator should be able to create/edit:

```text
COURT 1

Status: Active
Type: Indoor
Surface: Acrylic
Rate: ₱600/hr
Capacity: 4
Opening hours: 7 AM–11 PM

Features:
- Lighting
- Air conditioning
- Seating
```

Admin can:

- Upload photos
- Change pricing
- Disable court
- Block time
- Schedule maintenance
- Add operating hours

---

## 24. Court Blocking / Maintenance

Example:

```text
Court 4
September 12
12:00 PM–4:00 PM
Reason: Surface maintenance
```

The system should immediately remove the affected slots from customer availability.

If existing customers are affected, administrators should receive a warning and customers may require:

- Rescheduling
- Refund
- Alternative court

---

## 25. Calendar / Scheduler for Staff

Staff should have a visual daily schedule.

Example:

```text
COURT 1
8 AM  █ BOOKED
9 AM  █ BOOKED
10 AM ░ AVAILABLE
11 AM ░ AVAILABLE

COURT 2
8 AM  ░ AVAILABLE
9 AM  █ BOOKED
10 AM █ BOOKED
11 AM ░ AVAILABLE
```

Staff should be able to view:

- Day
- Week
- Court
- Booking status
- Customer
- Payment status

---

## 26. Walk-In Booking

Reception should be able to create reservations.

Workflow:

```text
Customer arrives
→ Staff chooses available court
→ Enter customer details
→ Select duration
→ Add rentals
→ Accept payment
→ Confirm booking
```

Walk-in bookings use the same availability engine to prevent conflicts.

---

## 27. Customer Profile

Store:

- Customer ID
- Name
- Email
- Mobile number
- Date of birth if required
- Emergency contact if required
- Membership
- Preferred branch
- Favorite courts
- Booking history
- Payment history
- Credits
- Reward points

Collect only information necessary for the business.

---

## 28. Notifications

System notifications should include:

### Booking Confirmation
Immediately after successful reservation.

### Booking Reminder
Possible schedule:

- 24 hours before
- 2 hours before

### Cancellation
When reservation is cancelled.

### Rescheduling
When reservation changes.

### Payment Receipt
After successful payment.

### Waitlist Availability
When requested slot becomes available.

### Maintenance Impact
If facility changes affect the customer's booking.

---

## 29. Admin Dashboard

Recommended dashboard cards:

```text
TODAY'S BOOKINGS
42

COURT UTILIZATION
78%

TODAY'S REVENUE
₱34,500

AVAILABLE COURTS NOW
3 / 8

CANCELLATIONS
4
```

Upcoming schedule should also be visible.

---

## 30. Reporting

### Revenue

- Daily revenue
- Weekly revenue
- Monthly revenue
- Revenue by branch
- Revenue by court
- Revenue by payment type

### Booking Analytics

- Bookings by court
- Bookings by hour
- Peak hours
- Off-peak hours
- Average duration
- Cancellation rate
- No-show rate

### Customer Analytics

- New customers
- Returning customers
- Most active customers
- Membership usage

### Court Analytics

- Utilization by court
- Downtime
- Maintenance hours
- Revenue per court

Reports should support CSV/Excel export if required.

---

## 31. Search & Filters

Customer search criteria may include:

- Date
- Time
- Duration
- Branch
- Indoor/outdoor
- Price
- Court type
- Amenities
- Available courts only

---

## 32. Multi-Branch Support

The architecture should preferably support multiple branches from the beginning even if launch starts with one venue.

```text
COMPANY
→ BRANCH
→ COURT
→ SCHEDULE
```

Example:

```text
PickleHub

├── Makati Branch
│   ├── Court 1
│   ├── Court 2
│   └── Court 3
│
└── BGC Branch
    ├── Court 1
    ├── Court 2
    └── Court 3
```

---

## 33. Role-Based Access Control

Example permission matrix:

- Customer: Own bookings only
- Reception: Bookings + check-in
- Court Manager: Bookings + courts + scheduling
- Finance: Payments + reports + refunds
- Admin: Everything
- Owner: Everything + executive analytics

Important administrative changes should create audit records.

---

## 34. Audit Trail

Track actions such as:

- Booking creation
- Booking cancellation
- Booking modification
- Payment update
- Refund
- Court closure
- Price change
- Manual override
- User permission change

Record:

- WHO
- WHAT
- WHEN
- OLD VALUE
- NEW VALUE

---

## 35. Non-Functional Requirements

### Performance

Typical pages should load quickly.

Availability searches should ideally return within approximately 1–2 seconds under normal operating conditions.

### Reliability

The system must not create duplicate reservations.

Database transactions and concurrency control should protect booking integrity.

### Scalability

Architecture should support:

- Additional courts
- Additional locations
- Higher user traffic
- Mobile applications
- League/tournament modules

### Security

Require:

- HTTPS
- Secure authentication
- Password hashing
- Session/token security
- Rate limiting
- Role permissions
- Audit logging
- Input validation
- Secure payment gateway
- Protection against common OWASP vulnerabilities

### Availability

Target production availability should be established.

Example:

```text
99.9%
```

### Backup

Define:

- Database backup frequency
- Retention period
- Disaster recovery process
- Recovery Point Objective
- Recovery Time Objective

---

## 36. Privacy Requirements

Determine applicable local privacy regulations.

The platform should define:

- Privacy policy
- Data retention
- Account deletion
- Data export
- Marketing consent
- Notification consent
- Payment data responsibilities

Only required personal data should be collected.

---

## 37. Core Data Model

Recommended major entities:

- USER
- CUSTOMER_PROFILE
- ROLE
- PERMISSION
- BRANCH
- COURT
- COURT_IMAGE
- COURT_AMENITY
- OPERATING_HOURS
- COURT_AVAILABILITY
- COURT_BLOCK
- BOOKING
- BOOKING_PLAYER
- BOOKING_ADDON
- BOOKING_HISTORY
- PAYMENT
- REFUND
- PRICING_RULE
- PROMOTION
- MEMBERSHIP
- MEMBERSHIP_PLAN
- WAITLIST
- NOTIFICATION
- AUDIT_LOG
- MAINTENANCE
- CHECK_IN
- REVIEW

---

## 38. Suggested High-Level Architecture

```text
Customer Web / Mobile App
          ↓
      API Gateway
          ↓
 ┌────────────────────┐
 │ Authentication     │
 │ Booking Service    │
 │ Availability       │
 │ Pricing Service    │
 │ Payment Service    │
 │ Notification       │
 └────────────────────┘
          ↓
       Database
```

External integrations may include:

- Payment Gateway
- Email Provider
- SMS Provider
- Push Notifications
- Analytics

---

## 39. Main API Domains

Potential API structure:

```text
/auth
/users
/customers
/branches
/courts
/courts/{id}/availability
/bookings
/bookings/{id}/cancel
/bookings/{id}/reschedule
/payments
/refunds
/promotions
/addons
/waitlist
/check-in
/admin/reports
/admin/courts
/admin/pricing
/admin/maintenance
```

---

## 40. MVP Scope

### Customer

- Registration/login
- Browse courts
- Court images
- Visual court layout
- Select date/time
- Real-time availability
- Select court
- Book court
- Checkout
- Payment
- Booking confirmation
- Email notification
- My bookings
- Cancellation

### Staff/Admin

- Login
- Court management
- Operating schedules
- Booking management
- Walk-in reservation
- Court blocking
- Maintenance
- Check-in
- Customer lookup
- Payment tracking
- Basic reports

---

## 41. Phase 2

Add:

- QR check-in
- Waitlist
- Promo codes
- Equipment rental
- Reviews
- Memberships
- Loyalty rewards
- Advanced pricing
- Push notifications

---

## 42. Phase 3

Add:

- Recurring reservations
- Coaches
- Lessons
- League management
- Tournament management
- Matchmaking
- Player ratings
- Community features
- Corporate accounts
- Dynamic pricing
- AI utilization recommendations

---

## 43. Critical User Stories

### Court Discovery

**As a player,**  
I want to see all courts visually,  
so that I know exactly which court I am reserving.

Acceptance criteria:

- Every active court is displayed.
- Court number/name is visible.
- Court status is visible.
- Indoor/outdoor type is displayed.
- Price is displayed.
- Available courts can be selected.
- Unavailable courts cannot be booked.

### Availability

**As a player,**  
I want to see available courts for my chosen date and time,  
so that I do not attempt to reserve an unavailable court.

Acceptance criteria:

- Availability reflects confirmed bookings.
- Maintenance blocks are excluded.
- Event blocks are excluded.
- Expired checkout holds are released.
- Overlapping bookings cannot be created.

### Booking

**As a customer,**  
I want to reserve an available court,  
so that the court is guaranteed for my selected time.

Acceptance criteria:

- Court remains temporarily locked during checkout.
- Booking information is reviewed before payment.
- Successful payment creates a confirmed reservation.
- Confirmation number is generated.
- Customer receives confirmation.

### Administrative Blocking

**As a manager,**  
I want to block a court for maintenance,  
so that customers cannot reserve it.

Acceptance criteria:

- Manager selects court/date/time.
- Reason is recorded.
- Availability immediately updates.
- Existing conflicts trigger a warning.

---

## 44. Important Edge Cases

Requirements must specifically cover:

1. Two customers booking the same court simultaneously.
2. Payment succeeds but booking confirmation fails.
3. Booking succeeds but payment provider callback is delayed.
4. Customer closes browser during payment.
5. Admin blocks a court containing existing bookings.
6. Customer attempts to book a past time.
7. Customer crosses midnight during booking.
8. Booking occurs during operating-hour changes.
9. Daylight-saving/timezone situations for international expansion.
10. Refund fails.
11. Customer reschedules repeatedly.
12. Internet connection drops during booking.
13. Price changes after the customer starts checkout.
14. Promo expires during checkout.
15. Court becomes unavailable after customer begins checkout.
16. Duplicate payment callbacks.
17. Staff accidentally creates duplicate walk-in booking.
18. Customer arrives late.
19. Customer wants to extend the session while the next slot is booked.
20. Facility closes due to emergency/weather.

---

## 45. Stakeholder Requirements-Gathering Questionnaire

### Business

1. How many branches exist?
2. How many courts per branch?
3. Is expansion to additional branches expected?
4. What percentage of bookings currently happen online, by phone, social media, and walk-in?
5. What problems are staff experiencing today?
6. What is the primary business goal?
7. What KPIs define success?

### Court Operations

8. What are operating hours?
9. Do different courts have different schedules?
10. Are courts indoor/outdoor?
11. Do courts have different prices?
12. Are courts physically identical?
13. How frequently are courts maintained?
14. How are courts currently blocked?
15. Is buffer time required between reservations?

### Reservations

16. Minimum reservation duration?
17. Maximum duration?
18. Booking interval: 30/60 minutes?
19. Maximum advance booking period?
20. Minimum advance notice?
21. Can customers extend bookings?
22. Can multiple courts be booked together?
23. Are recurring bookings allowed?
24. Are guests allowed to book without creating accounts?

### Pricing

25. Standard rates?
26. Peak rates?
27. Weekend rates?
28. Holiday rates?
29. Member pricing?
30. Student/senior discounts?
31. Promo codes?
32. Deposit required?
33. Taxes/service fees?

### Payments

34. Required payment methods?
35. Full payment or deposit?
36. Can customers pay at the venue?
37. Automatic refunds required?
38. Who can approve refunds?
39. Is store credit allowed?

### Cancellation

40. Cancellation window?
41. Cancellation fee?
42. Refund percentage?
43. No-show policy?
44. Rescheduling rules?

### Equipment

45. Are paddles rented?
46. Balls rented/sold?
47. Inventory tracking required?
48. Other services/add-ons?

### Customer Experience

49. Email confirmation required?
50. SMS?
51. Push notifications?
52. Booking reminders?
53. QR check-in?
54. Reviews?
55. Loyalty points?
56. Membership program?

### Staff Operations

57. Who manages bookings?
58. Who collects payments?
59. Who can cancel bookings?
60. Who can override schedules?
61. Who can change pricing?
62. Are tablets/computers available at reception?

### Reporting

63. Which financial reports are required?
64. Which occupancy reports?
65. Daily closing report?
66. Tax reports?
67. Export to Excel?
68. Accounting integration required?

### Technical

69. Web only or mobile app?
70. iOS/Android required?
71. Existing website?
72. Existing POS?
73. Existing payment gateway?
74. Existing customer database?
75. Existing accounting software?
76. Expected users/bookings per day?
77. Required languages?
78. Required currencies?
79. Required privacy/compliance standards?

---

## 46. Definition of MVP Success

The MVP can be considered successful when a customer can complete this entire journey without staff assistance:

```text
OPEN APP
→ SELECT LOCATION
→ CHOOSE DATE
→ CHOOSE TIME
→ SEE VISUAL COURT AVAILABILITY
→ SELECT COURT
→ REVIEW PRICE
→ PAY
→ RECEIVE CONFIRMATION
→ ARRIVE AT VENUE
→ CHECK IN
```

while the system guarantees that the same court/time cannot be sold to another customer.

---

## 47. Recommended Product Principle

The central user experience should answer one question immediately:

> **Which courts can I play on at the time I want?**

Therefore the home booking experience should prioritize:

**DATE + TIME + COURT VISUALIZATION + PRICE**

rather than forcing the customer through several screens before showing availability.
