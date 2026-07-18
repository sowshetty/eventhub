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
