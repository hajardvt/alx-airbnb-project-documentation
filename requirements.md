# Backend Requirement Specifications

This document details the **functional** and **technical** specs for three key features:
1) User Authentication
2) Property Management
3) Booking System

---

## 1) User Authentication

### Functional
- Register with email + password + role (guest/host).
- Login to obtain JWT access/refresh tokens.
- Refresh token to renew session.
- Logout (revoke refresh).
- View/Update profile (name, phone, avatar).

### API (REST, JSON)
- `POST /api/v1/auth/register`
  - In: `{ email, password, role }`
  - Out: `201 Created` → `{ user: {...}, tokens: { access, refresh } }`
  - Errors: `400` validation, `409` email exists
- `POST /api/v1/auth/login`
  - In: `{ email, password }`
  - Out: `200` → `{ user, tokens }`
  - Errors: `401` invalid credentials
- `POST /api/v1/auth/refresh`
  - In: `{ refresh }`
  - Out: `200` → `{ access }`
  - Errors: `401` invalid/expired
- `GET /api/v1/users/me` (auth)
  - Out: `200` → `{ user }`
- `PATCH /api/v1/users/me` (auth, multipart optional for avatar)
  - In: `{ first_name?, last_name?, phone? } | form-data`
  - Out: `200` → `{ user }`

### Validation
- Email format; password length ≥ 8; role ∈ {guest, host}.
- Unique email.

### Security
- Hash passwords (bcrypt/argon2).
- JWT with short-lived access, long-lived refresh.
- Rate limit login/register.
- CORS configured.

### Performance
- Index on `users.email`.
- Avoid N+1 on profile lookups.

---

## 2) Property Management

### Functional
- Hosts: create/update/delete/list own properties.
- Guests: list/search/filter properties; view details.
- Images: upload 1..n images (scenario-based: local FS or cloud).

### API
- `POST /api/v1/properties` (auth: host)
  - In: `{ title, description, location, price_per_night, amenities[], images? }`
  - Out: `201` → `{ property }`
- `GET /api/v1/properties`
  - Query: `q, location, min_price, max_price, guests, amenities[], sort, page, page_size`
  - Out: `200` → `{ items: [...], page, total }`
- `GET /api/v1/properties/{id}` → `{ property, reviews?, host? }`
- `PATCH /api/v1/properties/{id}` (auth: host owner) → `{ property }`
- `DELETE /api/v1/properties/{id}` (auth: host owner) → `204`

### Validation
- Required: title, location, price_per_night ≥ 0.
- Ownership checks for updates/deletes.

### Performance
- Indexes: `location`, `price_per_night`, FKs.
- Pagination mandatory.

---

## 3) Booking System

### Functional
- Create booking for available date range; prevent overlaps.
- Status lifecycle: `pending` → `confirmed` → `completed` / `canceled`.
- Guest: view/cancel own bookings per policy.
- Host: view bookings for owned properties.
- Payment integration (mock/test) to confirm bookings.

### API
- `POST /api/v1/bookings` (auth: guest)
  - In: `{ property_id, start_date, end_date }`
  - Flow: validate dates → check availability → compute total → create booking `pending`
  - Out: `201` → `{ booking }`
- `POST /api/v1/bookings/{id}/pay` (auth: booking owner)
  - In: `{ payment_method, card_token? }`
  - Out: `200` → `{ booking: { status: "confirmed" }, payment }`
- `GET /api/v1/bookings/mine` (auth) → list guest’s bookings
- `GET /api/v1/host/bookings` (auth: host) → bookings for my properties
- `PATCH /api/v1/bookings/{id}/cancel` (auth: owner/host/admin) → `{ booking }`

### Validation
- `start_date <= end_date`; min stay (optional).
- No overlap with existing confirmed bookings for the property.

### Security & Consistency
- Idempotency key on payment.
- Transactional updates: payment success → booking `confirmed`.

### Performance
- Indexes: `(property_id, start_date, end_date)`, `(user_id)`.

---

## Common Error Model
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "min_price must be <= max_price",
    "fields": { "min_price": "must be <= max_price" }
  }
}
