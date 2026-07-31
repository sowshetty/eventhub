# Payment Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Payment Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Payment Service processes payments for event bookings. It manages payment transactions, payment status, and publishes payment events for downstream services.

---

# 2. Responsibilities

- Process payments
- Verify payment status
- Handle payment callbacks
- Maintain payment history
- Publish payment events

**Out of Scope**

- User Authentication
- Booking Management
- Event Management
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
         Payment Service
          │          │
          │          ├──────────────► Kafka
          │          │               PaymentCompleted
          │          │               PaymentFailed
          ▼          │
      payment_db
```

---

# 4. Security Flow

### Authentication

- JWT is validated by the API Gateway.
- Authentication is managed by the Authentication Service.

### Authorization

- USER can view their own payment history.
- ADMIN can access all payment records.

---

# 5. Kafka Event Flow

### Kafka Role

**Producer & Consumer**

### Published Events

| Event | Topic |
|--------|--------|
| PaymentCompleted | payment-events |
| PaymentFailed | payment-events |

### Consumed Events

| Event | Topic |
|--------|--------|
| BookingCreated | booking-events |

---

# 6. Database Overview

**Database**

`payment_db`

**Primary Tables**

| Table |
|--------|
| payments |

---

# 7. API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/v1/payments | Process payment |
| GET | /api/v1/payments/{id} | Get payment details |
| GET | /api/v1/payments | List payments |

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Authentication | JWT |
| Authorization | RBAC |
| Synchronous Communication | REST |
| Asynchronous Communication | Kafka |
| Payment Ownership | Payment Service |

---

# 9. Future Enhancements

- Multiple Payment Gateways
- Refund Processing
- Payment Retry
- Invoice Generation
- Fraud Detection

---

# 10. References

- Spring Boot Documentation
- Spring Data JPA Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Payment Service Design |