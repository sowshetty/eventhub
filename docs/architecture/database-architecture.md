# Database Architecture

---

## 1. Purpose

This document defines the database architecture of the EventHub platform. It describes the data persistence strategy, database ownership model, storage technologies, data consistency mechanisms, security considerations, and operational guidelines for managing application data.

The objective of this architecture is to provide a scalable, reliable, and maintainable data layer that supports the business requirements of the EventHub platform while adhering to microservices best practices.

---

## 2. Scope

This document applies to all persistence technologies used within the EventHub platform.

The architecture covers:

- Relational database design
- Document database design
- Database ownership
- Polyglot persistence
- Caching strategy
- Search indexing
- Data consistency
- Database security
- Backup and recovery

Data models for individual services are documented separately within their respective service documentation.

---

## 3. Database Architecture Overview

EventHub adopts a polyglot persistence architecture where multiple storage technologies are used based on the functional and non-functional requirements of each service.

```
                    EventHub Platform

                            │

     ┌──────────────────────┼──────────────────────┐

     ▼                      ▼                      ▼

 PostgreSQL             MongoDB                Redis

 Transactional        Document Storage         Cache

     │                      │

     └──────────────┬───────┘

                    ▼

             Elasticsearch

             Search & Analytics

                    │

                    ▼

              Apache Kafka

             Event Streaming
```

Each microservice owns its data and interacts with other services through APIs or asynchronous events rather than direct database access.

---

## 4. Polyglot Persistence Strategy

EventHub uses multiple persistence technologies to leverage the strengths of each database.

| Technology | Purpose |
|------------|---------|
| PostgreSQL | Transactional data and relational entities |
| MongoDB | Flexible document-oriented storage |
| Redis | Distributed caching |
| Elasticsearch | Full-text search |
| Apache Kafka | Event streaming and asynchronous communication |

Each technology addresses a specific architectural requirement rather than attempting to solve all problems with a single database.

---

## 5. Database Ownership

Every microservice owns and manages its own data.

Direct database access between services is prohibited.

| Microservice | Primary Data Store |
|--------------|--------------------|
| Auth Service | PostgreSQL |
| User Service | PostgreSQL |
| Event Service | PostgreSQL + MongoDB |
| Booking Service | PostgreSQL |
| Payment Service | PostgreSQL |
| Notification Service | MongoDB |
| Search Service | Elasticsearch |
| Analytics Service | PostgreSQL |

Inter-service communication occurs through REST APIs or Apache Kafka events.

---

## 6. PostgreSQL Architecture

PostgreSQL serves as the primary relational database for transactional workloads.

Typical data stored includes:

- Users
- Roles
- Events
- Bookings
- Payments
- Ticket Categories
- Venues

All relational entities follow a standardized schema design.

Common audit columns include:

- id (UUID)
- created_at
- created_by
- updated_at
- updated_by
- version
- status

Database schema changes are managed using Flyway migrations.

---

## 7. MongoDB Architecture

MongoDB stores flexible, document-oriented data where schema evolution is expected.

Typical document collections include:

- Event Details
- Event Metadata
- FAQs
- Speaker Information
- Gallery Metadata
- Notification Templates

MongoDB collections are independently versioned and indexed according to application requirements.

---

## 8. Redis Strategy

Redis provides high-performance distributed caching.

Typical cache usage includes:

- Frequently accessed reference data
- User session metadata (if required)
- Rate limiting support
- API response caching
- Temporary application data

Cache entries should remain disposable and rebuildable from the primary data sources.

---

## 9. Elasticsearch Strategy

Elasticsearch provides search and analytical capabilities.

Indexed content includes:

- Event titles
- Event descriptions
- Categories
- Locations
- Organizer names
- Tags

Search indexes are populated asynchronously through Apache Kafka events.

---

## 10. Data Consistency

Each microservice maintains transactional consistency within its own database.

Distributed transactions across multiple services are avoided.

Cross-service consistency is achieved through:

- Event-driven communication
- Eventual consistency
- Idempotent event processing
- Retry mechanisms

This approach reduces coupling and improves scalability.

---

## 11. Database Security

Database security measures include:

- Role-based database access
- Encrypted communication
- Secure credential management
- Least privilege principle
- Secrets stored outside source code
- Database auditing
- Regular credential rotation

Production credentials are managed through Kubernetes Secrets and may later integrate with AWS Secrets Manager.

---

## 12. Backup and Recovery

Backup strategies include:

- Scheduled PostgreSQL backups
- MongoDB backup snapshots
- Elasticsearch snapshot repositories
- Backup verification
- Disaster recovery procedures

Recovery objectives and retention policies are defined as part of the operational runbooks.

---

## 13. Architecture Decisions

| Decision | Rationale |
|----------|-----------|
| PostgreSQL for transactional data | Provides ACID compliance and strong consistency |
| MongoDB for document storage | Supports flexible and evolving schemas |
| Database per service | Enables loose coupling and independent deployment |
| UUID primary keys | Supports distributed microservice architecture |
| Flyway for schema migrations | Enables version-controlled database evolution |
| Redis for caching | Improves application performance and reduces database load |
| Elasticsearch for search | Provides efficient full-text search capabilities |
| Kafka for data synchronization | Enables asynchronous communication and eventual consistency |

---

## 14. References

### Internal Documents

- [System Overview](system-overview.md)
- [Technology Stack](technology-stack.md)
- [Deployment Architecture](deployment-architecture.md)
- [Security Architecture](security-architecture.md)
- [API Design Guidelines](api-design-guidelines.md)

---

### External References

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [MongoDB Documentation](https://www.mongodb.com/docs/)
- [Elasticsearch Documentation](https://www.elastic.co/guide/)
- [Redis Documentation](https://redis.io/docs/)
- [Flyway Documentation](https://documentation.red-gate.com/fd)

---

## Version History

| Version | Date | Author | Changes |
|----------|------------|----------------|-----------------------------|
| 1.0 | 23-Jul-2026 | Sowmyaa Shetty | Initial version |