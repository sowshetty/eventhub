# Database Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Database Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

EventHub follows the **Database per Service** pattern, where each microservice owns its database. This ensures loose coupling, independent deployment, and better scalability.

---

# 2. Database Strategy

- PostgreSQL for all services
- Database per Service
- UUID as Primary Key
- Flyway for database migrations
- No shared database between services

---

# 3. Naming Conventions

| Item | Convention |
|------|------------|
| Tables | snake_case |
| Columns | snake_case |
| Primary Key | id |
| Foreign Key | `<entity>_id` |
| Timestamp | created_at, updated_at |

---

# 4. Common Audit Columns

| Column | Type |
|---------|------|
| id | UUID |
| created_at | TIMESTAMP |
| updated_at | TIMESTAMP |
| created_by | UUID |
| updated_by | UUID |

---

# 5. Service Databases

| Service | Database |
|----------|----------|
| Authentication Service | auth_db |
| User Service | user_db |
| Event Service | event_db |
| Booking Service | booking_db |
| Payment Service | payment_db |
| Notification Service | notification_db |
| Analytics Service | analytics_db |

---

# 6. Entity Ownership

| Service | Entities |
|----------|----------|
| Authentication | users, roles, refresh_tokens |
| User | user_profiles |
| Event | events, categories |
| Booking | bookings |
| Payment | payments |
| Notification | notifications |
| Analytics | analytics_records |

---

# 7. Design Principles

- Each service owns its database.
- No cross-database joins.
- Services communicate through REST APIs or Kafka events.
- Foreign keys are used only within the same service database.
- Business data is never accessed directly from another service.

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Architecture | Database per Service |
| Primary Key | UUID |
| Migration Tool | Flyway |
| Communication | REST + Kafka |
| Cross-Service Access | APIs / Events Only |

---

# 9. Future Enhancements

- Read Replicas
- Database Partitioning
- Redis Caching
- Multi-Region Replication
- Database Encryption at Rest

---

# 10. References

- PostgreSQL Documentation
- Flyway Documentation
- Microservices.io – Database per Service Pattern

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 30-Jul-2026 | Initial Database Design |