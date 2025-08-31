# Use Case Diagram — Backend Features

> Export your diagram as **use-case.png** and store it in this folder.

## Actors
- **Guest**: browses, books, pays, reviews.
- **Host**: manages properties, views/accepts bookings, responds to reviews.
- **Admin**: moderates users/listings, audits payments/logs.
- **Payment Gateway** (external system)
- **Email Service** (external system)

## Use Cases (by Actor)
### Guest
- Register / Login / Logout
- View & Update Profile
- Search & Filter Properties
- View Property Details
- Create Booking
- Pay for Booking
- Cancel Booking (policy permitting)
- Write Review (post-stay)
- Send Message to Host (optional)

### Host
- Login
- Create/Update/Delete Property
- View Bookings for My Properties
- Accept/Decline/Cancel Bookings (if policy allows)
- Respond to Reviews (optional)
- Message Guests (optional)

### Admin
- Login
- View/Suspend Users or Properties
- View Bookings/Payments
- Issue Refund (simulated)
- View Audit Logs

### Includes / Extends (optional)
- **Pay for Booking** ⟶ *includes* **Create Payment Intent**
- **Create Booking** ⟶ *includes* **Check Availability**, **Calculate Total**


