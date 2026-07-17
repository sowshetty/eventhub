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

Sprint 0 – Day 2 In Progress ✅