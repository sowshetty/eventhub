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
| Language | Java 21 LTS |
| Framework | Spring Boot 3.x |
| Security | Spring Security, JWT |
| Database | PostgreSQL |
| NoSQL | MongoDB |
| Cache | Redis |
| Search | Elasticsearch |
| Messaging | Apache Kafka |
| API Documentation | Swagger / OpenAPI |
| Build Tool | Maven |
| Version Control | Git & GitHub |
| Containerization | Docker & Docker Compose |
| CI/CD | Jenkins, GitHub Actions |
| Orchestration | Kubernetes |
| Cloud | AWS |
| Monitoring | Spring Boot Actuator, Prometheus, Grafana 

---

# Core Technologies

- Java 21 LTS
- Spring Boot 3.x
- Spring Security
- Spring Data JPA
- Spring Cloud Gateway
- Apache Kafka
- PostgreSQL
- MongoDB
- Redis
- Elasticsearch
- Docker
- Kubernetes
- Jenkins
- GitHub Actions
- AWS
- Swagger / OpenAPI

---

# High-Level Architecture

```
                API Gateway
                     │
      ┌──────────────┼──────────────┐
      │              │              │
 Authentication   User Service   Event Service
                                     │
                              Booking Service
                                     │
                           Notification Service
                                     │
                             Search Service
                                     │
                           Analytics Service
```

> Detailed architecture diagrams will be added in future sprints.

---

# Repository Structure

```
eventhub/
│
├── backend/
├── docs/
├── architecture/
├── docker/
├── kubernetes/
├── monitoring/
├── openapi/
├── scripts/
│
├── README.md
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

Current Development Stage: Sprint 0 – Project Foundation

**Version:** 0.1

**Sprint:** Sprint 0

**Status:** Planning & Architecture Phase

---

# Roadmap

- Sprint 0 – Planning & Architecture
- Sprint 1 – Authentication Service
- Sprint 2 – User & Organization Services
- Sprint 3 – Event Management
- Sprint 4 – Booking & Notifications
- Sprint 5 – Search & Analytics
- Sprint 6 – Docker, Jenkins & GitHub Actions
- Sprint 7 – Kubernetes & AWS
- Sprint 8 – Monitoring, Testing & Interview Preparation

---

# Documentation

Project documentation will be maintained under the `docs/` directory.

Additional architecture documents, API specifications, deployment guides, and technical notes will be added incrementally during development.

---

# License

License information will be finalized before Version 1.0 release.

---

# Maintainer

Sowmyaa Shetty