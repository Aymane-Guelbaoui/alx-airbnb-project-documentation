# Backend Requirement Specifications – ALX Airbnb Clone Project

This document defines the functional and technical specifications for key backend features of the Airbnb Clone system.

---

## 1. User Authentication

###  Description
Allows users to register, log in, and maintain authenticated sessions securely.

###  API Endpoints

| Method | Endpoint           | Description                |
|--------|--------------------|----------------------------|
| POST   | `/api/register`    | Create a new user account  |
| POST   | `/api/login`       | Authenticate user          |
| GET    | `/api/profile`     | Get current user profile   |

###  Authentication

- Use JWT tokens for session management.
- Use HTTPS to secure all auth-related requests.

###  Input / Output

- **Register Input:** `{ "email": "user@example.com", "password": "secret", "role": "host" }`
- **Login Output:** `{ "token": "jwt_token_here" }`

###  Validation

- Email format check.
- Password min 8 characters, include one uppercase, one number.

---

## 2. Property Management

###  Description
Enables hosts to create, update, view, and delete property listings.

###  API Endpoints

| Method | Endpoint               | Description                 |
|--------|------------------------|-----------------------------|
| POST   | `/api/properties`      | Add new property            |
| GET    | `/api/properties`      | Get all listings (with filters) |
| GET    | `/api/properties/:id`  | Get property details        |
| PUT    | `/api/properties/:id`  | Update property             |
| DELETE | `/api/properties/:id`  | Delete property             |

###  Input / Output

- **Input:** `{ "title": "Modern Loft", "location": "Casablanca", "price": 120, "availability": true }`
- **Output:** Property object with `id`, `created_at`, etc.

###  Validation

- Title required, max 100 chars.
- Price must be a positive number.
- Availability must be a boolean.

###  File Storage

- Use Cloudinary or local file storage for property images.
- Store image URLs in the database.

---

## 3. Booking System

###  Description
Allows guests to book available properties for specified dates.

###  API Endpoints

| Method | Endpoint            | Description                 |
|--------|---------------------|-----------------------------|
| POST   | `/api/bookings`     | Create a booking            |
| GET    | `/api/bookings`     | List user's bookings        |
| DELETE | `/api/bookings/:id` | Cancel a booking            |

###  Input / Output

- **Input:** `{ "property_id": "123", "start_date": "2025-08-01", "end_date": "2025-08-03" }`
- **Output:** Booking confirmation with `booking_id`, status, total cost.

###  Validation

- Start date must be today or later.
- End date must be after start date.
- Check for overlapping bookings before confirming.

###  Payment Integration

- Upon booking, integrate with Stripe or PayPal to charge guest.
- If payment fails, booking is not created.

---

##  Security Requirements

- All API endpoints require JWT-based authentication.
- Use role-based access control: guests, hosts, admins.
- Sanitize inputs to prevent SQL injection / XSS.

---

##  Performance Requirements

- Cache popular search filters using Redis.
- Optimize database indexes for `location`, `price`, `availability`.

---

##  Non-Functional Requirements

- API response time: <500ms on average.
- 99.9% uptime with auto-scaling support.
- Logging with timestamps and error levels.

---
