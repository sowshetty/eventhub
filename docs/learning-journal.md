# Learning Journal

This journal documents my daily learning journey while building **EventHub**, a production-grade cloud-native backend application as part of my Java Backend Engineering Masterclass.

The objective is to understand not only *how* technologies are used, but *why* they are used in modern enterprise software development.

---

# Sprint 0

---

# Day 1 - Project Foundation

**Date:** 17 July 2026

## Objective

Lay the foundation for the EventHub project by setting up the GitHub repository, understanding Git workflow, defining the project direction, and preparing the development environment.

---

## What I Learned

### Git Fundamentals

# Day 2 - Understanding Product Requirements Document (PRD)

**Date:** 18 July 2026

## Objective

Understand the purpose of a Product Requirements Document (PRD) and how software products are planned before development begins.

---

## What I Learned

- A PRD defines **what** needs to be built and **why** it should be built.
- A PRD intentionally avoids implementation details.
- It serves as a common reference for Product Managers, Business Analysts, Architects, Developers, QA Engineers, and other stakeholders.
- The EventHub project will follow a documentation-first approach before writing production code.

---

## Key Takeaways

- Product requirements should be clearly defined before designing the system.
- Good documentation reduces misunderstandings during development.
- Software engineering starts with understanding the business problem, not writing code.

---

## Questions for Tomorrow

- How do we convert business requirements into functional requirements?
- What sections should be included in a professional PRD?
- How do we define the scope of Version 1.0?

---

## Status

Sprint 0 – Day 2 In Progress ✅

- Difference between Git and GitHub.
- Difference between Local Repository and Remote Repository.
- How Git tracks changes using commits.
- Why commit messages should follow professional conventions.
- Basic Git workflow:
  - git init
  - git add
  - git commit
  - git remote
  - git push

---

### GitHub Repository

Created a public GitHub repository:

EventHub

Learned:

- Repository naming conventions
- Public vs Private repositories
- Why not to initialize the repository with README or .gitignore when learning Git from scratch
- How local and remote repositories are connected

---

### Markdown Documentation

Learned that:

- README.md is written using Markdown.
- Markdown is preferred over Word documents because:
  - It is plain text.
  - Git can track changes efficiently.
  - GitHub automatically renders Markdown.
  - It supports headings, tables, images, links, code blocks, and diagrams.

---

### README

Created the initial README containing:

- Project Overview
- Vision
- Business Goals
- Technology Stack
- High-Level Architecture
- Repository Structure
- Engineering Principles
- Development Workflow
- Roadmap

---

### Git Ignore

Created a custom .gitignore file.

Learned why generated files should never be committed into Git.

---

### Project Vision

Finalized the project:

EventHub

Enterprise-grade Cloud-Native Event Management Platform

Purpose:

To build a production-style backend system using modern Java backend technologies and enterprise engineering practices.

---

### Technology Stack (Finalized)

- Java 21
- Spring Boot 3
- Spring Security
- PostgreSQL
- MongoDB
- Redis
- Elasticsearch
- Apache Kafka
- Docker
- Kubernetes
- Jenkins
- GitHub Actions
- AWS
- Swagger / OpenAPI
- JUnit 5
- Mockito
- REST Assured

---

### Engineering Practices

Introduced to:

- Documentation First Development
- API First Development
- Clean Architecture
- SOLID Principles
- Conventional Commits
- Professional Git Workflow

---

## Challenges Faced

- GitHub rejected the initial push due to email privacy protection.
- Understood how GitHub verifies commit author email.
- Successfully resolved the issue and pushed the repository.

---

## Key Takeaways

- Git is a version control system.
- GitHub is a remote hosting platform for Git repositories.
- A commit saves changes locally.
- Push uploads commits to GitHub.
- README is the homepage of a GitHub project.
- Good documentation is as important as writing good code.

---

## Questions for Tomorrow

- Why should this project use microservices instead of a monolith?
- How should we divide the microservices?
- Why are we using PostgreSQL, MongoDB, Redis, and Elasticsearch together?
- How should the project be structured using Maven?
- What are the responsibilities of each service?

---

## Time Spent

Approximately 3–4 hours

---

## Status

Sprint 0 – Day 1 Completed ✅

# Day 2 - Understanding Product Requirements Document (PRD)

**Date:** 18 July 2026

## Objective

Understand the purpose of a Product Requirements Document (PRD) and how software products are planned before development begins.

---

## What I Learned

- A PRD defines **what** needs to be built and **why** it should be built.
- A PRD intentionally avoids implementation details.
- It serves as a common reference for Product Managers, Business Analysts, Architects, Developers, QA Engineers, and other stakeholders.
- The EventHub project will follow a documentation-first approach before writing production code.

---

## Key Takeaways

- Product requirements should be clearly defined before designing the system.
- Good documentation reduces misunderstandings during development.
- Software engineering starts with understanding the business problem, not writing code.

---

## Questions for Tomorrow

- How do we convert business requirements into functional requirements?
- What sections should be included in a professional PRD?
- How do we define the scope of Version 1.0?

---

## Status

Sprint 0 – Day 2 Completed✅

---

# Day 3 - Writing the Product Requirements Document (PRD)

**Date:** 19 July 2026

## Objective

Create the first version of the Product Requirements Document (PRD) for the EventHub project and understand how software products are planned before development begins.

---

## What I Learned

### Product Requirements Document (PRD)

- A PRD defines **what** the product should do and **why** it should exist.
- It does not describe implementation details such as programming languages, databases, or frameworks.
- A PRD acts as the foundation for architecture, development, testing, and deployment planning.

---

### Structure of a Professional PRD

Learned the purpose of the following sections:

- Document Information
- Product Overview
- Business Problem
- Vision Statement
- Objectives
- Target Users
- Scope
- Functional Features
- Non-Functional Expectations
- Out of Scope
- Assumptions
- Constraints
- Success Metrics
- Future Enhancements
- Version History

---

### Product Thinking

Understood how to define:

- The business problem
- Product vision
- Primary objectives
- User roles
- MVP scope
- Features intentionally excluded from Version 1.0

---

### EventHub Product Vision

Defined EventHub as an:

> Enterprise-grade Cloud-Native Event Management Platform

Designed for:

- Customers
- Organizers
- Administrators

---

### MVP Features

Finalized Version 1.0 features:

- User Registration
- Login
- JWT Authentication
- Event Management
- Event Search
- Ticket Booking
- Booking History
- Notifications
- Basic Administration
- Basic Analytics

---

### Software Engineering Concepts

Learned the difference between:

- PRD (What & Why)
- FRD (How the business functionality behaves)
- HLD (Overall Architecture)
- LLD (Detailed Technical Design)

---

## Challenges Faced

- Understanding the difference between business requirements and technical implementation.
- Learning to keep implementation details out of the PRD.

---

## Key Takeaways

- Every successful software product starts with understanding the business problem.
- Good documentation reduces confusion during development.
- Defining project scope early helps prevent scope creep.
- A clear PRD makes architecture and implementation easier.

---

## Questions for Tomorrow

- What is an FRD?
- How is an FRD different from a PRD?
- How are business requirements converted into functional requirements?
- How do we prepare the project for architecture design?

---

## Time Spent

Approximately 2–3 hours

---

## Status

Sprint 0 – Day 3 Completed ✅

---

# Sprint 0 – Day 4
## Topic: Functional Requirements Document (FRD)

**Date:** 19 July 2026

---

# Objective

Understand the purpose of a Functional Requirements Document (FRD) and learn how business requirements are converted into detailed functional specifications before software development begins.

---

# Theory Learned

Today I learned that a Functional Requirements Document (FRD) defines how a software system should behave from the business and user perspective.

Unlike the Product Requirements Document (PRD), which explains what the product is and why it is needed, the FRD focuses on the detailed functionality of the application.

The FRD acts as a bridge between business requirements and software design. It provides developers, testers, architects, and business analysts with a common understanding of how the application should function.

---

# Why an FRD is Important

An FRD helps ensure that everyone involved in the project understands the expected behavior of the system before implementation begins.

Benefits include:

- Eliminates ambiguity in requirements
- Defines expected system behavior
- Helps developers understand business expectations
- Provides a reference for QA and testing
- Reduces misunderstandings during development
- Improves communication between business and technical teams

---

# Practical Work Completed

Completed the Version 1.0 Functional Requirements Document (FRD) for the EventHub project.

The document includes:

- Purpose
- Functional Overview
- User Roles
- Functional Requirements
- Business Rules
- Validation Rules
- Error Handling
- Functional Flow
- Assumptions
- Out of Scope
- Future Enhancements
- Version History

Saved the document as:

```
docs/frd.md
```

Committed and pushed the document to the GitHub repository.

---

# Functional Modules Identified

The EventHub application consists of the following major functional modules:

- User Registration
- User Authentication
- User Profile
- Event Management
- Event Search
- Ticket Booking
- Booking Management
- Administrator Module

Each module has clearly defined responsibilities and expected behavior.

---

# Business Rules Learned

Examples of business rules documented today include:

- Email address must be unique.
- Passwords must be encrypted.
- Event dates cannot be in the past.
- Booking is allowed only if seats are available.
- Duplicate bookings are not permitted.
- Organizers can manage only their own events.

Business rules define the constraints that the application must always follow.

---

# Validation Rules Learned

Validation ensures that user input is correct before processing.

Examples include:

- Mandatory fields for registration.
- Mandatory fields for event creation.
- Capacity must be greater than zero.
- Event title cannot be empty.
- Valid email format is required.

---

# Error Handling

Instead of returning generic errors, the system should provide meaningful business messages.

Examples:

- Email already registered
- Invalid email or password
- Event not found
- Event is full
- Authentication required
- Access denied

These messages improve user experience and simplify troubleshooting.

---

# New Concepts Learned

- Functional Requirements
- Business Rules
- Validation Rules
- Functional Modules
- User Roles
- Functional Flow
- Error Handling
- Requirement Traceability

---

# Difference Between PRD and FRD

| PRD | FRD |
|------|------|
| Defines what should be built | Defines how the system should behave |
| Focuses on business goals | Focuses on functional behavior |
| Product-oriented | User and system-oriented |
| Created before FRD | Created after PRD |

---

# Git Activity

Updated project documentation.

Typical Git workflow:

```bash
git status
git add .
git commit -m "docs: add functional requirements document"
git push
```

---

# Interview Questions

### Q1. What is a Functional Requirements Document (FRD)?

A Functional Requirements Document defines the expected behavior of a software application from the user's and business perspective. It describes features, workflows, validations, business rules, and functional requirements without specifying technical implementation.

---

### Q2. What is the difference between PRD and FRD?

PRD explains what the product is and why it should be built.

FRD explains how the system should behave to satisfy those business requirements.

---

### Q3. Who prepares an FRD?

Typically, a Business Analyst or Product Analyst prepares the FRD with input from Product Managers and stakeholders.

---

### Q4. Who uses the FRD?

- Software Developers
- QA Engineers
- Solution Architects
- Product Owners
- Business Analysts

---

# Challenges Faced

Understanding the difference between business requirements and technical implementation.

Initially, it was tempting to think about Spring Boot classes and APIs while writing the FRD, but I learned that an FRD should remain technology-independent and focus only on system functionality.

---

# Key Takeaways

- Requirements should always be documented before coding.
- The FRD describes system behavior, not implementation.
- Business rules are different from technical implementation.
- Validation rules improve data quality.
- Error handling should provide meaningful messages.
- Good documentation reduces development risk and improves communication across teams.

---

# Next Day Goal

Learn High-Level Design (HLD) and understand how enterprise applications are architected before implementation begins.

Topics to cover:

- System Architecture
- Microservices
- Component Diagram
- Technology Stack
- High-Level Data Flow
- Integration Overview

---

# Status

✅ Sprint 0 – Day 4 Completed

---

# Date: 2026-07-19

## Sprint 1

Sprint 1 – Architecture & Design
---

# Session Objectives

Today's objective was to finalize the EventHub repository structure and establish the engineering foundation before beginning architecture documentation and implementation.

Instead of rushing into coding, the focus was on making architectural decisions that would influence the project throughout its lifecycle.

---

# Work Completed

## Repository Structure

Finalized and locked Repository Structure Version 1.0.

```
EventHub/
│
├── .github/
│
├── services/
│
├── docs/
│   ├── architecture/
│   │   ├── adr/
│   │   └── diagrams/
│   ├── api/
│   ├── database/
│   ├── operations/
│   ├── prd.md
│   ├── frd.md
│   └── learning-journal.md
│
├── infrastructure/
│   ├── docker/
│   └── kubernetes/
│
├── scripts/
│
├── README.md
├── CHANGELOG.md
└── ENGINEERING-PORTFOLIO.md
```

Repository structure has now been frozen before implementation begins.

---

# Major Engineering Discussions

## 1. Monorepo vs Multi-repo

One of today's most important discussions was selecting the repository strategy.

### Monorepo

Advantages

- Easier project setup
- Single Git repository
- Easier local development
- Easier architectural consistency
- Shared CI/CD pipeline if desired
- Better suited for learning and portfolio projects

Disadvantages

- Larger repository size over time
- Requires discipline to maintain service independence

### Multi-repo

Advantages

- Complete service independence
- Independent release cycles
- Smaller repositories

Disadvantages

- Harder local development
- More repositories to manage
- More complicated onboarding
- More CI/CD pipelines

### Final Decision

EventHub will use a **Monorepo**.

Reason:

Although services will be independently deployable, keeping them in one repository makes the project easier to learn, maintain, review, and present as a portfolio while still following microservice principles.

---

## 2. Independent Microservices

Discussed whether services should share code.

Conclusion:

Every microservice should own:

- Business Logic
- Database
- Dependencies
- Build
- Deployment
- Release Lifecycle

Each service should remain independently deployable.

---

## 3. Shared Libraries

Initially discussed creating a shared module.

After evaluating modern microservice practices, this idea was rejected.

Reason:

Sharing business code creates tight compile-time coupling between services.

Future changes in one service can unintentionally affect others.

Instead:

Business logic will remain inside each service.

Only engineering standards may be shared through documentation rather than shared code.

---

## 4. Parent POM

Discussed using a common Maven Parent POM.

Advantages considered:

- Common dependency versions
- Plugin management
- Centralized build configuration

Disadvantages:

- Tight build coupling
- Every service depends on a common parent
- Reduced service autonomy

Decision:

Each microservice will maintain its own `pom.xml`.

Dependency versions will be updated independently when required.

This aligns with modern cloud-native microservice practices.

---

## 5. Repository Organization

Several repository layouts were evaluated.

Rejected

```
backend/
```

Reason:

EventHub contains multiple backend applications rather than one backend.

Chosen

```
services/
```

Reason:

Each directory inside `services` represents an independent deployable microservice.

---

Rejected

```
architecture/
```

at repository root.

Chosen

```
docs/architecture/
```

Reason:

Architecture is documentation rather than executable code.

---

Rejected

```
openapi/
```

at repository root.

Chosen

```
docs/api/
```

Reason:

OpenAPI specifications are documentation.

---

Rejected

```
monitoring/
```

at repository root.

Reason:

Monitoring infrastructure has not yet been implemented.

Future monitoring resources will be added when observability is implemented.

---

# Repository Decisions

The following repository principles were finalized.

- Documentation belongs under `docs`.
- Source code belongs under `services`.
- Infrastructure belongs under `infrastructure`.
- Automation belongs under `scripts`.
- Documentation should be grouped by concern rather than technology.
- Architecture diagrams belong inside `docs/architecture/diagrams`.

Repository Structure Version 1.0 is now locked.

---

# Git Learnings

Today's Git learning included understanding that Git does not track empty directories.

Solutions:

- `.gitkeep`
- `README.md`

Used `.gitkeep` temporarily until real project files are added.

---

# Software Engineering Learnings

Today's session reinforced several software engineering principles.

- Architecture should be planned before implementation.
- Repository organization affects maintainability.
- Documentation is part of engineering, not an afterthought.
- Good folder structures reduce future technical debt.
- Microservices should be independent, not merely separated into folders.
- Build independence is as important as runtime independence.
- Architectural decisions should be documented rather than remembered.

---

# Challenges Faced

Several design questions required discussion before implementation.

- Should the project use Monorepo or Multi-repo?
- Should services share code?
- Should a common Parent POM be used?
- Should there be a backend folder?
- Where should architecture documentation live?
- Where should OpenAPI specifications live?
- Should monitoring exist before implementation?
- How should diagrams be organized?

These discussions helped establish a clean architectural foundation before any code is written.

---

# Outcome

Today's work completed the repository foundation phase.

The project now has:

- Professional repository organization
- Clear documentation strategy
- Defined engineering boundaries
- Independent service philosophy
- Locked repository structure
- Architecture-first development approach

---

# Next Steps

Sprint 1 – Architecture Documentation

Planned documents

1. docs/architecture/README.md
2. system-overview.md
3. technology-stack.md
4. service-boundaries.md
5. communication-patterns.md
6. deployment-architecture.md
7. security-architecture.md
8. observability.md
9. architecture-principles.md

After architecture documentation

- Architecture Decision Records (ADRs)
- High-Level Design (HLD)
- Low-Level Design (LLD)
- Database Design
- OpenAPI Specifications

Finally

Implementation of the first Spring Boot microservice.

---

# Personal Reflection

Although no Java code was written today, one of the most important milestones of the project was achieved.

Today's work established the engineering foundation that will guide every future implementation.

A well-designed repository, clear architectural boundaries, and documented engineering decisions are just as important as writing clean code.

This session reinforced an important lesson:

**Good software architecture begins long before the first line of code is written.**

✅ Sprint 0 – Day 5 Completed

---

**Date:** 2026-07-20

**Sprint:** Sprint 1 – Architecture & Design

---

## Objective

Complete the `technology-stack.md` architecture document by documenting the technologies used in EventHub and the rationale behind each technology selection.

---

## Work Completed

Completed the following sections in `technology-stack.md`:

- Purpose
- Technology Selection Principles
- Backend Technologies
  - Java 21
  - Spring Boot 3.x
  - Spring Cloud Gateway
  - Spring Security + JWT
- Data Layer
  - PostgreSQL
  - MongoDB
  - Elasticsearch
  - Redis
  - Polyglot Persistence Strategy
- Messaging
  - Apache Kafka
- API Documentation
  - OpenAPI 3
  - Swagger UI
- Infrastructure
  - Docker
  - Kubernetes
- Observability
  - Micrometer
  - Prometheus
  - Grafana
  - OpenTelemetry
- Build & CI/CD
  - Maven
  - GitHub Actions
- Technology Compatibility Matrix
- Future Considerations
- Related Documents

---

## Key Concepts Learned

- Technology selection should be based on architectural requirements rather than popularity.
- Polyglot Persistence enables different databases to handle workloads they are best suited for.
- Each technology in a microservices architecture has a specific responsibility and should integrate well with the overall platform.
- Architecture documentation should clearly explain the purpose, rationale, advantages, and trade-offs of each technology.

---

## Interview Notes

Topics reinforced during today's work:

- Why Java 21 and Spring Boot 3.x for enterprise applications?
- What is Polyglot Persistence?
- Why use PostgreSQL and MongoDB together?
- Why use Elasticsearch instead of relying only on relational database search?
- Why Redis for caching?
- Why Kafka in a microservices architecture?
- Difference between Docker and Kubernetes.
- Role of Prometheus, Grafana, and OpenTelemetry in observability.

---

## Challenges Faced

- Keeping the documentation concise while still explaining the reasoning behind each technology choice.
- Maintaining a consistent structure across all technology sections.
- Refining the document by removing duplicate headings and improving readability.

---

## Key Takeaway

A technology stack is more than a list of tools. Each technology should be selected because it addresses a specific architectural need and works effectively with the rest of the system. Understanding these decisions is essential for designing and explaining enterprise applications.

---

## Next Steps

Begin `service-boundaries.md` to define the responsibilities, ownership, and interactions of each microservice in EventHub.

---

# Learning Journal

**Date:** 22 July 2026

**Sprint:** Sprint 1 – Architecture & Design

## Objective

Understand how to define service boundaries in a microservices architecture by identifying business capabilities, assigning responsibilities, establishing data ownership, and documenting service interactions.

---

## Work Completed

Completed the `service-boundaries.md` architecture document for the EventHub project.

The document includes:

- Purpose of service boundaries
- Service Boundary Principles
- Infrastructure Services
  - API Gateway
- Business Services
  - Authentication Service
  - User Service
  - Event Service
  - Booking Service
  - Notification Service
- Service Responsibility Summary
- Database Ownership
- Service Communication Summary
- High-Level Communication Flow
- Guiding Principles
- Design Decisions
- Out of Scope
- Related Documents
- Version History

---

## Key Concepts Learned

- A microservice should own a single business capability.
- Every service should own and manage its own data.
- Services must never directly access another service's database.
- Communication between services should happen through REST APIs or asynchronous events.
- Infrastructure components such as API Gateway should remain separate from business services.
- Designing services around business domains improves scalability, maintainability, and independent deployment.

---

## Interview Notes

Today I strengthened my understanding of several commonly asked system design concepts:

- Defining service boundaries in a microservices architecture.
- Separating Authentication and User services based on responsibility.
- Understanding the Database per Service pattern.
- Choosing synchronous REST communication versus asynchronous event-driven messaging.
- Explaining why loose coupling and high cohesion are important in distributed systems.
- Identifying when an API Gateway acts as infrastructure rather than a business service.

These concepts are frequently discussed in backend engineering and system design interviews.

---

## Challenges

- Determining the appropriate responsibility for each service without creating overlap.
- Ensuring clear ownership of data while avoiding cross-service database access.
- Organizing the document so it flows logically from principles to implementation details.

---

## Key Takeaway

Effective service boundaries are based on business capabilities, not technical layers. Clear ownership of responsibilities and data leads to loosely coupled, independently deployable services that are easier to scale and maintain.

---

## Next Steps

- Begin documenting `communication-patterns.md`.
- Learn synchronous vs asynchronous communication in greater depth.
- Explore event-driven architecture using Apache Kafka.
- Study request-response patterns, event publishing, retries, idempotency, and fault tolerance in distributed systems.

---

# Learning Journal

**Date:** 22 July 2026

**Sprint:** Sprint 1 – Architecture & Design

## Objective

Understand communication patterns in a microservices architecture, including synchronous and asynchronous communication, event-driven architecture, reliability, and request traceability.

---

## Work Completed

Completed the `communication-patterns.md` architecture document for the EventHub project.

The document includes:

- Purpose
- Communication Principles
- Synchronous Communication
- Asynchronous Communication
- Communication Flow
- Reliability Considerations
- Correlation & Traceability
- Design Decisions
- Out of Scope
- Related Documents
- Version History

---

## Key Concepts Learned

- Differences between synchronous and asynchronous communication.
- Request-response communication using REST APIs.
- Event-driven architecture using Apache Kafka.
- Event publishing and event consumption.
- Communication flow between microservices.
- Reliability concepts such as idempotency, retries, timeouts, and Dead Letter Queues (DLQs).
- Correlation IDs for request tracing.
- Distributed tracing in microservices.

---

## Interview Questions & Short Answers

### Why use REST instead of Kafka for user login?

User login requires an immediate response. REST provides synchronous request-response communication, making it suitable for authentication workflows.

---

### Why use Kafka instead of REST for notifications?

Notifications are background tasks that do not require an immediate response. Kafka enables asynchronous processing, improves scalability, and reduces coupling between services.

---

### What is Event-Driven Architecture?

An architectural style where services communicate by publishing and consuming events instead of directly invoking one another.

---

### What is Idempotency?

Idempotency ensures that processing the same request or event multiple times produces the same result without creating duplicate business operations.

---

### What is a Dead Letter Queue (DLQ)?

A Dead Letter Queue stores messages that repeatedly fail processing after the configured retry attempts, allowing them to be inspected or replayed later.

---

### Why are Timeouts important?

Timeouts prevent services from waiting indefinitely for responses, improving system responsiveness and preventing resource exhaustion.

---

### What is a Correlation ID?

A Correlation ID is a unique identifier assigned to a request and propagated across services, enabling end-to-end request tracing and easier debugging.

---

### How do you trace a request across multiple microservices?

Generate a Correlation ID at the API Gateway and propagate it through HTTP headers, Kafka event metadata, and logs across all services.

---

## Challenges

- Understanding when to use synchronous versus asynchronous communication.
- Learning how Kafka supports event-driven workflows.
- Understanding reliability mechanisms such as retries, idempotency, and DLQs.
- Understanding how distributed tracing works using Correlation IDs.

---

## Key Takeaway

Choosing the right communication pattern is essential in microservices. REST is best for immediate request-response interactions, while Kafka enables scalable, resilient, and loosely coupled event-driven communication. Reliability and observability mechanisms ensure that distributed systems remain robust and maintainable.

---

## Next Steps

- Begin documenting `deployment-architecture.md`.
- Learn containerization using Docker.
- Understand Kubernetes architecture and service deployment.
- Explore service discovery, load balancing, and scaling strategies.

---

## Revision Notes

- REST → Immediate response
- Kafka → Background processing
- Idempotency → No duplicate operations
- DLQ → Failed messages after retries
- Correlation ID → Trace requests across services

---


