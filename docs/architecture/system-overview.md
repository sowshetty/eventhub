# System Overview

**Project:** EventHub  
**Version:** 1.0  
**Status:** Draft  
**Last Updated:** 2026-07-20

---

# Purpose

This document provides a high-level overview of the EventHub system architecture.

It introduces the major components of the platform, explains how they interact, and defines the architectural principles that guide the implementation of all services.

This document serves as the entry point for understanding the overall system before diving into service-specific or implementation-level documentation.

---

# Project Overview

EventHub is a cloud-native, enterprise-grade Event Management Platform built using a Microservices Architecture.

The platform enables users to:

- Register and manage accounts
- Discover and search events
- Create and manage events
- Book event tickets
- Receive booking confirmations and notifications
- View booking history

The project is designed as a portfolio-quality enterprise application that demonstrates modern software engineering practices using Java, Spring Boot, Docker, Kubernetes, Kafka, Redis, MongoDB, Elasticsearch, PostgreSQL, and cloud-native architecture principles.

---

# Business Goals

The architecture has been designed to achieve the following goals:

- Independent service development
- Independent deployments
- Horizontal scalability
- High availability
- Fault isolation
- Cloud-native deployment
- High-performance search
- Distributed caching
- Event-driven communication
- Production-ready observability

---

# Architectural Style

EventHub follows a **Microservices Architecture**.

Each service:

- Owns a single business capability
- Owns its own data
- Can be deployed independently
- Can be scaled independently
- Has its own lifecycle
- Communicates using REST APIs and Kafka events

The architecture also incorporates:

- Database per Service
- Polyglot Persistence
- API-First Development
- Event-Driven Architecture
- Cloud-Native Design
- Infrastructure as Code

---

# High-Level Components

## API Gateway

Responsibilities:

- Single entry point
- Request routing
- Authentication forwarding
- Rate limiting (future)
- Request validation
- Cross-cutting concerns

---

## Authentication Service

Responsibilities:

- User Registration
- Login
- JWT Token Generation
- Token Validation
- Password Management

Primary Database:

- PostgreSQL

---

## User Service

Responsibilities:

- User Profile
- Preferences
- Account Management

Primary Database:

- PostgreSQL

---

## Event Service

Responsibilities:

- Event Creation
- Event Management
- Event Publishing
- Event Search Integration
- Organizer Information

Primary Database:

- MongoDB

Search Index:

- Elasticsearch

Cache:

- Redis

---

## Booking Service

Responsibilities:

- Ticket Booking
- Booking History
- Booking Management

Primary Database:

- PostgreSQL

Cache:

- Redis

---

## Notification Service

Responsibilities:

- Email Notifications
- Booking Confirmation
- Event Reminder
- Future SMS Notifications
- Future Push Notifications

Primary Database:

- PostgreSQL

---

# High-Level System Architecture

```
                           Client Applications
                   (Web | Mobile | Third-Party APIs)
                                   │
                                   ▼
                          +------------------+
                          |   API Gateway    |
                          +------------------+
                                   │
        ┌───────────────┬──────────┼───────────────┬──────────────┐
        ▼               ▼          ▼               ▼              ▼
+---------------+ +--------------+ +--------------+ +--------------+ +------------------+
| Auth Service  | | User Service | | Event Service| |BookingService| |NotificationService|
+---------------+ +--------------+ +--------------+ +--------------+ +------------------+
       │                 │                 │                 │                  │
       ▼                 ▼                 ▼                 ▼                  ▼
 PostgreSQL         PostgreSQL         MongoDB         PostgreSQL         PostgreSQL
                                           │
                                           ▼
                                   Elasticsearch
                                           ▲
                                           │
                                  Search Index Updates

                 ──────────────────────────────────────────────

                         Redis (Distributed Cache)

                 ──────────────────────────────────────────────

                         Apache Kafka Event Bus

         UserRegistered
         EventCreated
         BookingCreated
         BookingCancelled
         NotificationRequested
```

---

# Communication Model

EventHub uses both synchronous and asynchronous communication.

## Synchronous Communication

REST APIs are used whenever an immediate response is required.

Examples:

- Login
- Register
- Get User Profile
- Create Booking
- View Booking History

---

## Asynchronous Communication

Apache Kafka is used for event-driven communication.

Examples:

- UserRegistered
- EventCreated
- BookingCreated
- BookingCancelled
- NotificationRequested

Benefits:

- Loose coupling
- Better scalability
- Independent processing
- Improved fault tolerance

---

# Database Strategy

EventHub follows both the **Database per Service** pattern and **Polyglot Persistence**.

Each service owns its data and selects the most appropriate storage technology based on its business requirements.

## PostgreSQL

Used for transactional data requiring ACID guarantees.

Examples:

- User Accounts
- Authentication
- Bookings
- Future Payment Module

---

## MongoDB

Used for document-oriented data with evolving schemas.

Examples:

- Event Information
- Event Schedules
- Rich Event Descriptions
- Organizer Profiles
- Media Metadata

---

## Elasticsearch

Used as a dedicated search engine.

Examples:

- Event Search
- Full-Text Search
- Autocomplete
- Filtering
- Sorting
- Relevance Ranking

Elasticsearch acts as a search index and is synchronized from MongoDB using Kafka events.

---

## Redis

Redis is used as a distributed cache.

Examples:

- Frequently Viewed Events
- User Sessions
- JWT Blacklisting (Future)
- API Response Caching
- Rate Limiting Data

Redis is not used as the system of record.

---

# Event Flow

The Event Service demonstrates multiple enterprise architecture patterns.

### Event Creation Flow

1. Organizer creates an event.
2. Event is stored in MongoDB.
3. Event Service publishes an **EventCreated** event to Kafka.
4. Search Index Consumer receives the event.
5. Elasticsearch indexes the event.
6. Frequently accessed data is cached in Redis.
7. Users search events through Elasticsearch.

This approach combines:

- Polyglot Persistence
- Event-Driven Architecture
- Search Indexing
- Distributed Caching

---

# Deployment Strategy

EventHub is designed for Kubernetes deployment.

Key principles:

- Docker Containers
- Kubernetes Deployments
- Kubernetes Services
- ConfigMaps
- Secrets
- Horizontal Pod Autoscaling
- Rolling Updates
- Self-Healing
- Service Discovery

Service discovery is handled by Kubernetes networking rather than Netflix Eureka.

---

# Security Overview

Authentication:

- Spring Security
- JWT

Authorization:

- Role-Based Access Control (RBAC)

Passwords:

- BCrypt

Secrets:

- Kubernetes Secrets

Future Enhancements:

- OAuth2
- Social Login
- Multi-Factor Authentication

---

# Observability

EventHub includes built-in observability.

Monitoring Stack:

- Micrometer
- Prometheus
- Grafana

Tracing:

- OpenTelemetry

Logging:

- Centralized Logging

Health Monitoring:

- Spring Boot Actuator

---

# Technology Stack

| Layer | Technology |
|---------|------------|
| Language | Java 21 |
| Framework | Spring Boot 3.x |
| Security | Spring Security + JWT |
| API Gateway | Spring Cloud Gateway |
| Relational Database | PostgreSQL |
| Document Database | MongoDB |
| Search Engine | Elasticsearch |
| Cache | Redis |
| Messaging | Apache Kafka |
| API Documentation | OpenAPI / Swagger |
| Build Tool | Maven |
| Containerization | Docker |
| Orchestration | Kubernetes |
| Monitoring | Micrometer |
| Metrics | Prometheus |
| Dashboard | Grafana |
| Tracing | OpenTelemetry |
| CI/CD | GitHub Actions |

---

# Design Principles

The EventHub architecture follows these principles:

- Single Responsibility Principle
- Separation of Concerns
- API First
- Database per Service
- Polyglot Persistence
- Event-Driven Architecture
- Cloud-Native Design
- Infrastructure as Code
- Twelve-Factor App
- Independent Deployability

---

# Related Documents

- README.md
- technology-stack.md
- service-boundaries.md
- communication-patterns.md
- deployment-architecture.md
- security-architecture.md
- observability.md
- architecture-principles.md
- Architecture Decision Records (ADRs)

---

# Version History

| Version | Date | Author | Changes |
|----------|------------|-------------|--------------------------------|
| 1.0 | 2026-07-20 | Project Team | Initial system overview |