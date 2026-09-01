# Pickleball Court Booking Platform
## Senior UI/UX Engineering Plan + Codex Implementation Instructions

**Recommended Stack:** Next.js + TypeScript + Tailwind CSS  
**Frontend Style:** Modern premium sports booking platform  
**Primary Experience:** Search → View Court Availability → Select Court → Select Time → Review → Checkout

---

# 1. Product UI/UX Vision

Design the product as a modern, premium, frictionless booking experience inspired by best-in-class reservation platforms.

The interface should feel:

- Modern
- Premium but approachable
- Fast
- Sporty
- Clean
- Trustworthy
- Mobile-first
- Highly visual
- Easy to scan
- Accessible

The most important product question should be answered immediately:

> **Which pickleball courts are available at the time I want, and how much will they cost?**

The application should prioritize:

1. Location
2. Date
3. Start time
4. Duration
5. Available courts
6. Court visual representation
7. Price
8. Booking confirmation

Avoid unnecessary screens before court availability is shown.

---

# 2. UX Principles

## 2.1 Availability First

Court availability should be the center of the experience.

Users should not need to:

- Create an account before viewing availability
- Open multiple pages to compare courts
- Guess whether a court is booked
- Call staff to verify a reservation

Show availability clearly and in real time.

---

## 2.2 Visual Court Selection

The user must be able to visually identify the court they are booking.

Each court card should communicate:

- Court name
- Court number
- Court type
- Indoor/outdoor
- Surface
- Price
- Rating if supported
- Amenities
- Availability
- Court preview
- Selected state

A venue may also have a visual court-layout mode.

Example:

```text
┌─────────────────────────────────────────────────────────────┐
│                        PLAYER LOUNGE                        │
├───────────────────┬───────────────────┬────────────────────┤
│     COURT 01      │     COURT 02      │      COURT 03      │
│    AVAILABLE      │      BOOKED       │     AVAILABLE      │
├───────────────────┼───────────────────┼────────────────────┤
│     COURT 04      │     COURT 05      │      COURT 06      │
│   MAINTENANCE     │     AVAILABLE     │      EVENT         │
└───────────────────┴───────────────────┴────────────────────┘
```

---

## 2.3 Progressive Disclosure

Do not overwhelm users.

Show the essential information first.

Court cards initially show:

- Name
- Type
- Price
- Availability
- Main amenities

Court details can reveal:

- Full amenity list
- Rules
- Photos
- Surface
- Capacity
- Cancellation policy
- Location within venue

---

## 2.4 Persistent Booking Context

Once a user selects booking parameters, keep them visible.

Desktop:

Use a sticky booking summary sidebar.

Mobile:

Use a sticky bottom booking summary / CTA.

Users should always know:

- Selected venue
- Selected court
- Date
- Time
- Duration
- Total

---

# 3. Recommended Visual Direction

## Brand Personality

Use a combination of:

- Athletic energy
- Premium sports club feel
- Calm booking interface
- Modern SaaS-level polish

Avoid overly aggressive sports styling.

The application should look suitable for:

- Families
- Casual players
- Competitive players
- Corporate groups
- Coaches
- Clubs

---

# 4. Recommended Color System

Use semantic Tailwind design tokens rather than scattering hard-coded values throughout components.

Suggested palette:

## Primary

Pickle / court green:

```text
Primary 50   #ECFDF5
Primary 100  #D1FAE5
Primary 200  #A7F3D0
Primary 300  #6EE7B7
Primary 400  #34D399
Primary 500  #10B981
Primary 600  #059669
Primary 700  #047857
Primary 800  #065F46
Primary 900  #064E3B
```

Recommended primary button:

```text
#059669
```

## Accent

Use a yellow-green accent sparingly for:

- Availability badges
- Important sports highlights
- Promotional elements

Example:

```text
#A3E635
```

Do not use the accent as a large background color.

## Neutral

Use Tailwind slate/gray tones.

Suggested:

```text
Background     slate-50
Surface        white
Border         slate-200
Primary text   slate-950
Secondary text slate-600
Muted text     slate-500
```

## Status Colors

Available:

```text
emerald-600
emerald-50
```

Booked:

```text
slate-500
slate-100
```

Maintenance:

```text
amber-600
amber-50
```

Error / cancellation:

```text
red-600
red-50
```

Selected:

```text
emerald-600 border
emerald-50 background
```

Do not communicate status using color alone.

Always pair status colors with:

- Text
- Icon
- Label

---

# 5. Typography

Recommended:

```text
Inter
Geist
```

For a pure Next.js solution, Geist is an excellent default.

Typography hierarchy:

## H1

```text
text-3xl md:text-4xl
font-bold
tracking-tight
```

## H2

```text
text-xl md:text-2xl
font-semibold
tracking-tight
```

## H3

```text
text-lg
font-semibold
```

## Body

```text
text-sm md:text-base
leading-6
```

## Supporting Text

```text
text-sm
text-slate-500
```

Avoid excessive small text.

Minimum mobile input text should generally be:

```text
text-base
```

to avoid iOS zoom behavior.

---

# 6. Spacing and Layout

Use a consistent spacing system.

Recommended main page:

```text
max-w-7xl
mx-auto
px-4
sm:px-6
lg:px-8
```

Desktop layout:

```text
Main Booking Content: 1fr
Booking Summary: 320px–360px
```

Example:

```tsx
<div className="grid gap-8 lg:grid-cols-[minmax(0,1fr)_340px]">
```

Use:

- 16px minimum mobile page padding
- 24–32px major section spacing
- 12–16px card internal spacing
- 44px minimum touch targets

---

# 7. Responsive Strategy

The UI must work from approximately 320px wide upward.

## Mobile

Priority layout:

```text
Header
↓
Search filters
↓
Availability summary
↓
Court cards
↓
Time slots
↓
Sticky booking CTA
```

Court cards:

```text
1 column
```

## Tablet

Court cards:

```text
2 columns
```

## Desktop

Court cards:

```text
2 or 3 columns
```

Booking summary:

Sticky right sidebar.

Example:

```text
lg:sticky
lg:top-6
```

Do not use fixed heights for the page.

---

# 8. Primary Navigation

Desktop:

```text
Logo

Book a Court
Locations
Membership
Events

----------------

Bookings
Profile
```

Mobile:

Use:

```text
Logo
Menu
```

Avoid overcrowded navigation.

For MVP, navigation can be simplified to:

```text
Book
My Bookings
Account
```

---

# 9. Main Booking Page

Recommended URL:

```text
/book
```

Page hierarchy:

```text
Header

Hero / Booking Introduction

Booking Search Bar

Availability Heading
Court Filters

Court Grid

Available Time Slots

Booking Summary

Footer
```

---

# 10. Hero Section

Do not make the hero too large.

The booking workflow must remain visible above or close to the fold.

Recommended content:

```text
Find your perfect court.

Book available pickleball courts instantly.
See live availability, pricing, and court details before checkout.
```

Supporting badges:

```text
Instant booking
Real-time availability
Secure checkout
```

Desktop height should remain compact.

---

# 11. Booking Search Component

Component:

```text
BookingSearch
```

Fields:

```text
Location
Date
Start Time
Duration
Players
```

Desktop:

Single row or 4–5 column grid.

Mobile:

Stack fields.

Recommended component behavior:

- Use native date input initially
- Use select/dropdown for time
- Use select for duration
- Players optional for MVP
- Update results without navigating away
- Debounce only if network request is required

Example:

```tsx
<BookingSearch
  location={location}
  date={date}
  startTime={startTime}
  duration={duration}
  players={players}
/>
```

---

# 12. Court Filters

Recommended filters:

```text
All Courts
Indoor
Outdoor
Premium
Available Only
```

Optional future filters:

```text
Price
Amenities
Surface
Air-conditioned
Covered
```

Use pill buttons.

Active filter:

```text
bg-emerald-50
border-emerald-600
text-emerald-800
```

Inactive:

```text
border-slate-200
bg-white
text-slate-700
```

---

# 13. Court Card

Component:

```text
CourtCard
```

Each card should show:

```text
Court Image / Court Illustration

Indoor / Outdoor Badge
Rating

Court Name
Surface

Amenities

Availability

Price / hour

Select Court
```

Recommended structure:

```text
┌─────────────────────────────┐
│        COURT VISUAL         │
│ Indoor            ★ 4.9    │
│                             │
│ Court One                   │
│ Pro Acrylic                 │
│                             │
│ AC     Seating     Lights   │
│                             │
│ ● Available      ₱650/hr    │
└─────────────────────────────┘
```

Selected court:

```text
border-emerald-600
ring-2
ring-emerald-100
```

Booked court:

- Reduced opacity
- Disabled interaction
- Visible "Booked" badge

Maintenance:

- Amber status
- Disabled
- Optional maintenance reason

---

# 14. Court Visual Representation

Create an optional component:

```text
CourtLayoutView
```

This is different from CourtCard.

Its purpose is to show physical court positioning inside the venue.

Example:

```tsx
<CourtLayoutView
  courts={courts}
  selectedCourtId={selectedCourtId}
  onCourtSelect={setSelectedCourtId}
/>
```

Each court tile should display:

```text
Court number
Status
Current price
```

Use CSS Grid.

Do not use canvas unless necessary.

Recommended layout data:

```ts
type CourtLayoutPosition = {
  row: number;
  column: number;
  rowSpan?: number;
  columnSpan?: number;
};
```

---

# 15. Court Details Drawer / Modal

When user selects "View details", open a dialog or drawer.

Desktop:

Modal.

Mobile:

Bottom sheet / full-screen dialog.

Content:

```text
Court images
Court name
Indoor/outdoor
Surface
Capacity
Amenities
Rules
Cancellation policy
Available times
Price
Select Court
```

Do not force the details modal before booking.

---

# 16. Time Slot Selector

Component:

```text
TimeSlotGrid
```

Recommended design:

```text
8:00 AM
9:00 AM
10:00 AM
11:00 AM
...
```

Use buttons.

Available:

```text
white
border-slate-200
```

Hover:

```text
border-emerald-500
```

Selected:

```text
bg-emerald-600
text-white
border-emerald-600
```

Unavailable:

```text
bg-slate-100
text-slate-400
cursor-not-allowed
```

Do not hide unavailable slots.

Showing unavailable times helps the user understand demand.

---

# 17. Booking Summary

Component:

```text
BookingSummary
```

Desktop:

Sticky sidebar.

Display:

```text
Selected Court
Venue
Date
Time
Duration
Players

Court Fee
Add-ons
Booking Fee
Discount

Total
```

CTA:

```text
Continue to Checkout
```

Before a court is selected:

```text
Select a court to continue
```

CTA disabled.

After selection:

CTA enabled.

---

# 18. Mobile Booking Summary

Do not place the entire desktop summary at the bottom of a very long page.

Use sticky bottom CTA:

```text
Court Three
₱1,090 total

[ Continue ]
```

Tap summary to expand details.

Use:

```text
sticky bottom-0
```

rather than `fixed` when practical.

---

# 19. Checkout Flow

Recommended route:

```text
/checkout
```

Steps:

```text
1. Booking
2. Details
3. Payment
4. Confirmation
```

Do not show unnecessary stepper complexity for a small MVP.

Checkout page:

```text
Customer Details

Player Count

Optional Add-ons

Payment Method

Booking Summary

Cancellation Agreement

Pay / Confirm Booking
```

---

# 20. Confirmation Page

Route:

```text
/booking/[bookingReference]/confirmation
```

Success state:

```text
✓ Booking Confirmed

Court Three

September 10, 2026
6:00 PM – 8:00 PM

Booking ID
PKL-260910-1234

[ View Booking ]
[ Add to Calendar ]
```

Optional:

QR code.

Show:

- Venue address
- Court
- Time
- Payment status
- Cancellation information

---

# 21. My Bookings

Route:

```text
/bookings
```

Tabs:

```text
Upcoming
Past
Cancelled
```

Booking card:

```text
Court Three
September 10
6 PM – 8 PM

CONFIRMED

Central Pickle Club

[ View ]
[ Reschedule ]
[ Cancel ]
```

---

# 22. Admin UI Direction

Admin route:

```text
/admin
```

Admin should feel like a modern SaaS dashboard, not the customer booking interface.

Navigation:

```text
Overview
Bookings
Calendar
Courts
Customers
Payments
Pricing
Promotions
Maintenance
Reports
Settings
```

---

# 23. Admin Dashboard

Cards:

```text
Today's Bookings
Court Utilization
Today's Revenue
Available Courts
Cancellations
```

Main section:

```text
Today's Court Schedule
```

Secondary:

```text
Revenue trend
Top courts
Peak hours
Recent bookings
```

---

# 24. Admin Schedule / Calendar

Route:

```text
/admin/bookings/calendar
```

Desktop scheduler example:

```text
             Court 1    Court 2    Court 3

08:00        BOOKED     AVAILABLE  BOOKED
09:00        BOOKED     BOOKED     AVAILABLE
10:00        AVAILABLE  BOOKED     AVAILABLE
11:00        AVAILABLE  AVAILABLE  BOOKED
```

Recommended implementation:

Use CSS Grid for MVP.

Do not immediately introduce a heavyweight calendar library unless necessary.

---

# 25. Court Management

Route:

```text
/admin/courts
```

Table/card information:

```text
Court
Type
Surface
Rate
Status
Bookings Today
Actions
```

Actions:

```text
Edit
Block Time
Schedule Maintenance
View Calendar
```

---

# 26. Loading States

Every async section should have loading states.

Use skeletons for:

```text
Court cards
Booking summary
Availability
Dashboard metrics
```

Avoid full-screen spinners.

Example:

```tsx
<div className="animate-pulse rounded-2xl bg-slate-100" />
```

---

# 27. Empty States

Examples:

## No Courts Available

```text
No courts are available at this time.

Try:
• A different start time
• A shorter duration
• Another location

[ View Next Available Times ]
```

## No Upcoming Bookings

```text
You don't have any upcoming games.

[ Book a Court ]
```

---

# 28. Error States

Examples:

## Court Became Unavailable

```text
This court was just booked by another player.

We refreshed availability for you.

[ Choose Another Court ]
```

## Payment Failure

```text
Payment couldn't be completed.

Your court is still held for 04:32.

[ Try Again ]
```

---

# 29. Booking Hold UX

When a temporary court hold exists:

Display a visible checkout countdown.

Example:

```text
Court reserved for you

04:58 remaining
```

Do not create anxiety before checkout.

Only show countdown after the user explicitly begins reservation/checkout.

---

# 30. Accessibility Requirements

Minimum WCAG target:

```text
WCAG 2.1 AA
```

Requirements:

- Keyboard navigable
- Proper semantic buttons
- Visible focus states
- Labels for inputs
- Status text not color-only
- Sufficient contrast
- Dialog focus trapping
- Escape closes modal
- ARIA live regions for dynamic booking updates
- 44×44px touch targets
- Images contain alt text
- Form errors linked to inputs

---

# 31. Interaction Rules

Animations should be subtle.

Use:

```text
150–200ms
```

for:

- Hover
- Select
- Expand
- Modal transitions

Avoid excessive motion.

Respect:

```css
prefers-reduced-motion
```

---

# 32. Technology Architecture

Use:

```text
Next.js
TypeScript
Tailwind CSS
```

Recommended:

```text
Next.js App Router
```

Optional supporting libraries:

```text
lucide-react
clsx
tailwind-merge
zod
react-hook-form
date-fns
```

Do not install all libraries automatically.

Only add them when actually needed.

---

# 33. Next.js Project Structure

Recommended:

```text
src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   │
│   ├── book/
│   │   ├── page.tsx
│   │   └── loading.tsx
│   │
│   ├── checkout/
│   │   └── page.tsx
│   │
│   ├── bookings/
│   │   ├── page.tsx
│   │   └── [bookingId]/
│   │       └── page.tsx
│   │
│   └── admin/
│       ├── layout.tsx
│       ├── page.tsx
│       ├── bookings/
│       ├── courts/
│       ├── customers/
│       ├── payments/
│       ├── reports/
│       └── settings/
│
├── components/
│   ├── booking/
│   │   ├── booking-search.tsx
│   │   ├── court-card.tsx
│   │   ├── court-grid.tsx
│   │   ├── court-layout-view.tsx
│   │   ├── court-details-dialog.tsx
│   │   ├── court-filter.tsx
│   │   ├── time-slot-grid.tsx
│   │   ├── booking-summary.tsx
│   │   ├── mobile-booking-bar.tsx
│   │   └── availability-status.tsx
│   │
│   ├── checkout/
│   │   ├── customer-details-form.tsx
│   │   ├── add-on-selector.tsx
│   │   ├── payment-methods.tsx
│   │   └── checkout-summary.tsx
│   │
│   ├── admin/
│   │   ├── admin-sidebar.tsx
│   │   ├── metric-card.tsx
│   │   ├── booking-calendar.tsx
│   │   └── revenue-chart.tsx
│   │
│   ├── layout/
│   │   ├── header.tsx
│   │   ├── footer.tsx
│   │   └── mobile-navigation.tsx
│   │
│   └── ui/
│       ├── button.tsx
│       ├── badge.tsx
│       ├── card.tsx
│       ├── dialog.tsx
│       ├── input.tsx
│       ├── select.tsx
│       ├── skeleton.tsx
│       └── empty-state.tsx
│
├── lib/
│   ├── utils.ts
│   ├── booking.ts
│   ├── pricing.ts
│   └── mock-data.ts
│
├── types/
│   ├── court.ts
│   ├── booking.ts
│   └── availability.ts
│
└── styles/
    └── globals.css
```

---

# 34. TypeScript Models

Create shared models.

## Court

```ts
export type CourtStatus =
  | "AVAILABLE"
  | "BOOKED"
  | "MAINTENANCE"
  | "EVENT"
  | "CLOSED";

export interface Court {
  id: string;
  number: number;
  name: string;
  type: "INDOOR" | "OUTDOOR" | "PREMIUM";
  surface: string;
  hourlyRate: number;
  capacity: number;
  status: CourtStatus;
  rating?: number;
  imageUrl?: string;
  amenities: string[];
}
```

## Availability

```ts
export interface CourtAvailability {
  courtId: string;
  date: string;
  startTime: string;
  endTime: string;
  available: boolean;
  status: CourtStatus;
}
```

## Booking Draft

```ts
export interface BookingDraft {
  locationId: string;
  courtId?: string;
  date: string;
  startTime: string;
  durationMinutes: number;
  players: number;
}
```

---

# 35. Component State Strategy

For the first UI implementation:

Use local React state.

Example:

```ts
const [selectedCourtId, setSelectedCourtId] = useState<string | null>(null);
const [date, setDate] = useState("");
const [time, setTime] = useState("");
const [duration, setDuration] = useState(120);
```

Do not introduce Redux for the initial booking UI.

If booking state must persist across routes, consider:

```text
React Context
URL query parameters
server-backed draft booking
```

Recommended production strategy:

Store key booking search parameters in URL.

Example:

```text
/book?location=central&date=2026-09-10&time=18:00&duration=120
```

Benefits:

- Shareable
- Refresh-safe
- Browser back/forward friendly

---

# 36. Server vs Client Components

Default to Server Components.

Use Client Components only where interaction is required.

Client components:

```text
BookingSearch
CourtGrid
CourtCard selection
TimeSlotGrid
BookingSummary
CourtDetailsDialog
```

Server components:

```text
Page shell
Venue content
SEO metadata
Static content
Initial court fetch
```

Add:

```tsx
"use client";
```

only where needed.

---

# 37. Mock Data Requirements

Before backend integration, create:

```text
src/lib/mock-data.ts
```

Include:

- 6 courts
- Indoor/outdoor/premium types
- Different pricing
- Available/booked/maintenance states
- Amenities
- Time slots

Ensure mock states demonstrate:

- Available
- Selected
- Booked
- Maintenance
- Empty availability

---

# 38. Tailwind Component Conventions

Avoid huge repeated class strings.

Create reusable UI primitives.

Example button variants:

```ts
primary
secondary
ghost
danger
```

Recommended primary:

```text
bg-emerald-600
text-white
hover:bg-emerald-700
focus-visible:ring-2
focus-visible:ring-emerald-500
```

Card:

```text
rounded-2xl
border
border-slate-200
bg-white
```

Input:

```text
h-11
rounded-xl
border
border-slate-300
bg-white
px-3
text-base
```

---

# 39. Global Tailwind Styling

Recommended `globals.css`:

```css
@import "tailwindcss";

:root {
  --background: #f8fafc;
  --foreground: #0f172a;
}

body {
  background: var(--background);
  color: var(--foreground);
}
```

If the project uses Tailwind v3, configure through:

```text
tailwind.config.ts
```

Do not mix Tailwind v3 and v4 configuration styles.

---

# 40. Suggested Homepage

Route:

```text
/
```

For MVP, the homepage can redirect to:

```text
/book
```

or display:

```text
Hero
Quick booking widget
Popular venues
Why book with us
```

Do not spend excessive effort on marketing pages before the booking flow is complete.

---

# 41. Design Components

## Button

Required variants:

```text
Primary
Secondary
Ghost
Danger
```

## Badge

Variants:

```text
Available
Booked
Maintenance
Premium
Indoor
Outdoor
```

## Card

Use for:

- Courts
- Bookings
- Dashboard stats

## Dialog

Use for:

- Court details
- Cancellation
- Booking confirmation prompts

## Skeleton

Use for async content.

---

# 42. Icons

Recommended:

```text
lucide-react
```

Suggested icons:

```text
MapPin
CalendarDays
Clock
Users
ChevronDown
Check
CircleCheck
CircleX
Wrench
CreditCard
Search
SlidersHorizontal
Star
ArrowRight
QrCode
```

Do not use emoji in the production UI if Lucide icons are available.

---

# 43. Court Image Strategy

Production court cards should support photographs.

Use Next.js:

```tsx
import Image from "next/image";
```

Example:

```tsx
<Image
  src={court.imageUrl}
  alt={`${court.name} pickleball court`}
  fill
  className="object-cover"
/>
```

Use:

```text
aspect-[16/10]
```

for court imagery.

If images are unavailable, use a court illustration placeholder.

---

# 44. Court Illustration Fallback

Build a reusable visual placeholder using CSS.

Example:

```text
Court surface background
White court boundary
Center net
Subtle court number
```

Do not use generic gray image placeholders if the court has no photo.

The fallback should still feel branded.

---

# 45. Booking Flow State Diagram

```text
SEARCH
  ↓
VIEW_AVAILABILITY
  ↓
SELECT_COURT
  ↓
SELECT_TIME
  ↓
REVIEW
  ↓
HELD
  ↓
CHECKOUT
  ↓
PAYMENT
  ↓
CONFIRMED
```

Alternate states:

```text
PAYMENT_FAILED
EXPIRED
COURT_NO_LONGER_AVAILABLE
CANCELLED
```

---

# 46. Performance Requirements

Target:

```text
LCP < 2.5s
CLS < 0.1
INP < 200ms
```

Implementation considerations:

- Use Server Components
- Use Next Image
- Lazy-load non-critical images
- Avoid oversized client bundles
- Avoid unnecessary global state
- Use route-level loading UI
- Cache venue metadata where appropriate

---

# 47. SEO

Public venue pages should have metadata.

Example:

```text
/book
/locations/[slug]
```

Use:

```ts
export const metadata = {
  title: "...",
  description: "...",
};
```

Venue pages can contain:

- Venue name
- Address
- Amenities
- Court availability
- Pricing

---

# 48. UX Analytics Events

Prepare semantic events.

Examples:

```text
booking_search_submitted
court_filter_selected
court_selected
court_details_opened
time_slot_selected
checkout_started
payment_started
booking_confirmed
booking_failed
```

Payload example:

```ts
{
  courtId,
  locationId,
  date,
  startTime,
  duration
}
```

Do not place analytics implementation throughout visual components.

Use a central analytics helper.

---

# 49. Codex Implementation Instructions

The following section should be treated as direct implementation instructions for Codex.

---

# 50. CODEX MASTER INSTRUCTION

## Objective

Implement a production-quality frontend for a pickleball court booking platform using:

```text
Next.js
TypeScript
Tailwind CSS
```

The design must feel like a modern booking platform.

Prioritize:

```text
Court discovery
Live availability
Visual court representation
Fast booking
Clear pricing
Responsive UI
Accessibility
```

Do not build a generic admin-template-looking customer interface.

---

# 51. Codex Development Rules

Codex must follow these rules:

1. Use Next.js App Router.
2. Use TypeScript.
3. Use Tailwind CSS.
4. Prefer Server Components.
5. Use Client Components only for interactive UI.
6. Do not use Redux.
7. Avoid unnecessary dependencies.
8. Use reusable components.
9. Avoid monolithic page components.
10. Maintain strict type safety.
11. Build mobile-first.
12. Use semantic HTML.
13. Ensure keyboard accessibility.
14. Use clear loading and empty states.
15. Do not rely on color alone for booking status.
16. Make all buttons and controls functional.
17. Do not leave placeholder controls that do nothing.
18. Do not use lorem ipsum.
19. Do not hard-code the entire UI directly in a single `page.tsx`.
20. Do not create unnecessary abstractions before the UI works.

---

# 52. Codex Step 1 — Foundation

Create or validate:

```text
Next.js
TypeScript
Tailwind
App Router
```

Create:

```text
src/components
src/components/ui
src/components/booking
src/lib
src/types
```

Implement global styling.

Ensure:

```text
bg-slate-50
text-slate-950
```

as the default product surface.

---

# 53. Codex Step 2 — Shared UI Components

Implement:

```text
Button
Badge
Card
Input
Select
Skeleton
EmptyState
```

All components must:

- Accept `className`
- Be reusable
- Support focus states
- Avoid visual duplication

---

# 54. Codex Step 3 — Booking Data Models

Create:

```text
Court
CourtAvailability
BookingDraft
BookingPrice
```

Use literal unions for court and booking status.

Do not use `any`.

---

# 55. Codex Step 4 — Mock Data

Create six realistic courts.

Required states:

```text
3 available
1 booked
1 maintenance
1 premium available
```

Give each:

- Rate
- Type
- Surface
- Amenities
- Rating
- Image or visual fallback

Create realistic availability slots.

---

# 56. Codex Step 5 — Booking Search

Implement:

```text
BookingSearch
```

Fields:

```text
Location
Date
Start time
Duration
Players
```

Responsive:

```text
mobile = stacked
desktop = horizontal grid
```

Changing search fields should update displayed booking context.

---

# 57. Codex Step 6 — Court Grid

Implement:

```text
CourtGrid
CourtCard
```

Court grid:

```text
1 column mobile
2 columns tablet
2–3 columns desktop
```

Court Card must support:

```text
available
selected
booked
maintenance
```

Unavailable cards must not be selectable.

---

# 58. Codex Step 7 — Court Layout Visualization

Implement:

```text
CourtLayoutView
```

Use CSS Grid.

Provide a toggle:

```text
Cards | Court Map
```

Court Map means venue floor layout, not geographical map.

Each court should visually show:

```text
Court number
Availability
Price
```

Selecting the same court from card or layout must update the same booking state.

---

# 59. Codex Step 8 — Time Slots

Implement:

```text
TimeSlotGrid
```

Required states:

```text
Available
Selected
Unavailable
```

Clicking a time updates booking state.

Unavailable times remain visible.

---

# 60. Codex Step 9 — Booking Summary

Implement:

```text
BookingSummary
MobileBookingBar
```

Desktop:

Sticky sidebar.

Mobile:

Sticky lower booking CTA.

Calculate:

```text
court fee = hourlyRate × duration
booking fee = configurable mock value
total = court fee + booking fee
```

Do not duplicate calculation logic in multiple components.

Create:

```text
src/lib/pricing.ts
```

---

# 61. Codex Step 10 — Court Details

Implement:

```text
CourtDetailsDialog
```

Include:

```text
Image
Court name
Type
Surface
Amenities
Capacity
Price
Availability
Book/select button
```

Use an accessible dialog implementation.

If no dialog library is installed, create a simple accessible implementation carefully.

---

# 62. Codex Step 11 — Booking Page

Build:

```text
src/app/book/page.tsx
```

Composition:

```tsx
<PageHeader />

<BookingHero />

<BookingSearch />

<CourtAvailabilitySection>
  <CourtFilter />
  <ViewToggle />
  <CourtGrid or CourtLayoutView />
</CourtAvailabilitySection>

<TimeSlotGrid />

<BookingSummary />
```

Do not put all component logic into `page.tsx`.

---

# 63. Codex Step 12 — Checkout Prototype

Create:

```text
src/app/checkout/page.tsx
```

Include:

```text
Customer details
Players
Optional add-ons
Payment method selection
Price summary
Confirm button
```

Mock payment only.

Clearly label the payment implementation as a UI prototype.

Do not simulate handling raw card information.

---

# 64. Codex Step 13 — Confirmation

Create booking confirmation route.

Example:

```text
/bookings/PKL-260910-1234
```

Display:

```text
Confirmed status
Court
Date
Time
Venue
Price
Booking reference
QR placeholder
```

Provide:

```text
View Booking
Book Another Court
```

---

# 65. Codex Step 14 — My Bookings

Implement:

```text
/bookings
```

Tabs:

```text
Upcoming
Past
Cancelled
```

Use mock data.

Build responsive booking cards.

---

# 66. Codex Step 15 — Admin Skeleton

After customer booking UI is complete, implement:

```text
/admin
```

Add:

```text
Admin sidebar
Metrics
Today's schedule
Recent bookings
Court availability
```

Do not prioritize advanced reports before booking experience is complete.

---

# 67. Codex Step 16 — Loading / Error / Empty States

Required:

```text
Court loading skeleton
Availability loading state
No availability
Booking conflict
Checkout payment failure
No bookings
```

Every major page must have a useful empty/error state.

---

# 68. Codex Step 17 — Accessibility Pass

Verify:

```text
Tab order
Focus states
Input labels
Button labels
Disabled states
Status descriptions
Modal keyboard behavior
Color contrast
```

Use semantic elements.

---

# 69. Codex Step 18 — Responsive Pass

Manually test layouts approximately at:

```text
320px
375px
768px
1024px
1440px
```

Confirm:

- No page-level horizontal scroll
- Booking CTA remains usable
- Court cards do not overflow
- Date inputs fit
- Filters wrap correctly
- Summary remains readable

---

# 70. Codex Step 19 — Polish

Add subtle transitions.

Example:

```text
transition-colors
duration-150
```

Use hover elevation sparingly.

Do not add:

```text
Large glassmorphism
Heavy gradients
Neon effects
Overdone shadows
Constant animations
```

The product should feel polished rather than decorative.

---

# 71. Codex Acceptance Criteria

The implementation is complete when:

## Search

- User can select date.
- User can select time.
- User can select duration.
- User can select venue.

## Courts

- User sees all courts.
- User sees visual status.
- User can select available court.
- User cannot select unavailable court.
- Selected court is visually obvious.

## Court Layout

- User can switch between cards and venue layout.
- Court status remains synchronized.

## Time

- Available slots are selectable.
- Unavailable slots are visible and disabled.

## Pricing

- Price updates based on court and duration.
- Total is visible.

## Responsive

- Works on mobile.
- Works on tablet.
- Works on desktop.

## Accessibility

- Keyboard navigation works.
- Focus states are visible.
- Statuses include text labels.

## Checkout

- Selected booking information reaches checkout.
- Checkout UI displays booking summary.

---

# 72. Suggested Future Backend Contract

Frontend should eventually retrieve availability from:

```http
GET /api/courts/availability
```

Parameters:

```text
locationId
date
startTime
duration
```

Example response:

```json
{
  "date": "2026-09-10",
  "startTime": "18:00",
  "durationMinutes": 120,
  "courts": [
    {
      "id": "court-01",
      "name": "Court One",
      "status": "AVAILABLE",
      "hourlyRate": 650
    }
  ]
}
```

---

# 73. Production Booking Safety

When connected to a real backend, the frontend must never assume that visual availability guarantees the court.

Before creating a booking:

```text
Backend revalidates availability.
```

Recommended:

```text
SELECT COURT
→ REQUEST HOLD
→ BACKEND VALIDATES
→ TEMPORARY HOLD CREATED
→ CHECKOUT
```

If availability changes:

```text
Show booking conflict UI.
Refresh availability.
```

---

# 74. Suggested API Interaction State

Use UI states such as:

```ts
type BookingActionState =
  | "IDLE"
  | "CHECKING_AVAILABILITY"
  | "CREATING_HOLD"
  | "HELD"
  | "CHECKOUT"
  | "CONFIRMED"
  | "ERROR";
```

This provides clearer UI logic than scattered loading booleans.

---

# 75. Design QA Checklist

Before considering a screen complete, confirm:

- [ ] Main action is obvious
- [ ] User can identify available courts quickly
- [ ] Price is visible before checkout
- [ ] Selected court is obvious
- [ ] Unavailable court is clearly disabled
- [ ] Empty state exists
- [ ] Error state exists
- [ ] Loading state exists
- [ ] Mobile layout works
- [ ] Keyboard navigation works
- [ ] Focus states are visible
- [ ] Touch targets are large enough
- [ ] No text relies only on color
- [ ] Spacing is consistent
- [ ] Typography hierarchy is clear
- [ ] No unnecessary modal interrupts booking

---

# 76. Final UI Direction for Codex

The final result should feel like:

```text
Modern sports booking platform
+
Premium facility reservation experience
+
Clean SaaS interaction quality
```

Not:

```text
Generic CRUD system
Generic Bootstrap dashboard
Old-school reservation form
Dense enterprise screen
```

The user should be able to open the booking page and understand within seconds:

```text
Where am I playing?
When am I playing?
Which courts are available?
How much does each court cost?
What am I booking?
How do I continue?
```

---

# 77. Recommended First Implementation Milestone

Codex should complete this milestone first:

```text
/book
```

with:

- Responsive header
- Booking hero
- Booking search
- Court filters
- Court cards
- Court layout view
- Availability statuses
- Time slots
- Court selection
- Dynamic booking summary
- Mobile booking bar
- Mock data
- Loading/empty/error examples

Only after this experience is polished should Codex proceed to:

```text
/checkout
/bookings
/admin
```

---

# 78. Definition of Done

The UI/UX implementation is ready for backend integration when:

1. Court booking can be completed using mock data.
2. Booking state is clearly modeled.
3. All core visual states exist.
4. Layout is responsive.
5. Components are reusable.
6. Pricing logic is centralized.
7. The court layout visualization works.
8. Checkout receives the booking selection.
9. Error/loading/empty states are implemented.
10. Accessibility fundamentals have been verified.
11. Code is TypeScript-safe.
12. No major UI component depends on hard-coded demo behavior.
13. Data can later be replaced with API responses without redesigning the UI architecture.

---

## End of UI/UX Engineering Plan
