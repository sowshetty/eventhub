# EventHub

> Enterprise-grade Cloud-Native Event Management Platform

EventHub is a production-grade cloud-native event management platform designed to demonstrate modern enterprise backend engineering using Java 21, Spring Boot, Microservices, Event-Driven Architecture, Cloud, and DevOps technologies.

The platform enables organizations to create, manage, discover, and book events such as conferences, workshops, corporate events, concerts, webinars, and meetups through a scalable microservices architecture.

---

# Project Vision

To design and develop a modern enterprise backend platform by following real-world software engineering practices used in today's product-based companies.

This project focuses on writing clean, maintainable, scalable, secure, and production-ready backend services while adopting cloud-native architecture and DevOps practices.

---

# Business Goals

- User Registration & Authentication
- Organization Management
- Event Management
- Venue Management
- Ticket Booking
- Event Search
- Notification Management
- Analytics Dashboard
- Audit Logging

---

# Technology Stack

| Category | Technology |
|-----------|------------|
| Language | Java 21 LTS (Oracle JDK) |
| Framework | Spring Boot 3.5.x |
| Microservices | Spring Cloud |
| Security | Spring Security, JWT |
| Database | PostgreSQL |
| Database Migration | Flyway |
| Messaging | Apache Kafka |
| API Documentation | Swagger / OpenAPI |
| Build Tool | Maven |
| Version Control | Git & GitHub |
| Containerization | Docker & Docker Compose |
| CI/CD | GitHub Actions, Jenkins |
| Orchestration | Kubernetes |
| Cloud | AWS |
| Monitoring | Spring Boot Actuator |
| Phase 2 | Elasticsearch, Redis, Prometheus, Grafana |
---

# Core Technologies

- Java 21 LTS
- Spring Boot 3.5.x
- Spring Cloud
- Spring Security
- Spring Data JPA
- Spring Cloud Gateway
- Apache Kafka
- PostgreSQL
- Flyway
- Docker
- Kubernetes
- GitHub Actions
- Jenkins
- Swagger / OpenAPI
- AWS (Deployment)

---

# High-Level Architecture

```text
                               Client
                                  │
                                  ▼
                            API Gateway
                                  │
          ┌───────────────────────┼────────────────────────┐
          ▼                       ▼                        ▼
 Authentication Service     User Service          Event Service
                                                          │
                                                          ▼
                                                   Booking Service
                                                          │
                                                          ▼
                                                   Payment Service

                      ─────────── Kafka Event Bus ───────────

                            ▼                      ▼
                 Notification Service     Analytics Service


           Discovery Server      Configuration Server
```

> Each microservice owns its database and communicates synchronously using REST APIs and asynchronously using Apache Kafka events.

---

# Repository Structure

```text
eventhub/
│
├── docs/
│   ├── architecture/
│   ├── design/
│   ├── api/
│   ├── database/
│   ├── operations/
│   ├── prd.md
│   ├── frd.md
│   └── learning-journal.md
│
├── services/
│
├── infrastructure/
│   ├── docker/
│   └── kubernetes/
│
├── scripts/
│
├── README.md
├── CHANGELOG.md
├── ENGINEERING-PORTFOLIO.md
└── .gitignore
```

---

# Engineering Principles

EventHub follows modern enterprise software engineering principles:

- Clean Architecture
- SOLID Principles
- Layered Architecture
- API-First Development
- Documentation-First Development
- Event-Driven Architecture
- Secure Coding Practices
- Container-First Development
- Continuous Integration & Continuous Delivery
- Observability & Monitoring
- Code Reviews
- Automated Testing

---

# Development Workflow

Every feature follows the same engineering workflow.

```
Requirement
      ↓
Architecture
      ↓
Implementation
      ↓
Testing
      ↓
Documentation
      ↓
Git Commit
      ↓
Code Review
      ↓
Deployment
```

---

# Current Status

**Current Version:** 0.2.0

**Current Sprint:** Sprint 1 – Implementation

**Project Status:** 🟢 Architecture Complete | Ready for Development

## Completed

- Product Requirements Document (PRD)
- Functional Requirements Document (FRD)
- System Architecture
- Infrastructure Architecture
- Service Design Documents
- Database Design
- Learning Journal
- Engineering Portfolio
- Changelog

## Next Milestone

- Discovery Server
- Configuration Server
- API Gateway
- Authentication Service
- JWT Security
- Flyway Integration
---

# Roadmap

| Sprint | Milestone | Status |
|---------|-----------|--------|
| Sprint 0 | Project Planning & Architecture | ✅ Completed |
| Sprint 1 | Infrastructure Services (Discovery, Config, API Gateway) | 🔄 Next |
| Sprint 2 | Authentication & User Service | ⏳ Planned |
| Sprint 3 | Event Management Service | ⏳ Planned |
| Sprint 4 | Booking & Payment Services | ⏳ Planned |
| Sprint 5 | Notification & Analytics Services | ⏳ Planned |
| Sprint 6 | Docker, CI/CD & Kubernetes | ⏳ Planned |
| Sprint 7 | Monitoring & Observability | ⏳ Planned |
| Sprint 8 | Elasticsearch Integration & Production Readiness | ⏳ Planned |

---

# Documentation

The project documentation is organized under the `docs/` directory.

- Product Requirements Document (PRD)
- Functional Requirements Document (FRD)
- Architecture Documents
- Service Design Documents
- Database Design
- Learning Journal
- Engineering Portfolio
- Changelog

Documentation will continue to evolve alongside the implementation while avoiding unnecessary duplication.

---

# License

License information will be finalized before Version 1.0 release.

---

# Maintainer

Sowmyaa Shetty