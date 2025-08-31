# Airbnb Clone — Backend Features & Functionalities

> This document enumerates the backend features to be shown in **features-and-functionalities.png** (exported from draw.io and stored in this folder).

## 1) User Management & Auth
- **Register (guest/host/admin via seeding)**: email, password, role, profile fields.
- **Login / Refresh / Logout**: JWT-based sessions, refresh tokens.
- **Profile**: view/update profile, avatar upload.
- **RBAC**: guest vs host vs admin permissions.
- **Security**: password hashing, rate limiting, IP throttling, email verification (optional).

## 2) Property Listings
- **CRUD for Hosts**: create/update/delete/list property.
- **Media**: image upload (local or cloud; e.g., S3/Cloudinary or local for this project).
- **Availability**: store nightly price, min/max stay, blackout dates (optional v1).
- **Searchable attributes**: title, description, location, price per night, amenities.

## 3) Search & Filters
- **Keyword search**: location, title/description.
- **Filters**: price range, guests, amenities, rating.
- **Sort & Pagination**: price asc/desc, rating, newest.

## 4) Booking Management
- **Create Booking**: validate date range, prevent overlaps, compute total.
- **Booking Status**: pending → confirmed → completed; cancellation flows.
- **View/Manage Bookings**: by guest (my bookings) and by host (bookings for my properties).
- **Calendar endpoint**: (optional) host availability snapshot.

## 5) Payments
- **Gateway Integration**: mock Stripe/PayPal (test mode) or simulation service.
- **Capture/Refund**: charge guest, payout host (simulated).
- **Receipts & Idempotency**: store payment intent IDs, prevent double charge.

## 6) Reviews & Ratings
- **Create Review**: guest after completed stay; 1–5 rating, comment.
- **Uniqueness rule**: (optional) one review per booking.
- **Host Replies**: (optional) reply to reviews.

## 7) Messaging (optional v1 → v2)
- **Guest ↔ Host**: send/receive messages tied to a property/booking context.
- **Basic moderation**: size limits, simple filtering.

## 8) Notifications
- **Email**: booking confirmation/cancellation, payment updates.
- **In-app**: (optional) unread counts for messages, booking events.

## 9) Admin
- **Dashboards**: users, listings, bookings, payments.
- **Controls**: suspend user/property, issue refunds (simulated), view logs.

## 10) Technical & Non-Functional
- **API**: REST (JSON), proper status codes; GraphQL optional.
- **DB**: MySQL/PostgreSQL; indices on FKs + frequently used filters.
- **Security**: HTTPS, JWT, CORS, input validation, OWASP basics.
- **Performance**: pagination, caching (optional), N+1 query avoidance.
- **Observability**: error handling, structured logs, request IDs.
- **Testing**: unit + integration (auth, booking rules, payments).


