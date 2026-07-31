# Booking Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Booking Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Booking Service manages event ticket bookings. It handles booking creation, cancellation, booking status, and communicates with the Payment and Notification services.

---

# 2. Responsibilities

- Create bookings
- View bookings
- Cancel bookings
- Manage booking status
- Reserve event seats
- Coordinate with Payment Service

**Out of Scope**

- User Authentication
- Event Management
- Payment Processing
- Notification Delivery

---

# 3. High-Level Architecture

```text
             Client
                │
                ▼
          API Gateway
                │
       JWT Validation
                │
                ▼
         Booking Service
                │
                ▼
           booking_db
```

---

# 4. Security Flow

### Authentication

- JWT is validated by the API Gateway.
- Authentication is handled by the Authentication Service.

### Authorization

- USER can manage their own bookings.
- ADMIN can access all bookings.

---

# 5. Database Overview

**Database**

`booking_db`

**Primary Tables**

| Table |
|--------|
| bookings |

---

# 6. API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/v1/bookings | Create booking |
| GET | /api/v1/bookings | List bookings |
| GET | /api/v1/bookings/{id} | Get booking |
| PUT | /api/v1/bookings/{id}/cancel | Cancel booking |

---

# 7. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Authentication | JWT |
| Authorization | RBAC |
| Communication | REST + Kafka |
| Booking Ownership | Booking Service |

---

# 8. Future Enhancements

- Seat Selection
- Booking History
- Booking QR Code
- Booking Expiration
- Waitlist Management

---

# 9. References

- Spring Boot Documentation
- Spring Data JPA Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Booking Service Design |