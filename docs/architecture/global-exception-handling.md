# Global Exception Handling Document

# 1. Purpose

The purpose of this document is to define a standardized exception handling strategy for the EventHub microservices platform.

Consistent exception handling improves API reliability, simplifies debugging, enhances security, and provides predictable error responses for API consumers.

This document establishes common standards for exception handling, error response structures, logging, HTTP status codes, correlation IDs, and application-specific error codes across all EventHub services.

---

# 2. Scope

This document applies to all EventHub microservices, including:

- Auth Service
- User Service
- Event Service
- Booking Service
- Payment Service
- Notification Service
- Search Service
- Analytics Service

It defines standards for:

- Exception hierarchy
- Global exception handling
- Validation errors
- Business exceptions
- Database exceptions
- Security exceptions
- External service failures
- Logging
- Error codes
- Standard error responses

All microservices shall follow these guidelines to ensure consistency across the platform.

---

# 3. Exception Handling Principles

Exception handling should provide meaningful information to API consumers while protecting internal implementation details.

The following principles shall be followed across all EventHub services.

## Fail Fast

Validate requests as early as possible and stop processing immediately when invalid input is detected.

---

## Centralized Exception Handling

All exceptions shall be processed using a centralized Global Exception Handler.

Business logic should not contain repetitive try-catch blocks for API response generation.

---

## Standardized Error Responses

All API errors shall return a consistent response structure regardless of the originating service.

---

## Meaningful Error Messages

Error messages should clearly describe the problem without exposing sensitive implementation details such as SQL queries, stack traces, or internal class names.

---

## Appropriate HTTP Status Codes

Exceptions shall be mapped to appropriate HTTP status codes based on the nature of the error.

---

## Structured Logging

All exceptions shall be logged using structured logging practices to support troubleshooting and monitoring.

---

## Correlation ID Propagation

Every error response shall include a Correlation ID to enable request tracing across distributed microservices.

---

## Security First

Internal implementation details shall never be exposed to API consumers.

Unexpected exceptions should return generic error messages while detailed information is recorded in application logs.

---

# 4. Exception Hierarchy

EventHub shall use a structured exception hierarchy to improve code readability, maintainability, and consistent error handling across all microservices.

Using specific exception types enables the application to return meaningful HTTP status codes, standardized error responses, and business-specific error codes.

---

## Exception Hierarchy

```
RuntimeException
│
├── BusinessException
│     ├── ResourceNotFoundException
│     ├── DuplicateResourceException
│     ├── InvalidOperationException
│     ├── PaymentFailedException
│     └── BookingClosedException
│
├── ValidationException
│
├── AuthenticationException
│
├── AuthorizationException
│
├── DatabaseException
│
├── ExternalServiceException
│
└── InternalServerException
```

---

## BusinessException

Represents business rule violations.

Examples:

- Booking a sold-out event
- Cancelling a completed payment
- Registering with an existing email

---

## ResourceNotFoundException

Thrown when the requested resource does not exist.

Examples:

- User not found
- Event not found
- Booking not found

Typical HTTP Status:

```
404 Not Found
```

---

## DuplicateResourceException

Thrown when attempting to create a resource that already exists.

Examples:

- Duplicate email
- Duplicate username
- Duplicate booking

Typical HTTP Status:

```
409 Conflict
```

---

## InvalidOperationException

Thrown when an operation violates business rules.

Examples:

- Booking after registration closes
- Updating a cancelled event
- Cancelling a completed booking

Typical HTTP Status:

```
400 Bad Request
```

---

## PaymentFailedException

Represents failures during payment processing.

Examples:

- Payment gateway declined
- Insufficient balance
- Payment timeout

Typical HTTP Status:

```
402 Payment Required
```

> Note: Some organizations prefer `400 Bad Request` or `503 Service Unavailable` depending on the payment provider and failure scenario.

---

## ValidationException

Thrown when request validation fails.

Examples:

- Missing required fields
- Invalid email format
- Negative seat count

Typical HTTP Status:

```
400 Bad Request
```

---

## AuthenticationException

Thrown when user authentication fails.

Examples:

- Invalid credentials
- Expired JWT
- Missing authentication token

Typical HTTP Status:

```
401 Unauthorized
```

---

## AuthorizationException

Thrown when an authenticated user lacks permission to perform an action.

Examples:

- Customer accessing admin APIs
- Organizer deleting another organizer's event

Typical HTTP Status:

```
403 Forbidden
```

---

## DatabaseException

Represents database-related failures.

Examples:

- Database unavailable
- Constraint violations
- Transaction failures

Typical HTTP Status:

```
500 Internal Server Error
```

---

## ExternalServiceException

Represents failures while communicating with external systems.

Examples:

- Payment gateway unavailable
- Email service timeout
- SMS provider failure

Typical HTTP Status:

```
503 Service Unavailable
```

---

## InternalServerException

Represents unexpected application failures.

Examples:

- NullPointerException
- Unexpected runtime failures
- Unknown application errors

Typical HTTP Status:

```
500 Internal Server Error
```

---

## Exception Design Guidelines

- Prefer specific exception classes over generic exceptions.
- Use meaningful exception names that describe the business problem.
- Do not expose internal implementation details in exception messages.
- Map exceptions consistently to HTTP status codes.
- Log detailed error information internally while returning safe messages to API consumers.

---

# 5. Standard Error Response

All EventHub microservices shall return a standardized error response structure whenever an exception occurs.

A consistent error response enables client applications to process errors predictably, improves debugging, and simplifies integration across the platform.

---

## Standard Error Response Structure

```json
{
  "success": false,
  "message": "User not found.",
  "errorCode": "USER_NOT_FOUND",
  "path": "/api/v1/users/123",
  "status": 404,
  "timestamp": "2026-07-25T14:30:15Z",
  "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Response Fields

| Field | Type | Description |
|--------|------|-------------|
| success | Boolean | Indicates whether the request was successful. Always `false` for error responses. |
| message | String | Human-readable description of the error. |
| errorCode | String | Application-specific error identifier. |
| timestamp | String | Time when the error occurred, represented in UTC using ISO-8601 format. |
| correlationId | String | Unique identifier used to trace the request across distributed microservices. |

---

## Field Guidelines

### success

- Shall always be `false`.

---

### message

- Should clearly describe the problem.
- Should be understandable by API consumers.
- Should not expose internal implementation details.

Good Example

```
Booking has already been cancelled.
```

Bad Example

```
NullPointerException at BookingService.java:78
```

---

### errorCode

Every application error shall have a unique error code.

Examples:

```
USER_NOT_FOUND

EVENT_NOT_FOUND

BOOKING_ALREADY_CANCELLED

PAYMENT_FAILED

INVALID_REQUEST

DATABASE_ERROR
```

Applications should rely on `errorCode` for programmatic handling rather than parsing the `message`.

---

### timestamp

The timestamp shall:

- use UTC
- follow ISO-8601 format

Example

```
2026-07-25T14:30:15Z
```

---

### correlationId

The correlation ID uniquely identifies a request flowing through multiple EventHub microservices.

This value enables:

- Distributed request tracing
- Centralized logging
- Faster troubleshooting
- Production monitoring

---

## Error Response Principles

- Return consistent error structures across all services.
- Never expose stack traces to API consumers.
- Never expose SQL queries or database details.
- Never expose internal class names.
- Return meaningful business messages.
- Use appropriate HTTP status codes.
- Include correlation IDs for every error response.

---

# 6. Global Exception Handler

EventHub shall use a centralized Global Exception Handler to process all application exceptions and return standardized error responses.

Spring Boot's `@RestControllerAdvice` shall be used to intercept exceptions thrown by controllers and convert them into consistent HTTP responses.

---

## Objectives

The Global Exception Handler shall:

- Centralize exception handling across all microservices.
- Return standardized error responses.
- Map exceptions to appropriate HTTP status codes.
- Prevent stack traces from being exposed to API consumers.
- Include Correlation IDs in every error response.
- Log exceptions consistently for monitoring and troubleshooting.

---

## Benefits

Using a centralized exception handler provides:

- Consistent API behavior
- Reduced duplicate code
- Easier maintenance
- Improved debugging
- Better client experience
- Improved production monitoring

---

## Request Flow

```
Client Request
       │
       ▼
Controller
       │
       ▼
Service
       │
       ▼
Repository
       │
       ▼
Exception Thrown
       │
       ▼
Global Exception Handler
       │
       ▼
Standard Error Response
       │
       ▼
Client
```

---

## Exception Handling Flow

1. A request reaches the Controller.
2. Business logic executes in the Service layer.
3. An exception is thrown.
4. Spring forwards the exception to the Global Exception Handler.
5. The handler logs the exception.
6. A standardized error response is created.
7. The appropriate HTTP status code is returned to the client.

---

## Design Guidelines

- Do not use repetitive try-catch blocks in controllers.
- Allow exceptions to propagate to the Global Exception Handler.
- Handle only exceptions that the application can process meaningfully.
- Unexpected exceptions shall return a generic Internal Server Error response.
- Business logic should focus on business rules, not HTTP response generation.
- Global exception handling shall remain independent of business logic. Services should throw meaningful exceptions, while the Global Exception Handler is responsible for converting those exceptions into standardized HTTP responses.

---

## Spring Boot Implementation

The Global Exception Handler shall be implemented using:

- `@RestControllerAdvice`
- `@ExceptionHandler`
- `ResponseEntity`

Implementation details will be provided during the coding phase of the project.

---

# 7. Custom Exceptions

EventHub shall define custom exception classes to represent specific business and technical error conditions.

Using custom exceptions improves code readability, enables standardized error handling, and allows the application to communicate meaningful failure reasons without exposing internal implementation details.

---

## Objectives

Custom exceptions shall:

- Represent specific business or technical errors.
- Improve code readability and maintainability.
- Support centralized exception handling.
- Enable standardized error responses.
- Map consistently to HTTP status codes.

---

## Exception Design Principles

Custom exceptions should:

- Represent a single error condition.
- Have meaningful and descriptive names.
- Extend the appropriate base exception.
- Avoid containing business logic.
- Include sufficient context for logging and troubleshooting.

---

## EventHub Exception Hierarchy

```
RuntimeException
        │
        ▼
EventHubException
        │
 ├── BusinessException
 │      ├── ResourceNotFoundException
 │      ├── DuplicateResourceException
 │      ├── InvalidOperationException
 │      ├── BookingClosedException
 │      └── PaymentFailedException
 │
 ├── ValidationException
 ├── AuthenticationException
 ├── AuthorizationException
 ├── DatabaseException
 ├── ExternalServiceException
 └── InternalServerException
```

---

## ResourceNotFoundException

Thrown when the requested resource does not exist.

Examples:

- User not found
- Event not found
- Booking not found

Typical HTTP Status:

```
404 Not Found
```

---

## DuplicateResourceException

Thrown when attempting to create a resource that already exists.

Examples:

- Duplicate email
- Duplicate username
- Duplicate booking

Typical HTTP Status:

```
409 Conflict
```

---

## InvalidOperationException

Thrown when an operation violates business rules.

Examples:

- Cancelling an already cancelled booking
- Updating a completed payment
- Booking after registration closes

Typical HTTP Status:

```
400 Bad Request
```

---

## BookingClosedException

Thrown when bookings are no longer accepted for an event.

Example:

```
Event registration has closed.
```

Typical HTTP Status:

```
400 Bad Request
```

---

## PaymentFailedException

Thrown when payment processing fails.

Examples:

- Payment declined
- Payment timeout
- Payment gateway failure

Typical HTTP Status:

```
402 Payment Required
```

> Note: Depending on the payment provider and failure scenario, some organizations may return `400 Bad Request` or `503 Service Unavailable`.

---

## ValidationException

Thrown when request validation fails.

Examples:

- Invalid email address
- Missing required fields
- Invalid UUID format

Typical HTTP Status:

```
400 Bad Request
```

---

## AuthenticationException

Thrown when user authentication fails.

Examples:

- Invalid credentials
- Expired JWT
- Missing authentication token

Typical HTTP Status:

```
401 Unauthorized
```

---

## AuthorizationException

Thrown when an authenticated user attempts an unauthorized operation.

Examples:

- Customer accessing admin APIs
- Organizer modifying another organizer's event

Typical HTTP Status:

```
403 Forbidden
```

---

## DatabaseException

Represents database-related failures.

Examples:

- Constraint violations
- Transaction failures
- Database unavailable

Typical HTTP Status:

```
500 Internal Server Error
```

---

## ExternalServiceException

Represents failures while communicating with external systems.

Examples:

- Payment gateway unavailable
- Email service unavailable
- SMS provider timeout

Typical HTTP Status:

```
503 Service Unavailable
```

---

## InternalServerException

Represents unexpected application failures.

Examples:

- Unexpected runtime errors
- NullPointerException
- Unknown system failures

Typical HTTP Status:

```
500 Internal Server Error
```

---

## Exception Naming Guidelines

- Exception names shall clearly describe the failure.
- All custom exceptions shall end with the suffix `Exception`.
- Business exceptions shall use business terminology.
- Generic exception names should be avoided.
- Exceptions shall not expose implementation details.

Examples:

```
ResourceNotFoundException
DuplicateResourceException
PaymentFailedException
BookingClosedException
ValidationException
```

---

# 8. Validation Exception Handling

Validation ensures that incoming requests meet the application's business and data integrity requirements before business logic is executed.

EventHub shall perform validation at the API boundary to reject invalid requests as early as possible.

---

## Objectives

Validation exception handling shall:

- Prevent invalid data from entering the application.
- Return consistent validation error responses.
- Improve API reliability.
- Provide meaningful feedback to API consumers.
- Reduce unnecessary processing.

---

## Validation Principles

Validation shall be performed:

- Before business logic execution.
- Using Jakarta Bean Validation annotations.
- At the Controller layer.
- Before database operations.
- Consistently across all microservices.

---

## Common Validation Annotations

Examples include:

- `@NotNull`
- `@NotBlank`
- `@Size`
- `@Email`
- `@Positive`
- `@Min`
- `@Max`
- `@Pattern`

---

## Validation Error Response

Validation failures shall return HTTP **400 Bad Request**.

Example:

```json
{
    "success": false,
    "message": "Validation failed.",
    "errorCode": "VALIDATION_ERROR",
    "status": 400,
    "path": "/api/v1/users",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a",
    "details": [
        {
            "field": "email",
            "message": "must be a valid email address"
        },
        {
            "field": "password",
            "message": "size must be between 8 and 20"
        }
    ]
}
```

---

## Validation Guidelines

- Validate all incoming request payloads.
- Return all validation errors in a single response where practical.
- Avoid exposing internal implementation details.
- Use clear, user-friendly validation messages.
- Maintain a consistent response structure across all services.

---

## Benefits

A standardized validation strategy provides:

- Better client experience
- Reduced debugging effort
- Improved data integrity
- Consistent API behavior
- Easier maintenance

---

# 9. Business Exception Handling

Business exceptions represent violations of application-specific business rules. Unlike validation exceptions, business exceptions occur after input validation has succeeded but the requested operation cannot be completed due to domain rules.

Business exceptions shall be represented using dedicated custom exception classes and handled centrally by the Global Exception Handler.

---

## Objectives

Business exception handling shall:

- Enforce business rules consistently.
- Return meaningful error messages.
- Prevent invalid business operations.
- Improve maintainability by separating business logic from error handling.
- Provide predictable responses to API consumers.

---

## Business Exception Principles

Business exceptions shall:

- Be thrown only after request validation succeeds.
- Represent business rule violations.
- Use meaningful exception names.
- Be mapped to appropriate HTTP status codes.
- Never expose internal implementation details.

---

## Common Business Exceptions

| Exception | Description | Typical HTTP Status |
|------------|-------------|---------------------|
| ResourceNotFoundException | Requested resource does not exist | 404 Not Found |
| DuplicateResourceException | Resource already exists | 409 Conflict |
| InvalidOperationException | Requested operation violates business rules | 400 Bad Request |
| BookingClosedException | Event registration is closed | 400 Bad Request |
| PaymentFailedException | Payment could not be processed | 402 Payment Required* |

> *Depending on organizational standards, payment failures may also return `400 Bad Request` or `503 Service Unavailable` when caused by an external provider.

---

## Business Rule Examples

### User Service

Examples:

- Email address already registered.
- Username already exists.
- User account is disabled.

---

### Event Service

Examples:

- Event has already started.
- Event registration has closed.
- Maximum participant limit reached.
- Organizer is not authorized to modify the event.

---

### Booking Service

Examples:

- Booking already cancelled.
- Seats are no longer available.
- Duplicate booking for the same event.
- Booking modification not allowed after confirmation.

---

### Payment Service

Examples:

- Payment already completed.
- Payment gateway rejected the transaction.
- Refund period has expired.

---

## Standard Business Error Response

```json
{
    "success": false,
    "message": "Event registration has closed.",
    "errorCode": "BOOKING_CLOSED",
    "status": 400,
    "path": "/api/v1/bookings",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Business Exception Guidelines

- Business services shall throw meaningful custom exceptions.
- Controllers shall not contain business-specific exception handling.
- The Global Exception Handler shall convert business exceptions into standardized HTTP responses.
- Business logic shall remain independent of HTTP response generation.
- Error messages shall be understandable by API consumers.

---

## Benefits

A standardized business exception strategy provides:

- Consistent enforcement of business rules.
- Cleaner service-layer implementation.
- Simplified debugging.
- Predictable API behavior.
- Improved maintainability.

---


# 10. Security Exception Handling

Security exceptions occur when authentication or authorization requirements are not satisfied.

EventHub shall use Spring Security to handle security-related exceptions and return standardized error responses consistent with the platform-wide API contract.

---

## Objectives

Security exception handling shall:

- Protect secured resources.
- Prevent unauthorized access.
- Return standardized security error responses.
- Avoid exposing sensitive security information.
- Maintain a consistent API experience across all microservices.

---

## Security Exception Types

EventHub shall distinguish between two primary security exception categories:

| Exception | Description | HTTP Status |
|------------|-------------|-------------|
| AuthenticationException | User identity cannot be verified. | 401 Unauthorized |
| AuthorizationException | User is authenticated but lacks sufficient permissions. | 403 Forbidden |

---

## Authentication Exceptions

Authentication exceptions occur when a request cannot be authenticated.

Common scenarios include:

- Missing JWT token
- Invalid JWT token
- Expired JWT token
- Invalid username or password
- Disabled user account
- Locked user account

Typical HTTP Status:

```
401 Unauthorized
```

Example Error Response:

```json
{
    "success": false,
    "message": "Authentication failed.",
    "errorCode": "INVALID_CREDENTIALS",
    "status": 401,
    "path": "/api/v1/auth/login",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Authorization Exceptions

Authorization exceptions occur when an authenticated user attempts an operation without the required permissions.

Examples:

- Customer accessing admin APIs
- Organizer editing another organizer's event
- User accessing restricted reports

Typical HTTP Status:

```
403 Forbidden
```

Example Error Response:

```json
{
    "success": false,
    "message": "Access denied.",
    "errorCode": "ACCESS_DENIED",
    "status": 403,
    "path": "/api/v1/admin/users",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Security Handling Guidelines

- Never expose internal security details.
- Do not reveal whether a username exists.
- Return generic authentication failure messages.
- Use standardized error codes.
- Log security events for auditing.
- Include correlation IDs in all security responses.

---

## Spring Security Integration

Security exceptions shall be handled using:

- AuthenticationEntryPoint
- AccessDeniedHandler
- Spring Security Filter Chain
- Global Exception Handler (where applicable)

Spring Security shall intercept authentication and authorization failures before requests reach application controllers.

---

## Benefits

A standardized security exception strategy provides:

- Improved application security
- Consistent client behavior
- Better auditability
- Easier monitoring
- Cleaner integration with Spring Security

---

# 11. Database Exception Handling

Database exceptions occur when the application encounters failures while interacting with the persistence layer.

EventHub shall handle database exceptions centrally to provide consistent error responses, preserve data integrity, and prevent exposure of sensitive database information.

---

## Objectives

Database exception handling shall:

- Maintain application stability.
- Protect database implementation details.
- Return standardized error responses.
- Preserve transactional integrity.
- Improve production troubleshooting.

---

## Database Exception Principles

Database exceptions shall:

- Be handled centrally by the Global Exception Handler.
- Never expose SQL statements or database schema.
- Be logged with sufficient diagnostic information.
- Return appropriate HTTP status codes.
- Preserve transactional consistency.

---

## Common Database Exceptions

| Exception | Description | Typical HTTP Status |
|------------|-------------|---------------------|
| DatabaseException | Generic database failure | 500 Internal Server Error |
| DataIntegrityViolationException | Constraint violation | 409 Conflict |
| DuplicateKeyException | Duplicate unique value | 409 Conflict |
| CannotAcquireLockException | Database lock timeout | 503 Service Unavailable |
| TransactionSystemException | Transaction failure | 500 Internal Server Error |

---

## Common Scenarios

### Duplicate Email

Attempting to create a user with an email address that already exists.

Result:

```
409 Conflict
```

---

### Foreign Key Violation

Attempting to create a booking for a non-existent event.

Result:

```
409 Conflict
```

---

### Database Connection Failure

Database server is unavailable.

Result:

```
500 Internal Server Error
```

or

```
503 Service Unavailable
```

depending on organizational standards.

---

### Transaction Rollback

A transaction fails because one or more operations cannot be completed successfully.

Result:

```
500 Internal Server Error
```

The entire transaction shall be rolled back to preserve data consistency.

---

## Standard Database Error Response

```json
{
    "success": false,
    "message": "A database error occurred.",
    "errorCode": "DATABASE_ERROR",
    "status": 500,
    "path": "/api/v1/bookings",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Database Exception Guidelines

- Never expose SQL queries.
- Never expose table names.
- Never expose column names.
- Never expose database vendor error messages.
- Convert low-level persistence exceptions into standardized application exceptions.
- Log complete diagnostic information internally while returning generic messages to clients.

---

## Transaction Management

Database operations shall use Spring's transaction management.

If an exception occurs within a transaction:

- The transaction shall be rolled back automatically.
- No partial updates shall be committed.
- Data consistency shall be preserved.

---

## Benefits

A standardized database exception strategy provides:

- Improved application reliability.
- Better data integrity.
- Consistent API responses.
- Enhanced security.
- Easier production support.

---

# 12. External Service Exception Handling

External service exceptions occur when EventHub communicates with third-party systems or other external infrastructure and those systems fail to respond successfully.

Examples include payment gateways, email providers, SMS services, cloud storage, external REST APIs, and other distributed services.

EventHub shall handle external service failures gracefully while maintaining application stability and providing standardized error responses.

---

## Objectives

External service exception handling shall:

- Prevent cascading failures.
- Improve application resilience.
- Return standardized error responses.
- Enable retry mechanisms where appropriate.
- Support production monitoring and troubleshooting.

---

## External Service Principles

External service exceptions shall:

- Be isolated from business logic.
- Never expose third-party implementation details.
- Be converted into standardized EventHub exceptions.
- Be logged with sufficient diagnostic information.
- Preserve application stability.

---

## Common External Service Exceptions

| Exception | Description | Typical HTTP Status |
|------------|-------------|---------------------|
| ExternalServiceException | Generic external service failure | 503 Service Unavailable |
| PaymentGatewayException | Payment provider unavailable | 503 Service Unavailable |
| EmailServiceException | Email delivery failed | 503 Service Unavailable |
| SmsServiceException | SMS delivery failed | 503 Service Unavailable |
| ExternalApiTimeoutException | External API timeout | 504 Gateway Timeout |

---

## Common Scenarios

### Payment Gateway Unavailable

The payment provider cannot process transactions.

Example:

```
Payment gateway is temporarily unavailable.
```

Result:

```
503 Service Unavailable
```

---

### Email Service Failure

Confirmation email cannot be sent.

Result:

```
503 Service Unavailable
```

---

### SMS Gateway Failure

OTP delivery fails.

Result:

```
503 Service Unavailable
```

---

### External API Timeout

The external service does not respond within the configured timeout period.

Result:

```
504 Gateway Timeout
```

---

## Standard External Service Error Response

```json
{
    "success": false,
    "message": "External service is temporarily unavailable.",
    "errorCode": "EXTERNAL_SERVICE_ERROR",
    "status": 503,
    "path": "/api/v1/payments",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Exception Handling Guidelines

- Do not expose third-party error messages.
- Do not expose API keys or secrets.
- Do not expose endpoint URLs.
- Convert vendor-specific exceptions into EventHub-specific exceptions.
- Log complete diagnostic information internally.

---

## Timeout Handling

All outbound requests shall define connection and read timeouts.

Applications shall fail fast when external services become unavailable.

Timeout values should be configurable through application configuration.

---

## Retry Strategy

Retries shall be performed only for transient failures.

Examples:

- Network timeout
- Temporary service outage
- HTTP 503 responses

Retries shall **not** be performed for:

- Authentication failures
- Authorization failures
- Validation errors
- Business rule violations

---

## Benefits

A standardized external service exception strategy provides:

- Better fault tolerance.
- Improved resilience.
- Consistent API behavior.
- Easier troubleshooting.
- Reduced impact of third-party failures.

---

# 13. Logging Strategy

Logging is a critical component of application observability. EventHub shall implement a standardized logging strategy to support monitoring, troubleshooting, auditing, and production incident analysis.

Logs shall provide sufficient operational information without exposing sensitive or confidential data.

---

## Objectives

The logging strategy shall:

- Capture meaningful application events.
- Support production troubleshooting.
- Enable distributed request tracing.
- Improve system monitoring.
- Facilitate auditing and compliance.
- Protect sensitive information.

---

## Logging Principles

Logging shall:

- Be consistent across all microservices.
- Use structured log messages.
- Include Correlation IDs.
- Avoid logging sensitive information.
- Differentiate log levels appropriately.
- Support centralized log aggregation.

---

## Log Levels

| Level | Purpose | Example |
|---------|---------|---------|
| TRACE | Detailed execution flow | Method entry/exit during debugging |
| DEBUG | Development diagnostics | SQL execution, variable values |
| INFO | Normal application events | User registered successfully |
| WARN | Unexpected but recoverable events | Retry attempt for email service |
| ERROR | Failures requiring investigation | Database connection failure |

---

## Information to Log

The following information should be included where applicable:

- Timestamp
- Log Level
- Correlation ID
- Service Name
- Request Path
- HTTP Method
- User Identifier (if available)
- Exception Type
- Error Code
- Execution Time

---

## Sensitive Information

The following information shall **never** be logged:

- Passwords
- JWT tokens
- Refresh tokens
- API keys
- Secret keys
- Credit card numbers
- CVV values
- Bank account details
- Personally identifiable information (PII) beyond operational necessity

---

## Example Log Entry

```
2026-07-25T14:30:15Z

INFO

Service=BookingService

CorrelationId=6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a

UserId=123e4567-e89b-12d3-a456-426614174000

Method=POST

Path=/api/v1/bookings

Message=Booking created successfully.
```

---

## Error Logging

Errors shall include:

- Exception type
- Error code
- Correlation ID
- Request path
- HTTP method
- Stack trace (internal logs only)

Stack traces shall never be returned to API consumers.

---

## Centralized Logging

Logs from all EventHub microservices should be aggregated into a centralized logging platform.

Examples include:

- ELK Stack (Elasticsearch, Logstash, Kibana)
- OpenSearch
- Grafana Loki
- Splunk

---

## Logging Guidelines

- Use INFO for normal business events.
- Use WARN for recoverable issues.
- Use ERROR for unexpected failures.
- Avoid excessive DEBUG logging in production.
- Ensure log messages are clear and meaningful.
- Use structured logging whenever possible.

---

## Benefits

A standardized logging strategy provides:

- Faster production troubleshooting.
- Improved observability.
- Better audit capabilities.
- Easier root cause analysis.
- Consistent operational practices across all microservices.

---

# 14. Correlation ID

A Correlation ID is a unique identifier assigned to every incoming request. It is propagated across all EventHub microservices to enable end-to-end request tracing.

Correlation IDs allow engineers to follow a single request through multiple services, making debugging, monitoring, and production incident analysis significantly easier.

---

## Objectives

Correlation IDs shall:

- Enable distributed request tracing.
- Simplify production debugging.
- Improve observability.
- Support centralized logging.
- Assist incident investigation.
- Correlate logs across multiple services.

---

## Correlation ID and Distributed Tracing

EventHub shall implement distributed tracing from the beginning using Micrometer Tracing and OpenTelemetry.

The application shall use two complementary identifiers:

- **Correlation ID** – A client-facing request identifier included in HTTP headers, API responses, and application logs to simplify request tracking and customer support.
- **Trace ID** – An internal distributed tracing identifier automatically generated by the tracing framework to track requests across multiple microservices.
- **Span ID** – A unique identifier representing an individual operation within a service, enabling detailed performance analysis.

The Correlation ID and Trace ID serve different purposes and shall coexist within the system.

All log entries should include the Correlation ID, Trace ID, and Span ID wherever available to provide complete end-to-end observability.

---

## Correlation ID Principles

Every incoming request shall have exactly one Correlation ID.

If the client supplies a Correlation ID, EventHub shall reuse it.

If the client does not supply one, the API Gateway shall generate a new UUID-based Correlation ID.

The same Correlation ID shall be propagated unchanged across all downstream services.

---

## Request Flow

```
                    X-Correlation-ID
Client  ─────────────────────────────────────► API Gateway

                          │
                          ▼
                 Generate / Continue Trace

                    Trace ID: abc123
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
  Auth Service      Booking Service   Payment Service
      │                  │                 │
  Span ID A          Span ID B        Span ID C
```

Every service receives exactly the same Correlation ID.

---

## HTTP Header

The Correlation ID shall be transmitted using the following HTTP header:

```
X-Correlation-ID
```

Example:

```
X-Correlation-ID:
6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a
```

---

## Correlation ID Generation

The API Gateway shall:

- Check whether the incoming request already contains a Correlation ID.
- Generate a UUID if none exists.
- Attach the Correlation ID to the request.
- Forward the same Correlation ID to downstream services.

---

## Correlation ID Propagation

Every microservice shall:

- Read the incoming Correlation ID.
- Store it for the duration of the request.
- Include it in all log entries.
- Include it in all outbound service calls.
- Return it in API responses.

The Correlation ID shall never change during request processing.

---

## Standard API Response

Every API response shall include:

```json
{
    "success": true,
    "message": "Booking created successfully.",
    "data": {},
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

Error responses shall also include the same Correlation ID.

---

## Logging Requirements

Every log entry shall include:

- Timestamp
- Service Name
- Log Level
- Correlation ID
- Request Path
- HTTP Method
- Error Code (if applicable)

---

## Benefits

Using Correlation IDs provides:

- End-to-end request tracing.
- Faster production troubleshooting.
- Improved observability.
- Easier root cause analysis.
- Better support for centralized logging platforms.

---

# 15. Error Codes

Error Codes provide a standardized, machine-readable identifier for application errors. Unlike error messages, which are intended for human understanding, error codes provide a stable contract between EventHub services and API consumers.

Every error response generated by EventHub shall include a unique error code.

---

## Objectives

Error codes shall:

- Standardize error identification.
- Simplify client-side error handling.
- Improve production troubleshooting.
- Support monitoring and analytics.
- Enable consistent logging across all microservices.
- Remain stable across application versions.

---

## Error Code Principles

Error codes shall:

- Be unique across the entire EventHub platform.
- Be descriptive and easy to understand.
- Be immutable once published.
- Be independent of HTTP status codes.
- Never expose implementation details.

---

## Error Code Naming Convention

Error codes shall:

- Use uppercase letters.
- Use words separated by underscores.
- Represent the business or technical failure.
- End users should never depend on the error message; they should rely on the error code.

Examples:

```
USER_NOT_FOUND
INVALID_CREDENTIALS
BOOKING_CLOSED
PAYMENT_FAILED
DATABASE_ERROR
EXTERNAL_SERVICE_ERROR
ACCESS_DENIED
VALIDATION_ERROR
```

---

## Error Code Categories

| Category | Prefix | Example |
|----------|--------|---------|
| Validation | VALIDATION | VALIDATION_ERROR |
| Authentication | AUTH | AUTH_INVALID_CREDENTIALS |
| Authorization | AUTHZ | AUTHZ_ACCESS_DENIED |
| User | USER | USER_NOT_FOUND |
| Event | EVENT | EVENT_CAPACITY_EXCEEDED |
| Booking | BOOKING | BOOKING_ALREADY_CANCELLED |
| Payment | PAYMENT | PAYMENT_FAILED |
| Notification | NOTIFICATION | NOTIFICATION_DELIVERY_FAILED |
| Database | DATABASE | DATABASE_ERROR |
| External Service | EXTERNAL | EXTERNAL_SERVICE_ERROR |
| Internal | INTERNAL | INTERNAL_SERVER_ERROR |

---

## Standard Error Response

```json
{
    "success": false,
    "message": "Event registration has closed.",
    "errorCode": "BOOKING_CLOSED",
    "status": 400,
    "path": "/api/v1/bookings",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Error Code Usage

Error codes shall be used consistently in:

- API responses
- Application logs
- Monitoring dashboards
- Alerting systems
- Audit records
- Client applications
- Automated testing

---

## ErrorCode Enumeration

The application shall maintain a centralized `ErrorCode` enumeration containing all supported error codes.

Example categories include:

### Validation

- VALIDATION_ERROR

### Authentication

- AUTH_INVALID_CREDENTIALS
- AUTH_TOKEN_EXPIRED
- AUTH_TOKEN_INVALID

### Authorization

- AUTHZ_ACCESS_DENIED

### User

- USER_NOT_FOUND
- USER_ALREADY_EXISTS
- USER_ACCOUNT_DISABLED

### Event

- EVENT_NOT_FOUND
- EVENT_CAPACITY_EXCEEDED
- EVENT_REGISTRATION_CLOSED

### Booking

- BOOKING_NOT_FOUND
- BOOKING_ALREADY_CANCELLED
- BOOKING_ALREADY_EXISTS

### Payment

- PAYMENT_FAILED
- PAYMENT_ALREADY_COMPLETED
- PAYMENT_REFUND_EXPIRED

### Notification

- NOTIFICATION_DELIVERY_FAILED

### Database

- DATABASE_ERROR
- DATABASE_CONSTRAINT_VIOLATION

### External Services

- EXTERNAL_SERVICE_ERROR
- EXTERNAL_SERVICE_TIMEOUT

### Internal

- INTERNAL_SERVER_ERROR

---

---

## Benefits

A centralized error code strategy provides:

- Stable API contracts.
- Easier frontend integration.
- Better production diagnostics.
- Consistent monitoring and alerting.
- Simplified maintenance across all microservices.

---

## Error Code Format

EventHub shall assign every published error a unique, immutable error code.

Format:

<DOMAIN>-<NUMBER>

Examples:

USER-001
BOOKING-001
PAYMENT-003
AUTH-002

The complete error code catalog shall be maintained in the EventHub Error Code Registry.

---

## Error Code Registry

The complete catalog of EventHub error codes shall be maintained in a dedicated **Error Code Registry** document.

The registry shall be created during the implementation phase and updated as each microservice is developed.

This document defines the governing standards, while the Error Code Registry serves as the authoritative reference for all published error codes.

---

# 16. HTTP Status Mapping

HTTP status codes communicate the outcome of an API request using standard HTTP semantics.

EventHub shall use HTTP status codes consistently across all microservices. Each status code shall accurately represent the result of the request, independent of the application's internal implementation.

---

## Objectives

HTTP status mapping shall:

- Provide predictable API behavior.
- Follow RESTful principles.
- Enable consistent client-side handling.
- Improve interoperability with external systems.
- Simplify monitoring and troubleshooting.

---

## HTTP Status Principles

HTTP status codes shall:

- Reflect the outcome of the request.
- Be consistent across all microservices.
- Not be used to convey business-specific details.
- Be accompanied by a standardized response body.
- Remain independent of application error codes.

---

## Success Status Codes

| HTTP Status | Meaning | Typical Usage |
|-------------|---------|---------------|
| 200 OK | Request completed successfully | Retrieve, update, delete operations |
| 201 Created | Resource created successfully | Create a new user, event, booking |
| 202 Accepted | Request accepted for asynchronous processing | Email, notification, background jobs |
| 204 No Content | Request successful with no response body | Delete operation with no payload |

---

## Client Error Status Codes

| HTTP Status | Meaning | Example |
|-------------|---------|---------|
| 400 Bad Request | Invalid request or business rule violation | Validation failed, registration closed |
| 401 Unauthorized | Authentication required or failed | Invalid or expired JWT |
| 403 Forbidden | Authenticated but insufficient permissions | Customer accessing admin API |
| 404 Not Found | Requested resource does not exist | User or event not found |
| 405 Method Not Allowed | HTTP method not supported | POST on a read-only endpoint |
| 409 Conflict | Resource conflict | Duplicate email, duplicate booking |
| 422 Unprocessable Entity | Semantically correct request but cannot be processed (optional) | Domain-specific validation if adopted |
| 429 Too Many Requests | Rate limit exceeded | Excessive API requests |

---

## Server Error Status Codes

| HTTP Status | Meaning | Example |
|-------------|---------|---------|
| 500 Internal Server Error | Unexpected application failure | Unhandled exception |
| 502 Bad Gateway | Invalid response from upstream service | API Gateway received invalid response |
| 503 Service Unavailable | Service temporarily unavailable | Payment gateway or database outage |
| 504 Gateway Timeout | Upstream service timeout | External API timeout |

---

## Exception-to-Status Mapping

| Exception | HTTP Status |
|-----------|-------------|
| ValidationException | 400 Bad Request |
| AuthenticationException | 401 Unauthorized |
| AuthorizationException | 403 Forbidden |
| ResourceNotFoundException | 404 Not Found |
| DuplicateResourceException | 409 Conflict |
| BookingClosedException | 400 Bad Request |
| PaymentFailedException | 503 Service Unavailable |
| DatabaseException | 500 Internal Server Error |
| ExternalServiceException | 503 Service Unavailable |
| InternalServerException | 500 Internal Server Error |

---

## Standard Success Response

```json
{
    "success": true,
    "message": "Booking created successfully.",
    "data": {},
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Standard Error Response

```json
{
    "success": false,
    "message": "Booking already exists.",
    "errorCode": "BOOKING_ALREADY_EXISTS",
    "status": 409,
    "path": "/api/v1/bookings",
    "timestamp": "2026-07-25T14:30:15Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

---

## Status Code Guidelines

- Use the most specific applicable HTTP status.
- Do not return `200 OK` for failed operations.
- Do not encode business failures solely through HTTP status codes.
- Pair every error response with an application-specific `errorCode`.
- Use standard HTTP semantics consistently across all APIs.

---

## Benefits

A standardized HTTP status mapping provides:

- Predictable API behavior.
- Easier frontend integration.
- Better interoperability with REST clients.
- Improved API consistency.
- Simplified debugging and monitoring.

---

## Relationship to Error Codes

HTTP status codes describe the outcome of the HTTP request.

Application-specific error codes provide detailed information about the failure.

The complete list of supported application error codes shall be maintained in the EventHub Error Code Registry.

---

# 17. Retry and Resilience Strategy

EventHub shall implement resilience patterns to improve reliability when communicating with external systems and distributed microservices.

Retries shall be applied only to transient failures where a subsequent attempt has a reasonable chance of succeeding.

The application shall avoid retries for permanent failures such as validation errors, authentication failures, or business rule violations.

---

## Objectives

The retry and resilience strategy shall:

- Improve system reliability.
- Reduce the impact of transient failures.
- Prevent cascading failures.
- Protect external dependencies.
- Improve overall application availability.

---

## Resilience Principles

EventHub shall:

- Retry only transient failures.
- Fail fast for permanent failures.
- Apply configurable retry policies.
- Use circuit breakers for unstable dependencies.
- Configure request timeouts.
- Log all retry attempts.
- Avoid infinite retry loops.

---

## Retryable Scenarios

The following failures may be retried:

| Scenario | Retry |
|----------|--------|
| Network timeout | Yes |
| Temporary database connection issue | Yes |
| External API timeout | Yes |
| HTTP 503 Service Unavailable | Yes |
| HTTP 504 Gateway Timeout | Yes |
| Temporary Kafka broker unavailable | Yes |

---

## Non-Retryable Scenarios

The following failures shall not be retried:

| Scenario | Retry |
|----------|--------|
| Validation failure | No |
| Invalid credentials | No |
| Access denied | No |
| Duplicate resource | No |
| Business rule violation | No |
| Resource not found | No |

---

## Retry Policy

The default retry policy shall:

- Maximum attempts: **3**
- Initial delay: **500 ms**
- Exponential backoff enabled
- Configurable through application configuration

Example:

Attempt 1 → Immediate

Attempt 2 → 500 ms

Attempt 3 → 1000 ms

---

## Timeout Policy

Every outbound service call shall define:

- Connection timeout
- Read timeout

Applications shall fail fast when configured timeout limits are exceeded.

---

## Circuit Breaker

Circuit breakers shall be used for unstable external services.

States:

- Closed – Normal operation.
- Open – Requests fail immediately.
- Half-Open – Limited requests allowed to test recovery.

This prevents repeated requests to unavailable services and protects system resources.

---

## Bulkhead Isolation

Critical components shall be isolated using dedicated thread pools or resource limits.

Bulkheads prevent failures in one dependency from impacting unrelated parts of the application.

---

## Fallback Strategy

Where appropriate, fallback responses may be provided.

Examples:

- Cached event information.
- Temporary service unavailable response.
- Queue request for later processing.

Fallback behavior shall not compromise data consistency.

---

## Logging Requirements

Retry operations shall log:

- Correlation ID
- Trace ID (if available)
- Retry attempt number
- Exception type
- Target service
- Execution time

---

## Monitoring

The following metrics should be monitored:

- Retry count
- Retry success rate
- Retry failure rate
- Circuit breaker state
- Timeout count
- External dependency availability

---

## Benefits

A standardized retry and resilience strategy provides:

- Higher availability.
- Better fault tolerance.
- Reduced cascading failures.
- Improved user experience.
- Greater operational visibility.

---

# 17. Retry and Resilience Strategy

EventHub shall implement resilience patterns to improve reliability when communicating with external systems and distributed microservices.

Retries shall be applied only to transient failures where a subsequent attempt has a reasonable chance of succeeding.

The application shall avoid retries for permanent failures such as validation errors, authentication failures, or business rule violations.

---

## Objectives

The retry and resilience strategy shall:

- Improve system reliability.
- Reduce the impact of transient failures.
- Prevent cascading failures.
- Protect external dependencies.
- Improve overall application availability.

---

## Resilience Principles

EventHub shall:

- Retry only transient failures.
- Fail fast for permanent failures.
- Apply configurable retry policies.
- Use circuit breakers for unstable dependencies.
- Configure request timeouts.
- Log all retry attempts.
- Avoid infinite retry loops.

---

## Retryable Scenarios

The following failures may be retried:

| Scenario | Retry |
|----------|--------|
| Network timeout | Yes |
| Temporary database connection issue | Yes |
| External API timeout | Yes |
| HTTP 503 Service Unavailable | Yes |
| HTTP 504 Gateway Timeout | Yes |
| Temporary Kafka broker unavailable | Yes |

---

## Non-Retryable Scenarios

The following failures shall not be retried:

| Scenario | Retry |
|----------|--------|
| Validation failure | No |
| Invalid credentials | No |
| Access denied | No |
| Duplicate resource | No |
| Business rule violation | No |
| Resource not found | No |

---

## Retry Policy

The default retry policy shall:

- Maximum attempts: **3**
- Initial delay: **500 ms**
- Exponential backoff enabled
- Configurable through application configuration

Example:

Attempt 1 → Immediate

Attempt 2 → 500 ms

Attempt 3 → 1000 ms

---

## Timeout Policy

Every outbound service call shall define:

- Connection timeout
- Read timeout

Applications shall fail fast when configured timeout limits are exceeded.

---

## Circuit Breaker

Circuit breakers shall be used for unstable external services.

States:

- Closed – Normal operation.
- Open – Requests fail immediately.
- Half-Open – Limited requests allowed to test recovery.

This prevents repeated requests to unavailable services and protects system resources.

---

## Bulkhead Isolation

Critical components shall be isolated using dedicated thread pools or resource limits.

Bulkheads prevent failures in one dependency from impacting unrelated parts of the application.

---

## Fallback Strategy

Where appropriate, fallback responses may be provided.

Examples:

- Cached event information.
- Temporary service unavailable response.
- Queue request for later processing.

Fallback behavior shall not compromise data consistency.

---

## Logging Requirements

Retry operations shall log:

- Correlation ID
- Trace ID (if available)
- Retry attempt number
- Exception type
- Target service
- Execution time

---

## Monitoring

The following metrics should be monitored:

- Retry count
- Retry success rate
- Retry failure rate
- Circuit breaker state
- Timeout count
- External dependency availability

---

## Benefits

A standardized retry and resilience strategy provides:

- Higher availability.
- Better fault tolerance.
- Reduced cascading failures.
- Improved user experience.
- Greater operational visibility.

---

## Enterprise Resilience Standards

EventHub shall standardize on the following resilience technologies:

- Resilience4j for retry, circuit breaker, bulkhead, and time limiter patterns.
- Micrometer for application metrics.
- OpenTelemetry for distributed tracing.
- Prometheus for metrics collection.
- Grafana for monitoring dashboards.
- Structured JSON logging for centralized log analysis.

These standards shall be consistently applied across all EventHub microservices.

---

# 18. Architecture Decisions Summary

The following architectural decisions have been adopted for EventHub's Global Exception Handling strategy.

| Decision ID | Decision |
|-------------|----------|
| AD-001 | Standardized API Response Format |
| AD-002 | Centralized Global Exception Handling using `@RestControllerAdvice` |
| AD-003 | Custom Exception Hierarchy |
| AD-004 | Standardized Error Code Strategy |
| AD-005 | Correlation ID with Distributed Tracing |
| AD-006 | Structured JSON Logging |
| AD-007 | Retry and Resilience using Resilience4j |
| AD-008 | Standard HTTP Status Mapping |
| AD-009 | Centralized Error Code Registry |
| AD-010 | Security-First Error Responses |

These decisions establish a consistent and scalable exception handling strategy across all EventHub microservices.

The detailed rationale, context, alternatives considered, and consequences for each decision shall be documented separately as individual Architecture Decision Records (ADRs) under the project's `docs/adr` directory.

---

# 19. References

The following references were used in defining the EventHub Global Exception Handling standards.

## Java

- Java Platform, Standard Edition 21 Documentation

## Spring Framework

- Spring Boot Reference Documentation
- Spring Framework Reference Documentation
- Spring Security Reference Documentation
- Spring Data JPA Documentation

## Jakarta

- Jakarta Bean Validation Specification

## HTTP Standards

- RFC 9110 – HTTP Semantics
- RFC 9457 – Problem Details for HTTP APIs (Reference Model)

## Observability

- OpenTelemetry Specification
- Micrometer Documentation

## Resilience

- Resilience4j Documentation

## Security

- OWASP API Security Top 10
- OWASP Logging Cheat Sheet

## Logging

- SLF4J Documentation
- Logback Documentation

## Enterprise Architecture

- Martin Fowler – Patterns of Enterprise Application Architecture
- Microsoft REST API Guidelines

---

# 20. Version History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | July 2026 | EventHub Architecture Team | Initial Global Exception Handling Architecture |
| Future | TBD | EventHub Architecture Team | Updates based on implementation and architectural evolution |

