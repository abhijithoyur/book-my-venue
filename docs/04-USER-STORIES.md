# User Stories

## Story Format

```
**Title**: [Feature Name]
**User Type**: [Customer/Owner/Admin]
**Story Points**: [1-13]
**Priority**: [P0/P1/P2]
**Status**: Backlog/Ready/In Progress/Done
**Dependencies**: [Other stories]
**Sprint**: [Sprint number]

**As a** [type of user]
**I want to** [action/feature]
**So that** [benefit]

**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

**Notes**:
- Implementation detail 1
- Implementation detail 2
```

---

## Epic 1: Authentication & User Management

### US-101: User Registration
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 1

**As a** potential user
**I want to** create an account with email and password
**So that** I can book venues and manage bookings

**Acceptance Criteria**:
- [ ] User can sign up with email, password, first name, last name
- [ ] Email validation is enforced
- [ ] Password must meet security requirements (min 8 chars, uppercase, number, special char)
- [ ] Duplicate emails are rejected
- [ ] User receives confirmation email with verification link
- [ ] User type (customer/owner) can be selected during signup
- [ ] User can login immediately after registration

**Tasks**:
- Backend: Create User model and serializer
- Backend: Implement registration endpoint with validation
- Backend: Setup email verification system
- Frontend: Create registration form with validation
- Frontend: Add success/error messaging

---

### US-102: User Login & JWT Token Management
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 1

**As a** registered user
**I want to** login with email/password and receive JWT tokens
**So that** I can authenticate API requests

**Acceptance Criteria**:
- [ ] User can login with email and password
- [ ] Successful login returns access_token (15 min expiry) and refresh_token (7 days)
- [ ] Tokens are stored securely in localStorage
- [ ] Failed login shows appropriate error message
- [ ] User can refresh their token before expiry
- [ ] Expired token returns 401 Unauthorized
- [ ] Token includes user info (id, email, user_type)

**Tasks**:
- Backend: Implement JWT authentication with djangorestframework-simplejwt
- Backend: Create login endpoint
- Backend: Create token refresh endpoint
- Frontend: Implement login form
- Frontend: Setup token storage and automatic token refresh

---

### US-103: User Profile Management
**Status**: Ready
**Story Points**: 2
**Priority**: P1
**Sprint**: Sprint 1

**As a** logged-in user
**I want to** view and edit my profile information
**So that** I can keep my details up to date

**Acceptance Criteria**:
- [ ] User can view their current profile
- [ ] User can edit: first name, last name, phone number, bio
- [ ] User can upload profile picture
- [ ] Changes are saved and reflected immediately
- [ ] User cannot change email or user_type
- [ ] Profile picture is validated (format, size)

**Tasks**:
- Backend: Create profile retrieval and update endpoints
- Backend: Implement file upload for profile picture
- Frontend: Create profile view/edit page
- Frontend: Add image cropping tool

---

### US-104: Logout & Session Management
**Status**: Ready
**Story Points**: 1
**Priority**: P1
**Sprint**: Sprint 1

**As a** logged-in user
**I want to** logout and have my session cleared
**So that** my account is secure on shared devices

**Acceptance Criteria**:
- [ ] User can logout from any page
- [ ] Tokens are cleared from localStorage
- [ ] User is redirected to home page
- [ ] Expired sessions automatically logout user
- [ ] User can logout on all devices (optional for MVP)

**Tasks**:
- Backend: Create logout endpoint (token blacklist)
- Frontend: Implement logout button
- Frontend: Clear tokens and redirect to home

---

## Epic 2: Venue Management

### US-201: Venue Owner Registration & Setup
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 1

**As a** venue owner
**I want to** register as a venue owner and set up my profile
**So that** I can list my venues

**Acceptance Criteria**:
- [ ] Owner can select "venue_owner" during registration
- [ ] Owner receives owner-specific onboarding
- [ ] Owner can upload business documents (optional for MVP)
- [ ] Owner profile shows "pending verification" status
- [ ] Owner can view verification timeline

**Tasks**:
- Backend: Add venue_owner user type
- Backend: Create owner verification workflow
- Frontend: Create owner signup flow
- Frontend: Show verification status

---

### US-202: Create & List Venues
**Status**: Ready
**Story Points**: 5
**Priority**: P0
**Sprint**: Sprint 2

**As a** venue owner
**I want to** create a new venue listing with details and images
**So that** customers can discover my venue

**Acceptance Criteria**:
- [ ] Owner can enter venue details: name, description, address, capacity, price
- [ ] Owner can upload multiple images (primary + gallery)
- [ ] Owner can add amenities from predefined list (AC, WiFi, Parking, etc.)
- [ ] Owner can assign category (Banquet Hall, Conference Room, etc.)
- [ ] Venue creation is saved as PENDING verification
- [ ] Owner receives confirmation and can track verification status
- [ ] Venue appears in search only AFTER admin approval

**Tasks**:
- Backend: Create Venue model and serializer
- Backend: Create venue creation endpoint with image upload
- Backend: Add amenity and category management
- Frontend: Create multi-step venue form
- Frontend: Implement image upload with preview
- Frontend: Show amenity selector

---

### US-203: Search & Filter Venues
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 2

**As a** customer
**I want to** search venues by location, capacity, and price
**So that** I can find suitable venues easily

**Acceptance Criteria**:
- [ ] Search results show venues by city
- [ ] Filters available: capacity range, price range, amenities, rating
- [ ] Search results show: venue image, name, price, capacity, rating
- [ ] Results are paginated (20 per page)
- [ ] Results sorted by rating, price, or recently added
- [ ] Search is fast (< 500ms)

**Tasks**:
- Backend: Create venue list endpoint with filtering
- Backend: Add search indexing
- Frontend: Create search page with filters
- Frontend: Display venue cards in grid
- Frontend: Implement pagination

---

### US-204: View Venue Details
**Status**: Ready
**Story Points**: 2
**Priority**: P0
**Sprint**: Sprint 2

**As a** customer
**I want to** view detailed information about a venue
**So that** I can decide if it matches my needs

**Acceptance Criteria**:
- [ ] Venue details include: images, description, amenities, capacity, price, reviews
- [ ] Customer can see venue owner contact info
- [ ] Customer can view availability calendar
- [ ] Customer can see venue location on map (optional for MVP)
- [ ] Customer can see reviews and ratings
- [ ] Customer can go directly to booking from this page

**Tasks**:
- Backend: Create venue detail endpoint
- Backend: Include related data (amenities, reviews, availability)
- Frontend: Create venue detail page with image gallery
- Frontend: Display amenities in a readable format
- Frontend: Show availability calendar

---

### US-205: Edit & Delete Venues
**Status**: Ready
**Story Points**: 2
**Priority**: P1
**Sprint**: Sprint 2

**As a** venue owner
**I want to** edit my venue details and images
**So that** I can keep information current

**Acceptance Criteria**:
- [ ] Owner can edit any venue field except category
- [ ] Owner can add/remove images
- [ ] Owner can update amenities
- [ ] Changes are saved immediately
- [ ] Owner can delete venue (soft delete, shows warning)
- [ ] Only owner can edit their own venues

**Tasks**:
- Backend: Create venue update endpoint
- Backend: Implement permission checks
- Frontend: Create venue edit form (prepopulated)
- Frontend: Show confirmation before delete

---

### US-206: Venue Reviews & Ratings
**Status**: Backlog
**Story Points**: 3
**Priority**: P2
**Sprint**: Sprint 3

**As a** customer
**I want to** leave a review and rating for a venue after booking
**So that** other customers can benefit from my experience

**Acceptance Criteria**:
- [ ] Customer can only review after booking is COMPLETED
- [ ] Review includes: rating (1-5 stars), title, content
- [ ] Reviews are visible on venue detail page
- [ ] Venue average rating updates automatically
- [ ] Admin can moderate/delete reviews
- [ ] Reviews show customer name and booking date

**Tasks**:
- Backend: Create Review model
- Backend: Create review endpoint
- Backend: Update venue rating calculation
- Frontend: Create review form
- Frontend: Display reviews on venue page

---

## Epic 3: Booking Management

### US-301: Submit Booking Request
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 2

**As a** customer
**I want to** submit a booking request for a venue
**So that** the venue owner can review and approve/reject

**Acceptance Criteria**:
- [ ] Customer can select date, number of guests, and notes
- [ ] System validates: date is available, guests <= capacity
- [ ] Booking is created with PENDING status
- [ ] Total price is calculated (price_per_day × capacity capacity)
- [ ] Confirmation message shows booking details
- [ ] Customer can see booking in their dashboard

**Tasks**:
- Backend: Create booking creation endpoint
- Backend: Validate availability before creating booking
- Backend: Calculate total price
- Frontend: Create booking form
- Frontend: Show booking confirmation
- Frontend: Add to customer dashboard

---

### US-302: View Booking History
**Status**: Ready
**Story Points**: 2
**Priority**: P1
**Sprint**: Sprint 2

**As a** customer
**I want to** view all my past and current bookings
**So that** I can track my reservations

**Acceptance Criteria**:
- [ ] Customer can see all bookings (past and future)
- [ ] Bookings show: venue name, date, status, total price
- [ ] Bookings are sorted by date (newest first)
- [ ] Filter by status: PENDING, APPROVED, REJECTED, COMPLETED
- [ ] Pagination (20 per page)
- [ ] Can click on booking to see full details

**Tasks**:
- Backend: Create booking list endpoint with filters
- Frontend: Create bookings page
- Frontend: Show booking cards with status badges
- Frontend: Implement filtering and pagination

---

### US-303: Approve/Reject Bookings (Venue Owner)
**Status**: Ready
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 2

**As a** venue owner
**I want to** review pending bookings and approve or reject them
**So that** I can manage my venue calendar

**Acceptance Criteria**:
- [ ] Owner sees PENDING bookings in owner dashboard
- [ ] Owner can view booking details: customer info, date, guests
- [ ] Owner can APPROVE booking with optional notes
- [ ] Owner can REJECT booking with rejection reason
- [ ] Customer is notified of approval/rejection
- [ ] Approved booking blocks that date on availability
- [ ] Only venue owner can approve/reject their bookings

**Tasks**:
- Backend: Create approve/reject endpoints
- Backend: Update availability when booking approved
- Backend: Send notifications to customer
- Frontend: Create owner dashboard with pending bookings
- Frontend: Add approve/reject buttons and modals

---

### US-304: Cancel Booking
**Status**: Ready
**Story Points**: 2
**Priority**: P1
**Sprint**: Sprint 3

**As a** customer
**I want to** cancel my booking if my plans change
**So that** I don't have to honor the reservation

**Acceptance Criteria**:
- [ ] Customer can cancel PENDING or APPROVED bookings
- [ ] Cancellation requires reason
- [ ] Owner is notified of cancellation
- [ ] Availability is released if booking was APPROVED
- [ ] Cannot cancel within X days of booking date (configurable)
- [ ] Cancelled bookings show in history

**Tasks**:
- Backend: Create cancel endpoint
- Backend: Release availability
- Backend: Send notification to owner
- Frontend: Add cancel button with modal
- Frontend: Show cancellation history

---

### US-305: Booking Status Tracking
**Status**: Ready
**Story Points**: 2
**Priority**: P1
**Sprint**: Sprint 2

**As a** customer
**I want to** track the status of my booking in real-time
**So that** I know if my booking is confirmed

**Acceptance Criteria**:
- [ ] Booking shows clear status: PENDING, APPROVED, REJECTED, CANCELLED, COMPLETED
- [ ] Status badge shows appropriate color (yellow=pending, green=approved, red=rejected)
- [ ] Customer can see when status changed and by whom
- [ ] History of all status changes is visible
- [ ] Customer can contact owner if needed

**Tasks**:
- Backend: Create booking history tracking
- Frontend: Display status timeline
- Frontend: Show booking history with timestamps

---

## Epic 4: Availability Management

### US-401: Create Venue Availability Slots
**Status**: Ready
**Story Points**: 2
**Priority**: P0
**Sprint**: Sprint 2

**As a** venue owner
**I want to** mark dates when my venue is available for booking
**So that** customers can only book available dates

**Acceptance Criteria**:
- [ ] Owner can bulk create availability for date range
- [ ] Each date is treated as full-day slot
- [ ] Owner can set availability for months in advance
- [ ] Availability is created with status = "available"
- [ ] Owner can delete future availability if needed

**Tasks**:
- Backend: Create Availability model
- Backend: Create bulk availability creation endpoint
- Frontend: Create availability calendar editor
- Frontend: Allow date range selection

---

### US-402: Block Dates (Maintenance/Special Events)
**Status**: Ready
**Story Points**: 1
**Priority**: P1
**Sprint**: Sprint 2

**As a** venue owner
**I want to** block specific dates when venue is unavailable
**So that** customers cannot book during maintenance or special events

**Acceptance Criteria**:
- [ ] Owner can block date ranges
- [ ] Blocked dates show reason (maintenance, special event, etc.)
- [ ] Blocked dates are removed from availability
- [ ] Blocked dates override previously available dates
- [ ] Owner can view all blocked dates

**Tasks**:
- Backend: Create BlockedDates model
- Backend: Create block dates endpoint
- Frontend: Add block dates form to calendar

---

### US-403: Check Availability
**Status**: Ready
**Story Points**: 1
**Priority**: P0
**Sprint**: Sprint 2

**As a** customer
**I want to** see which dates are available for a venue
**So that** I can choose the best date for my event

**Acceptance Criteria**:
- [ ] Availability calendar shows available/booked/blocked dates
- [ ] Visual indication: green (available), red (booked), gray (blocked)
- [ ] Customer can hover to see price and details
- [ ] Calendar shows next 3 months by default
- [ ] Can navigate to future months

**Tasks**:
- Backend: Create availability check endpoint
- Frontend: Implement interactive calendar
- Frontend: Show date status with colors

---

## Epic 5: Admin Dashboard

### US-501: User Management (Admin)
**Status**: Backlog
**Story Points**: 3
**Priority**: P1
**Sprint**: Sprint 4

**As an** admin
**I want to** manage users, view their activity, and handle issues
**So that** I can maintain platform integrity

**Acceptance Criteria**:
- [ ] Admin can view all users with filters (user_type, status)
- [ ] Admin can deactivate/reactivate users
- [ ] Admin can view user activity and booking history
- [ ] Admin can send messages to users
- [ ] Admin can reset user passwords (with email confirmation)
- [ ] Changes are logged in audit trail

**Tasks**:
- Backend: Create admin user endpoints with filtering
- Backend: Implement user deactivation/reactivation
- Backend: Create audit logging
- Frontend: Create admin user management page
- Frontend: Show user details and activity

---

### US-502: Venue Verification & Moderation
**Status**: Backlog
**Story Points**: 3
**Priority**: P0
**Sprint**: Sprint 3

**As an** admin
**I want to** review and approve/reject new venue listings
**So that** only legitimate venues are on the platform

**Acceptance Criteria**:
- [ ] Admin sees list of pending venues
- [ ] Admin can view full venue details, images, owner info
- [ ] Admin can APPROVE venue (becomes visible in search)
- [ ] Admin can REJECT venue with reason
- [ ] Admin can request additional info from owner
- [ ] Owner is notified of decision
- [ ] Admin can flag venues for compliance issues

**Tasks**:
- Backend: Create venue verification endpoints
- Backend: Send notification to owner
- Frontend: Create venue moderation dashboard
- Frontend: Show approve/reject buttons and forms

---

### US-503: Booking Dispute Resolution
**Status**: Backlog
**Story Points**: 3
**Priority**: P2
**Sprint**: Sprint 4

**As an** admin
**I want to** handle disputes between customers and venue owners
**So that** platform trust is maintained

**Acceptance Criteria**:
- [ ] Admin can view disputed bookings
- [ ] Admin can view communication history
- [ ] Admin can make decisions: refund, cancel, force approve
- [ ] Decisions are documented in audit trail
- [ ] Both parties are notified of decision

**Tasks**:
- Backend: Create dispute endpoints
- Backend: Implement decision logging
- Frontend: Create dispute management dashboard

---

### US-504: System Monitoring & Reports
**Status**: Backlog
**Story Points**: 2
**Priority**: P2
**Sprint**: Sprint 4

**As an** admin
**I want to** monitor platform metrics and generate reports
**So that** I can track growth and identify issues

**Acceptance Criteria**:
- [ ] Dashboard shows: total users, venues, bookings, revenue
- [ ] Charts showing growth trends (weekly/monthly)
- [ ] Filters by date range, venue, category
- [ ] Export reports to CSV
- [ ] System health monitoring (API response time, error rates)

**Tasks**:
- Backend: Create analytics endpoints
- Backend: Implement metrics collection
- Frontend: Create analytics dashboard
- Frontend: Add charting library (Chart.js)

---

## Sprint Summary

| Sprint | Focus | Stories | Points |
|--------|-------|---------|--------|
| Sprint 1 | Auth & Setup | US-101, US-102, US-103, US-104, US-201 | 12 |
| Sprint 2 | Core Booking | US-202, US-203, US-204, US-205, US-301, US-302, US-303, US-401, US-402, US-403 | 23 |
| Sprint 3 | Refinement | US-206, US-304, US-502 | 8 |
| Sprint 4 | Admin & Polish | US-501, US-503, US-504 | 8 |

---

## Backlog

- Payment Integration (Phase 2)
- Real-time Notifications (Phase 2)
- Advanced Analytics (Phase 2)
- Multi-language Support (Future)
- Mobile App (Future)
