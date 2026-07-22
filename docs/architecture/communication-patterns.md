# Purpose

This document describes the communication patterns used by the EventHub platform.

It explains how services exchange information using synchronous REST APIs and asynchronous event-driven messaging while maintaining loose coupling, scalability, and resilience.

The document also outlines the principles and design decisions that govern communication between microservices.

---

# Communication Principles

Communication between services follows these principles:

- Services communicate through well-defined APIs or events.
- Direct database access between services is prohibited.
- Synchronous communication is used only when an immediate response is required.
- Asynchronous communication is preferred for long-running or non-blocking workflows.
- Services remain loosely coupled and independently deployable.
- Communication mechanisms should support scalability, reliability, and fault tolerance.

---

# Synchronous Communication

Synchronous communication is used when a service requires an immediate response from another service before continuing its execution.

In EventHub, synchronous communication is implemented using REST APIs for request-response interactions.

## REST APIs

REST APIs enable services to communicate over HTTP using well-defined endpoints.

Typical REST operations include:

- User authentication
- User profile management
- Event retrieval
- Ticket booking requests

REST communication is appropriate for operations where the client expects an immediate result.

---

## Request-Response Pattern

In the request-response pattern, a client sends a request to a service and waits until a response is received.

Example flow:

Client
→ API Gateway
→ Booking Service
→ Response returned to Client

This pattern is simple, predictable, and well suited for user-facing operations that require immediate feedback.

---

## Typical Use Cases

EventHub uses synchronous communication for:

- User login
- User registration
- Fetching user profiles
- Retrieving event information
- Creating booking requests
- Viewing booking history

## When Not to Use Synchronous Communication

Synchronous communication should be avoided for long-running or non-critical background tasks.

Examples include:

- Sending email notifications
- Processing analytics
- Generating reports
- Publishing audit events

These operations are better suited for asynchronous communication to avoid blocking client requests and to improve overall system responsiveness.

---

# Asynchronous Communication

Asynchronous communication enables services to exchange information without requiring an immediate response.

Instead of waiting for another service to complete its work, a service publishes an event and continues processing. Other interested services consume the event independently.

EventHub uses Apache Kafka as its event streaming platform to support asynchronous communication between services.

---

## Event-Driven Architecture

In an event-driven architecture, services communicate by publishing and consuming events.

An event represents something significant that has occurred within the system.

Examples include:

- EventCreated
- EventUpdated
- EventDeleted
- BookingCreated
- BookingCancelled

Services that are interested in these events subscribe to them and perform their respective tasks independently.

This approach reduces direct dependencies between services and improves scalability and resilience.

---

## Apache Kafka

Apache Kafka acts as the messaging backbone for asynchronous communication within EventHub.

Instead of one service directly calling another, events are published to Kafka topics, allowing multiple services to consume the same event independently.

Kafka provides:

- High throughput
- Fault tolerance
- Durable message storage
- Scalable event processing
- Loose coupling between services

---

## Event Publishing and Consumption

The typical communication flow is:

1. A service performs a business operation.
2. The service publishes an event to Kafka.
3. Kafka stores the event in the appropriate topic.
4. Interested services consume the event.
5. Each consumer processes the event independently.

This pattern enables multiple services to react to the same event without introducing tight coupling.

## Event Processing Flow

```text
               Booking Service
                      │
                      ▼
          Publish BookingCreated Event
                      │
                      ▼
                  Kafka Topic
            ┌─────────┴─────────┐
            ▼                   ▼
 Notification Service     Analytics Service
            │                   │
      Send Confirmation    Update Metrics
```

---

## Why Kafka?

Apache Kafka is used because it enables services to communicate asynchronously without creating direct dependencies.

Compared to synchronous REST communication, Kafka offers several advantages for background processing:

- Producers and consumers remain loosely coupled.
- Multiple services can consume the same event independently.
- Temporary consumer failures do not affect event publication.
- High event throughput supports scalable distributed systems.
- Events can be retained for replay and auditing if required.

Kafka is therefore well suited for notifications, analytics, auditing, and other background workflows that do not require an immediate client response.

---

# Communication Flow

EventHub uses both synchronous REST APIs and asynchronous event-driven messaging depending on the business requirement.

The following diagram illustrates a typical communication flow during the ticket booking process.

```text
                         Client
                            │
                            ▼
                      API Gateway
                            │
                            ▼
                    Booking Service
                            │
                Validate Booking Request
                            │
                            ▼
                     Store Booking Data
                            │
                            ▼
               Publish BookingCreated Event
                            │
                            ▼
                         Kafka Topic
                  ┌─────────┴─────────┐
                  ▼                   ▼
       Notification Service   Analytics Service
                  │                   │
          Send Confirmation    Update Metrics
```

The booking request is completed synchronously so that the user receives an immediate response. Background operations such as notifications and analytics are processed asynchronously through Kafka, improving responsiveness and reducing coupling between services.

---

# Reliability Considerations

Reliable communication is essential in distributed systems to ensure that failures do not result in lost data or inconsistent system behavior.

---

## Idempotency

Idempotency ensures that processing the same request or event multiple times produces the same outcome.

For example, if a `BookingCreated` event is delivered more than once, the Booking Service should prevent duplicate bookings by recognizing that the booking has already been processed.

---

## Retry Strategy

Temporary failures such as network interruptions or third-party service outages should be handled using controlled retry mechanisms.

Retries should:

- Be limited to a configurable number of attempts.
- Use exponential backoff where appropriate.
- Avoid creating duplicate operations.

---

## Timeouts

Synchronous service calls should always define appropriate timeout values.

Timeouts prevent services from waiting indefinitely for responses, allowing failures to be detected quickly and improving overall system responsiveness.

---

## Dead Letter Queue (Future Enhancement)

If an event cannot be processed successfully after the configured retry attempts, it may be redirected to a Dead Letter Queue (DLQ).

A DLQ preserves failed events for later inspection, replay, or manual intervention, preventing problematic messages from blocking normal event processing.

---

# Correlation & Traceability

In a distributed system, a single client request may pass through multiple services before completing.

To enable end-to-end request tracking, EventHub uses a Correlation ID that is generated when a request first enters the system through the API Gateway.

The Correlation ID is propagated across all downstream service calls and event messages, allowing related logs and traces to be associated with the same request.

---

## Correlation ID

A Correlation ID is a unique identifier assigned to a request.

Example:

```
Correlation ID: 4f8d2b7a-91d2-4a6f-b8d1-53f4d19c2d7e
```

Every service includes this identifier in:

- HTTP request headers
- Kafka event metadata
- Application logs

This enables developers to trace the complete lifecycle of a request across multiple services.

---

## Distributed Tracing

Distributed tracing provides visibility into how a request travels through different services.

For example:

```text
Client
   │
   ▼
API Gateway
   │
   ▼
Booking Service
   │
   ▼
Kafka
   │
   ▼
Notification Service
```

By using the same Correlation ID throughout this flow, engineers can quickly identify where failures, delays, or unexpected behavior occur.

---

## Benefits

Using Correlation IDs and distributed tracing provides several benefits:

- Faster troubleshooting
- Easier root cause analysis
- Improved observability
- Better monitoring of distributed requests
- Simplified production debugging

---

## Request Trace Example

```text
Client
  │
  │ Correlation ID: ABC123
  ▼
API Gateway
  │
  │ ABC123
  ▼
Booking Service
  │
  │ Publish BookingCreated (ABC123)
  ▼
Kafka
  │
  │ ABC123
  ▼
Notification Service

All logs generated during this request contain:
Correlation ID = ABC123
```

---

# Design Decisions

The communication patterns in EventHub are designed to balance responsiveness, scalability, and reliability.

The following architectural decisions guide service communication:

- REST APIs are used for synchronous request-response interactions that require an immediate response.
- Apache Kafka is used for asynchronous communication between services for non-blocking background processing.
- Services communicate through APIs or events rather than accessing another service's database directly.
- Event-driven communication is preferred for workflows involving multiple independent consumers.
- Communication mechanisms are selected based on business requirements rather than technology preferences.
- Reliability is improved through idempotency, retry strategies, and timeout handling.
- Correlation IDs enable end-to-end request tracing across distributed services.

These decisions promote loose coupling, fault tolerance, independent scalability, and maintainability across the platform.

---


# Out of Scope

This document does not cover:

- REST API specifications
- Kafka topic configuration
- Event schema definitions
- Message serialization formats
- Authentication and authorization
- Deployment configuration
- Monitoring and observability implementation
- Infrastructure provisioning

These topics are documented separately in their respective architecture documents.

---

# Related Documents

The following documents provide additional architectural context for the EventHub platform:

- [System Overview](system-overview.md)
- [Technology Stack](technology-stack.md)
- [Service Boundaries](service-boundaries.md)
- Deployment Architecture *(to be added)*
- Security Architecture *(to be added)*
- Observability *(to be added)*
- Architecture Principles *(to be added)*

---

# Version History

| Version | Date | Author | Description |
|----------|------|---------|-------------|
| 1.0 | 2026-07-22 | Sowmyaa Shetty | Initial version of the Communication Patterns architecture document. |