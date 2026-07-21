# Infrastructure Services

## API Gateway

### Purpose

The API Gateway is the single entry point for all client requests. It routes requests to the appropriate backend services and handles cross-cutting concerns such as authentication, authorization, and request routing.

---

### Responsibilities

- Receive all client requests
- Route requests to appropriate microservices
- Validate JWT tokens
- Enforce security policies
- Apply request filtering
- Provide a unified entry point for clients

---

### Data Ownership

The API Gateway does not own or persist any business data.

---

### Incoming Requests

- Web Application
- Mobile Application
- Future Third-Party Clients

---

### Outgoing Communication

Routes requests to:

- Authentication Service
- User Service
- Event Service
- Booking Service
- Notification Service

---

### Dependencies

- Spring Cloud Gateway
- Spring Security
- JWT
- Kubernetes Service Discovery

---

### Notes

The API Gateway should remain lightweight and should never contain business logic. Its responsibility is limited to routing, security, and request management.

---

# Business Services

## Authentication Service

### Purpose

The Authentication Service is responsible for verifying user identities and issuing secure authentication tokens. It acts as the central authentication provider for the EventHub platform.

---

### Responsibilities

- User registration
- User login
- Password management
- JWT token generation
- JWT token validation
- Refresh token management (future enhancement)

---

### Data Ownership

Owns and manages:

- User credentials
- Authentication data
- User roles
- Permissions

---

### Incoming Requests

Receives requests from:

- API Gateway

---

### Outgoing Communication

- Returns JWT tokens to the API Gateway
- Shares authenticated user information with other services when required

---

### Dependencies

- PostgreSQL
- Spring Security
- JWT
- BCrypt Password Encoder

---

### Notes

The Authentication Service is responsible only for identity verification and access control. Business-related user information is managed separately by the User Service.

---

## User Service

### Purpose

The User Service manages user profile information and account-related details. It is responsible for maintaining user data beyond authentication.

---

### Responsibilities

- Manage user profiles
- Update personal information
- Manage profile preferences
- View user account details
- Support future profile enhancements

---

### Data Ownership

Owns and manages:

- User profile
- Name

- Email
- Phone number
- Profile picture
- User preferences

---

### Incoming Requests

Receives requests from:

- API Gateway

---

### Outgoing Communication

- Provides user profile information to authorized services when required
- Publishes profile update events for future integrations

---

### Dependencies

- PostgreSQL
- Spring Boot
- Kafka (future event publishing)

---

### Notes

The User Service manages profile information only. Authentication, password management, and token generation are handled exclusively by the Authentication Service.

---

## Event Service

### Purpose

The Event Service manages the complete lifecycle of events, including event creation, updates, publishing, and retrieval. It acts as the central service for all event-related operations within the EventHub platform.

---

### Responsibilities

- Create new events
- Update event details
- Delete events
- Publish and unpublish events
- Manage event categories
- Associate events with venue information
- Manage event metadata and media references
- Trigger search indexing events

---

### Data Ownership

Owns and manages:

- Event information
- Event descriptions
- Categories
- Venue details
- Event images and metadata
- Event status

---

### Incoming Requests

Receives requests from:

- API Gateway

---

### Outgoing Communication

- Publishes **EventCreated** events
- Publishes **EventUpdated** events
- Publishes **EventDeleted** events
- Sends event notifications to Kafka for downstream consumers

---

### Dependencies

- MongoDB
- Apache Kafka
- Elasticsearch (through indexing process)
- Redis (for frequently accessed event data)

---

### Notes

The Event Service is the source of truth for all event-related information. Search data stored in Elasticsearch is derived from this service and should never be updated directly.

---

## Booking Service

### Purpose

The Booking Service manages ticket bookings, reservations, and booking history. It ensures that booking requests are processed reliably while maintaining data consistency.

---

### Responsibilities

- Create bookings
- Cancel bookings
- Retrieve booking history
- Validate booking eligibility and availability
- Manage booking status
- Publish booking-related events

---

### Data Ownership

Owns and manages:

- Booking records
- Booking status
- Reservation details
- Booking history
- Ticket information

---

### Incoming Requests

Receives requests from:

- API Gateway

---

### Outgoing Communication

- Publishes **BookingCreated** events
- Publishes **BookingCancelled** events
- Sends booking notifications through Kafka
- Shares booking information with the Notification Service when required

---

### Dependencies

- PostgreSQL
- Apache Kafka
- Redis (future caching)

---

### Notes

The Booking Service is the source of truth for all booking-related information. It validates booking requests and publishes events for downstream services without directly managing notifications.

---

## Notification Service

### Purpose

The Notification Service is responsible for delivering notifications to users based on events occurring within the EventHub platform. It processes notification requests asynchronously without affecting the performance of core business services.

---

### Responsibilities

- Send email notifications
- Send booking confirmations
- Send event-related notifications
- Process notification requests from Kafka
- Manage notification status
- Support future notification channels such as SMS and push notifications

---

### Data Ownership

Owns and manages:

- Notification records
- Notification status
- Delivery history
- Notification templates (future enhancement)

---

### Incoming Requests

Receives events from:

- Apache Kafka

---

### Outgoing Communication

- Sends emails to users
- Integrates with external notification providers
- Publishes notification status events (future enhancement)

---

### Dependencies

- Apache Kafka
- PostgreSQL
- Email Service Provider (SMTP or third-party provider)

---

### Notes

The Notification Service operates asynchronously and should not be part of synchronous business workflows. Failures in notification delivery should not impact booking or event operations.

---

# Service Responsibility Summary

The following table provides a high-level overview of the primary responsibility of each service within the EventHub platform.

| Service | Primary Responsibility |
|----------|------------------------|
| API Gateway | Request routing, authentication, and request filtering |
| Authentication Service | User authentication, authorization, and JWT management |
| User Service | User profile and account management |
| Event Service | Event lifecycle management and event publishing |
| Booking Service | Ticket booking, reservations, and booking management |
| Notification Service | Asynchronous notification processing and delivery |

---

# Database Ownership

Each microservice owns its data and is the only service allowed to read from or write to its database.

Services must never directly access another service's database. Any required information should be obtained through REST APIs or asynchronous events.

| Service | Primary Database | Data Owned |
|----------|------------------|------------|
| Authentication Service | PostgreSQL | User credentials, roles, and permissions |
| User Service | PostgreSQL | User profiles and preferences |
| Event Service | MongoDB | Events, categories, venue details, and metadata |
| Booking Service | PostgreSQL | Bookings, reservations, and booking history |
| Notification Service | PostgreSQL | Notification records and delivery history |

By ensuring that each service owns and manages its own data, EventHub maintains loose coupling, enables independent deployments, and allows individual services to evolve without impacting other parts of the system.

---

# Service Communication Summary

EventHub uses a combination of synchronous REST APIs and asynchronous event-driven messaging to enable communication between services.

## Synchronous Communication

REST APIs are used when an immediate response is required.

Examples include:

- API Gateway → Authentication Service
- API Gateway → User Service
- API Gateway → Event Service
- API Gateway → Booking Service

This communication pattern is suitable for request-response operations such as user authentication, profile management, event retrieval, and booking requests.

---

## Asynchronous Communication

Apache Kafka is used for asynchronous communication where immediate responses are not required.

Examples include:

- EventCreated
- EventUpdated
- EventDeleted
- BookingCreated
- BookingCancelled

This approach enables services to process events independently, improving scalability, fault tolerance, and loose coupling across the platform.

## High-Level Communication Flow

```text
                        Client
    │
    ▼
API Gateway
    │
    ▼
Booking Service
    │
    ├──────────────► Event Service
    │                    │
    │                    ▼
    │              Validate Event
    │
    ▼
Create Booking
    │
    ▼
Publish BookingCreated
    │
    ▼
Kafka
    │
    ▼
Notification Service
```

---

# Guiding Principles

The service boundaries in EventHub are designed around the following principles:

- Each service is responsible for a single business capability.
- Every service owns and manages its own data.
- Services communicate through APIs or asynchronous events.
- Business logic remains within the owning service.
- Services can be developed, deployed, and scaled independently.
- Event-driven communication is preferred for non-blocking workflows.
- Infrastructure responsibilities remain separate from business responsibilities.

---

# Out of Scope

This document does not cover:

- REST API endpoint definitions
- Database schema design
- Internal service implementation
- Class and package structure
- Deployment configuration
- Security implementation details
- Monitoring and observability configuration

These topics are documented separately in their respective architecture documents.

---

