# Analytics Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Analytics Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Analytics Service collects and processes business events to generate insights, reports, and dashboards. It consumes Kafka events without impacting business services.

---

# 2. Responsibilities

- Collect business events
- Generate reports
- Produce business metrics
- Generate dashboards
- Track platform statistics

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
          Analytics Service
                    │
                    ▼
             analytics_db
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
| EventCreated | eventhub.event.events |
| EventUpdated | eventhub.event.events |
| EventDeleted | eventhub.event.events |
| BookingCreated | eventhub.booking.events |
| BookingCancelled | eventhub.booking.events |
| PaymentCompleted | eventhub.payment.events |
| PaymentFailed | eventhub.payment.events |

---

# 6. Database Overview

**Database**

`analytics_db`

**Primary Tables**

| Table |
|--------|
| analytics_records |

---

# 7. API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /api/v1/analytics/dashboard | Dashboard summary |
| GET | /api/v1/analytics/reports | Reports |
| GET | /api/v1/analytics/statistics | Platform statistics |

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Communication | Kafka |
| Processing | Asynchronous |
| Reporting | REST APIs |

---

# 9. Future Enhancements

- Elasticsearch
- Kibana Dashboards
- Real-time Analytics
- Predictive Analytics

---

# 10. References

- Spring Kafka Documentation
- Spring Boot Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Analytics Service Design |