# User Stories — Airbnb Clone Backend

## Authentication & Profile
1. As a **guest**, I want to **create an account** so that I can **book properties**.
2. As a **user**, I want to **log in securely** so that I can **access my dashboard**.
3. As a **user**, I want to **update my profile** so that my **contact information** is current.

## Properties
4. As a **host**, I want to **create a property listing** so that I can **receive bookings**.
5. As a **host**, I want to **edit or remove my listing** so I can **keep information accurate**.
6. As a **guest**, I want to **search and filter properties** so I can **find a stay that fits my needs**.

## Bookings & Payments
7. As a **guest**, I want to **book available dates** so I can **reserve a property**.
8. As a **guest**, I want to **pay securely** so that my **booking is confirmed**.
9. As a **host**, I want to **view bookings for my properties** so I can **prepare for arrivals**.
10. As a **guest**, I want to **cancel a booking (within policy)** so I can **change my plans**.

## Reviews & Messaging
11. As a **guest**, I want to **leave a review** after my stay so I can **share feedback**.
12. As a **host**, I want to **respond to reviews** so I can **address guest comments**.
13. As a **guest/host**, I want to **exchange messages** so that **logistics are clear**. *(optional)*

## Admin
14. As an **admin**, I want to **monitor users/listings/bookings** so I can **keep the platform safe**.
15. As an **admin**, I want to **suspend abusive users or listings** so I can **enforce policy**.

---

## Sample Acceptance Criteria (Gherkin)
**Create Booking**
- Given an authenticated guest  
- And a property with available dates  
- When the guest posts valid `start_date` and `end_date`  
- Then the system **creates a booking** with status `pending` and **calculates total price**  
- And returns **201 Created** with the booking payload.

**Pay for Booking**
- Given a `pending` booking  
- When the guest submits valid payment details  
- Then the system **creates a payment**, **marks booking confirmed**, and sends a **confirmation email**.
