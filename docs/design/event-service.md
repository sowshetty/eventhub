# Event Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Event Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Event Service manages the complete lifecycle of events, including event creation, updates, publishing, searching, and retrieval. It is the core business service of the EventHub platform.

---

# 2. Responsibilities

- Create events
- Update events
- Delete events
- Publish events
- Search events
- View event details
- Manage event categories

**Out of Scope**

- User Authentication
- Booking Management
- Payment Processing
- Notifications

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
          Event Service
          │          │
          │          ├──────────────► Kafka
          │          │               EventCreated
          │          │               EventUpdated
          │          │               EventDeleted
          ▼          │
          event_db
```

---

# 4. Security Flow

### Authentication

- JWT is validated by the API Gateway.
- Authentication is managed by the Authentication Service.

### Authorization

- ORGANIZER can manage their own events.
- ADMIN can manage all events.
- USER can only view published events.

---

# 5. Event Flow

### Kafka Role

Producer & Consumer

### Published Events

- BookingCreated
- BookingCancelled
- BookingConfirmed

### Consumed Events

- PaymentCompleted
- PaymentFailed

---

# 6. Database Overview

**Database**

`event_db`

**Primary Tables**

| Table |
|--------|
| events |
| categories |

---

# 7. API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/v1/events | Create event |
| GET | /api/v1/events | List events |
| GET | /api/v1/events/{id} | Get event |
| PUT | /api/v1/events/{id} | Update event |
| DELETE | /api/v1/events/{id} | Delete event |

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Authentication | JWT |
| Authorization | RBAC |
| Communication | REST |
| Event Ownership | Event Service |

---

# 9. Future Enhancements

- Event Images
- Event Tags
- Event Approval Workflow
- Event Recommendations
- Elasticsearch Integration

---

# 10. References

- Spring Boot Documentation
- Spring Data JPA Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Event Service Design |