# Notification Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Notification Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Notification Service is responsible for sending email notifications based on events published by other microservices. It operates asynchronously by consuming Kafka events.

---

# 2. Responsibilities

- Send booking confirmation emails
- Send booking cancellation emails
- Send payment confirmation emails
- Send event-related notifications
- Maintain notification history

**Out of Scope**

- User Authentication
- Event Management
- Booking Management
- Payment Processing

---

# 3. High-Level Architecture

```text
                  Kafka
                    │
                    ▼
        Notification Service
           │             │
           ▼             ▼
 notification_db     Email Server
```

---

# 4. Security Flow

### Authentication

- Internal service communication.
- No direct client access.

### Authorization

- Not Applicable.

---

# 5. Kafka Event Flow

### Kafka Role

**Consumer**

### Consumed Events

| Event | Topic |
|--------|-------|
| BookingCreated | eventhub.booking.events |
| BookingCancelled | eventhub.booking.events |
| PaymentCompleted | eventhub.payment.events |
| PaymentFailed | eventhub.payment.events |
| EventCreated | eventhub.event.events |

---

# 6. Database Overview

**Database**

`notification_db`

**Primary Tables**

| Table |
|--------|
| notifications |

---

# 7. API Endpoints

No public REST APIs.

Notifications are processed through Kafka event consumers.

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Communication | Kafka |
| Notification Channel | Email |
| Processing | Asynchronous |

---

# 9. Future Enhancements

- SMS Notifications
- Push Notifications
- WhatsApp Notifications
- Retry Mechanism
- Dead Letter Queue (DLQ)

---

# 10. References

- Spring Kafka Documentation
- Spring Mail Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Notification Service Design |