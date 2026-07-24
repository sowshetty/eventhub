# API Design guidelines 

---

# 1. Purpose

The purpose of this document is to define the API design standards and best practices for all REST APIs exposed by the EventHub microservices platform.

These guidelines establish a consistent approach to designing, implementing, documenting, and maintaining APIs across the system. Following these standards ensures that APIs are predictable, secure, scalable, maintainable, and easy for both developers and consumers to use.

This document serves as the primary reference for API development throughout the EventHub project.

---

# 2. Scope

These guidelines apply to all REST APIs developed as part of the EventHub platform, including current and future microservices.

This document defines standards for:

- REST API design
- Resource naming conventions
- HTTP methods
- Request and response structures
- HTTP status codes
- Error handling
- Pagination, sorting, and filtering
- Input validation
- API versioning
- Security considerations
- API documentation using OpenAPI/Swagger

The standards described in this document are mandatory for all EventHub services to ensure consistency and interoperability across the platform.

---

# 3. REST Design Principles

The EventHub platform follows REST (Representational State Transfer) principles for designing web APIs. REST provides a simple, scalable, and widely adopted architectural style for communication between clients and microservices.

The following principles shall be followed throughout the platform:

- Design APIs around business resources rather than actions.
- Use standard HTTP methods appropriately.
- Maintain stateless communication between clients and services.
- Exchange data using JSON.
- Use meaningful and consistent URI naming conventions.
- Return appropriate HTTP status codes.
- Provide consistent request and response structures.
- Design APIs to be backward compatible whenever possible.
- Version APIs explicitly.
- Secure all APIs using HTTPS and JWT-based authentication.
- Document every public API using OpenAPI (Swagger).
- Validate all client input before processing requests.
- Avoid exposing internal implementation details through API responses.

---

# 4. API Naming Standards 

Consistent naming conventions improve code readability, maintainability, and collaboration across development teams. All EventHub APIs shall follow the naming standards defined in this section.

## General Guidelines

- Use meaningful and descriptive names.
- Avoid abbreviations unless they are industry-standard.
- Maintain consistency across all microservices.
- Follow standard Java naming conventions for classes and methods.
- Use camelCase for JSON properties.
- Use PascalCase for Java class names.

---

## Controller Naming

Controllers shall represent business resources.

Examples:

```
AuthController
UserController
EventController
BookingController
PaymentController
NotificationController
SearchController
AnalyticsController
```

---

## Service Naming

Business services shall use the **Service** suffix.

Examples:

```
AuthService
UserService
EventService
BookingService
PaymentService
SearchService
AnalyticsService
```

Implementation classes shall use the **Impl** suffix.

Examples:

```
AuthServiceImpl
EventServiceImpl
BookingServiceImpl
```

---

## Repository Naming

Repositories shall represent data access components.

Examples:

```
UserRepository
EventRepository
BookingRepository
PaymentRepository
```

---

## Request DTO Naming

Request objects shall use descriptive names ending with **Request**.

Examples:

```
CreateUserRequest
UpdateUserRequest
LoginRequest
RegisterRequest
CreateEventRequest
UpdateEventRequest
```

---

## Response DTO Naming

Response objects shall use descriptive names ending with **Response**.

Examples:

```
UserResponse
EventResponse
BookingResponse
LoginResponse
AuthenticationResponse
```

---

## Exception Naming

Custom exceptions shall end with **Exception**.

Examples:

```
ResourceNotFoundException
DuplicateResourceException
UnauthorizedException
ValidationException
PaymentFailedException
BusinessException
```

---

## Enum Naming

Enumeration types shall use singular nouns.

Examples:

```
UserRole
BookingStatus
PaymentStatus
EventCategory
NotificationType
```

Enum values shall use uppercase letters.

Examples:

```
ACTIVE
INACTIVE
PENDING
CONFIRMED
CANCELLED
SUCCESS
FAILED
```

---

## Package Naming

Package names shall use lowercase letters.

Example:

```
com.eventhub.auth.controller
com.eventhub.auth.service
com.eventhub.auth.repository
com.eventhub.auth.dto
com.eventhub.auth.entity
com.eventhub.auth.exception
```

---

## JSON Property Naming

JSON request and response properties shall use camelCase.

Example:

```json
{
    "eventTitle": "Spring Boot Workshop",
    "eventDate": "2026-08-15",
    "totalSeats": 200
}
```

---

## URI Naming

REST resource names shall use plural nouns.

Examples:

```
/api/v1/events
/api/v1/bookings
/api/v1/users
```

---

## Query Parameter Naming

Query parameters shall use camelCase.

Examples:

```
?page=0
&size=20
&sort=createdAt,desc
&eventCategory=Technology
```

---

## HTTP Header Naming

HTTP headers shall follow standard naming conventions.

### Standard Headers

| Header | Purpose |
|---------|----------|
| Authorization | Carries the JWT access token for authenticated requests |
| Content-Type | Specifies the format of the request body |
| Accept | Specifies the expected response format |
| X-Correlation-ID | Uniquely identifies a request across distributed microservices |

### Example

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...

Content-Type: application/json

Accept: application/json

X-Correlation-ID: 6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a
```

### Header Guidelines

- Use standard HTTP header names whenever possible.
- Protected APIs shall require the `Authorization` header.
- JSON APIs shall use `Content-Type: application/json`.
- Clients shall specify the expected response format using the `Accept` header.
- The `X-Correlation-ID` header shall be propagated across all microservices to enable distributed request tracing.

---

## Naming Principles

- Use singular names for Java classes.
- Use plural names for REST resources.
- Use meaningful business terminology.
- Avoid technology-specific names in public APIs.
- Follow consistent naming conventions across all EventHub microservices.

---

## Controller Naming

Controllers shall represent business resources.

Examples:

```
AuthController
UserController
EventController
BookingController
PaymentController
NotificationController
SearchController
AnalyticsController
```

---

## Service Naming

Business services shall use the **Service** suffix.

Examples:

```
AuthService
UserService
EventService
BookingService
PaymentService
SearchService
AnalyticsService
```

Implementation classes shall use the **Impl** suffix.

Examples:

```
AuthServiceImpl
EventServiceImpl
BookingServiceImpl
```

---

## Repository Naming

Repositories shall represent data access components.

Examples:

```
UserRepository
EventRepository
BookingRepository
PaymentRepository
```

---

## Request DTO Naming

Request objects shall use descriptive names ending with **Request**.

Examples:

```
CreateUserRequest
UpdateUserRequest
LoginRequest
RegisterRequest
CreateEventRequest
UpdateEventRequest
```

---

## Response DTO Naming

Response objects shall use descriptive names ending with **Response**.

Examples:

```
UserResponse
EventResponse
BookingResponse
LoginResponse
AuthenticationResponse
```

---

## Exception Naming

Custom exceptions shall end with **Exception**.

Examples:

```
ResourceNotFoundException
DuplicateResourceException
UnauthorizedException
ValidationException
PaymentFailedException
BusinessException
```

---

## Enum Naming

Enumeration types shall use singular nouns.

Examples:

```
UserRole
BookingStatus
PaymentStatus
EventCategory
NotificationType
```

Enum values shall use uppercase letters.

Examples:

```
ACTIVE
INACTIVE
PENDING
CONFIRMED
CANCELLED
SUCCESS
FAILED
```

---

## Package Naming

Package names shall use lowercase letters.

Example:

```
com.eventhub.auth.controller
com.eventhub.auth.service
com.eventhub.auth.repository
com.eventhub.auth.dto
com.eventhub.auth.entity
com.eventhub.auth.exception
```

---

## JSON Property Naming

JSON request and response properties shall use camelCase.

Example:

```json
{
    "eventTitle": "Spring Boot Workshop",
    "eventDate": "2026-08-15",
    "totalSeats": 200
}
```

---

## URI Naming

REST resource names shall use plural nouns.

Examples:

```
/api/v1/events
/api/v1/bookings
/api/v1/users
```

---

## Query Parameter Naming

Query parameters shall use camelCase.

Examples:

```
?page=0
&size=20
&sort=createdAt,desc
&eventCategory=Technology
```

---

## HTTP Header Naming

HTTP headers shall follow standard naming conventions.

### Standard Headers

| Header | Purpose |
|---------|----------|
| Authorization | Carries the JWT access token for authenticated requests |
| Content-Type | Specifies the format of the request body |
| Accept | Specifies the expected response format |
| X-Correlation-ID | Uniquely identifies a request across distributed microservices |

### Example

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...

Content-Type: application/json

Accept: application/json

X-Correlation-ID: 6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a
```

### Header Guidelines

- Use standard HTTP header names whenever possible.
- Protected APIs shall require the `Authorization` header.
- JSON APIs shall use `Content-Type: application/json`.
- Clients shall specify the expected response format using the `Accept` header.
- The `X-Correlation-ID` header shall be propagated across all microservices to enable distributed request tracing.

---

## Naming Principles

- Use singular names for Java classes.
- Use plural names for REST resources.
- Use meaningful business terminology.
- Avoid technology-specific names in public APIs.
- Follow consistent naming conventions across all EventHub microservices.

---

# 5. HTTP Methods

EventHub APIs shall use standard HTTP methods in accordance with REST architectural principles. Each method shall be used consistently to represent its intended operation on a resource.

## Supported HTTP Methods
| HTTP Method | Purpose                               | Request Body |
| ----------- | ------------------------------------- | ------------ |
| GET         | Retrieve one or more resources        | No           |
| POST        | Create a new resource                 | Yes          |
| PUT         | Replace an existing resource          | Yes          |
| PATCH       | Partially update an existing resource | Yes          |
| DELETE      | Remove a resource                     | No           |


> *PATCH is generally not guaranteed to be idempotent. If implemented, its behavior should be carefully designed to ensure predictable updates where appropriate.

---

## Method Usage Guidelines

### GET

Use GET to retrieve resources without modifying server-side data.

Examples:

```
GET /api/v1/events

GET /api/v1/events/{eventId}

GET /api/v1/users/{userId}
```

---

### POST

Use POST to create new resources.

Examples:

```
POST /api/v1/events

POST /api/v1/bookings

POST /api/v1/auth/login
```

A successful POST request shall typically return:

- HTTP 201 (Created)
- Location header (where applicable)
- Newly created resource or resource identifier

---

### PUT

Use PUT to completely replace an existing resource.

Examples:

```
PUT /api/v1/events/{eventId}

PUT /api/v1/users/{userId}
```

PUT requests should include the complete representation of the resource.

---

### PATCH

Use PATCH to partially update an existing resource.

Examples:

```
PATCH /api/v1/users/{userId}

PATCH /api/v1/events/{eventId}
```

PATCH requests should update only the specified fields without affecting the remaining resource data.

---

### DELETE

Use DELETE to remove a resource.

Examples:

```
DELETE /api/v1/events/{eventId}

DELETE /api/v1/bookings/{bookingId}
```

Repeated DELETE requests should not cause unintended side effects.

---

## HTTP Method Best Practices

- Use the appropriate HTTP method for the intended operation.
- Do not use GET for operations that modify data.
- Avoid using POST for update operations when PUT or PATCH is more appropriate.
- Use PUT for complete replacements and PATCH for partial updates.
- Return appropriate HTTP status codes for every operation.
- Keep API behavior consistent across all EventHub microservices.

---

# 6. Request Design

All API requests shall follow a consistent structure to improve readability, maintainability, and interoperability across the EventHub platform.

## Request Body

- Request bodies shall use JSON format.
- Property names shall follow camelCase naming conventions.
- Request payloads shall contain only the fields required by the operation.
- Unknown or unsupported fields should be ignored or rejected based on business requirements.

Example:

```json
{
  "title": "Spring Boot Workshop",
  "category": "Technology",
  "city": "Bengaluru",
  "capacity": 200
}
```

## Path Variables

Path variables shall uniquely identify a resource.

Example:

```
GET /api/v1/events/{eventId}
```

## Query Parameters

Query parameters shall be used for filtering, sorting, searching, and pagination.

Examples:

```
GET /api/v1/events?category=Music

GET /api/v1/events?city=Bengaluru

GET /api/v1/events?page=0&size=20

GET /api/v1/events?sort=eventDate,asc
```

## Request Headers

HTTP request headers shall follow the standards defined in **Section 4 – API Naming Standards**.

Authenticated requests must include a valid JWT access token in the `Authorization` header.

---

# 7. Response Design

All EventHub APIs shall return responses using a consistent structure to improve usability, simplify client integration, and provide predictable behavior.

Response bodies shall be returned in JSON format.

Successful responses should include:

- Success status
- Human-readable message
- Response data
- Timestamp

Error responses should include:

- Error status
- Error message
- Validation or business errors (if applicable)
- Timestamp

API responses should avoid exposing internal implementation details, stack traces, or sensitive system information.

---

# 8. Standard Response Format

To ensure consistency across all microservices, EventHub shall use a standardized response structure.

## Success Response

```json
{
    "success": true,
    "message": "Event created successfully.",
    "data": {
        ...
    },
    "timestamp": "2026-07-23T18:30:00Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

## Error Response

```json
{
    "success": false,
    "message": "Validation failed.",
    "errors": [
        {
            "field": "email",
            "message": "Email address is invalid."
        }
    ],
    "timestamp": "2026-07-23T18:30:00Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

## Response Guidelines

- All responses shall be returned in JSON.
- The success field shall indicate whether the request completed successfully.
- The message field shall contain a concise, human-readable description.
- The data field shall contain the requested resource or operation result.
- The errors field shall be returned only when applicable.
- All timestamps shall follow the ISO-8601 UTC format.

---

# 9. HTTP Status Codes

EventHub APIs shall use standard HTTP status codes consistently.

| Status Code | Meaning | Usage |
|-------------|---------------------------|------------------------------|
| 200 OK | Request successful | GET, PUT, PATCH |
| 201 Created | Resource created | POST |
| 204 No Content | Resource deleted successfully | DELETE |
| 400 Bad Request | Invalid client request | Validation failure |
| 401 Unauthorized | Authentication required | Missing or invalid JWT |
| 403 Forbidden | Access denied | Insufficient permissions |
| 404 Not Found | Resource not found | Invalid resource identifier |
| 409 Conflict | Business conflict | Duplicate resource |
| 422 Unprocessable Entity | Business validation failure | Optional |
| 500 Internal Server Error | Unexpected server error | System failure |

Status codes should accurately represent the outcome of the request and should never be misused.

---

# 10. Error Response Format

Error responses shall provide sufficient information for clients to understand and resolve request failures without exposing internal implementation details.

## Standard Error Response

```json
{
    "success": false,
    "message": "Validation failed.",
    "errors": [
        {
            "field": "email",
            "message": "Email must be a valid email address."
        },
        {
            "field": "password",
            "message": "Password must contain at least 8 characters."
        }
    ],
    "timestamp": "2026-07-23T18:30:00Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

## Error Handling Guidelines

- All responses shall be returned in JSON.
- The success field shall indicate whether the request completed successfully.
- The message field shall contain a concise, human-readable description.
- The data field shall contain the requested resource or operation result.
- The errors field shall be returned only when applicable.
- All timestamps shall follow the ISO-8601 UTC format.
- The correlationId field shall uniquely identify each request for tracing and troubleshooting across distributed services.

---

# 11. Pagination

Pagination shall be implemented for all APIs that return collections of resources to improve performance and reduce response size.

## Standard Query Parameters

| Parameter | Description | Default |
|------------|-------------|---------|
| page | Page number (zero-based) | 0 |
| size | Number of records per page | 20 |
| sort | Sorting criteria | None |

## Example

```
GET /api/v1/events?page=0&size=20&sort=eventDate,asc
```

## Guidelines

- Page numbering shall start from **0**.
- The default page size shall be **20**.
- The maximum page size shall be configurable.
- Clients may specify sorting using the sort parameter.
- Pagination responses should include metadata such as total elements, total pages, current page, and page size.

## Standard Pagination Response

All paginated APIs shall return pagination metadata using a standardized response structure.

Example:

```json
{
    "success": true,
    "message": "Events retrieved successfully.",
    "data": [
        ...
    ],
    "page": {
        "pageNumber": 0,
        "pageSize": 20,
        "totalElements": 250,
        "totalPages": 13,
        "hasNext": true,
        "hasPrevious": false
    },
    "timestamp": "2026-07-23T18:30:00Z",
    "correlationId": "6f4b4d58-8d4b-4db5-92b3-7bdb8c2b4d1a"
}
```

The platform shall not expose framework-specific pagination objects directly. Instead, all paginated responses shall follow the standardized response format defined in this document.

---

# 12. Sorting

Sorting allows clients to retrieve resources in a specific order.

## Syntax

```
sort=<field>,<direction>
```

## Examples

```
GET /api/v1/events?sort=eventDate,asc

GET /api/v1/events?sort=createdAt,desc

GET /api/v1/users?sort=lastName,asc
```

## Guidelines

- Multiple sorting fields may be supported.
- Supported directions are:
  - asc
  - desc
- Sorting shall be applied only to supported resource attributes.
- Invalid sorting fields shall return an appropriate validation error.

---

# 13. Filtering

Filtering enables clients to retrieve only the resources matching specified criteria.

## Examples

```
GET /api/v1/events?category=Music

GET /api/v1/events?city=Bengaluru

GET /api/v1/events?status=ACTIVE

GET /api/v1/events?category=Technology&city=Bengaluru
```

## Guidelines

- Filtering shall be implemented using query parameters.
- Multiple filters may be combined.
- Filtering parameters shall be validated.
- Unsupported filters shall return a validation error.
- Filtering should remain simple and intuitive for API consumers.

---

# 14. Validation

All incoming requests shall be validated before business processing begins.

Validation improves application reliability, security, and data integrity.

## Validation Guidelines

- Validate all request payloads.
- Validate path variables.
- Validate query parameters.
- Reject invalid requests with meaningful error messages.
- Return HTTP 400 (Bad Request) for validation failures.

## Common Validation Rules

- Required fields
- String length limits
- Email format
- Phone number format
- UUID format
- Numeric ranges
- Date validation
- Business rule validation

## Bean Validation

The EventHub platform shall use Jakarta Bean Validation annotations.

Examples include:

- @NotNull
- @NotBlank
- @Email
- @Size
- @Min
- @Max
- @Positive
- @Pattern

Validation errors shall follow the standard error response format defined in this document.

---

# 15. API Versioning

API versioning allows the platform to evolve without breaking existing client integrations.

EventHub shall use URI-based versioning.

## Version Format

```
/api/v1
```

Example

```
GET /api/v1/events

POST /api/v1/bookings
```

Future versions may introduce:

```
/api/v2
```

## Guidelines

- Every public API shall include a version.
- Breaking changes shall require a new API version.
- Existing versions shall be maintained until officially deprecated.
- Version numbers shall be incremented only for incompatible API changes.

---

# 16. Idempotency

Idempotency ensures that performing the same operation multiple times produces the same result without causing unintended side effects.

## Idempotent HTTP Methods

| HTTP Method | Idempotent |
|-------------|------------|
| GET | Yes |
| PUT | Yes |
| PATCH | Yes* |
| DELETE | Yes |
| POST | No |

> *PATCH should be designed carefully to ensure predictable behavior where applicable.

## Guidelines

- GET requests shall never modify server-side data.
- PUT requests shall completely replace an existing resource.
- DELETE requests shall safely handle repeated requests.
- POST requests shall create new resources and are generally not idempotent.
- Where business requirements demand safe retries (such as payment processing), idempotency keys should be considered.

---

# 17. Date and Time Standards

Consistent date and time handling is essential for interoperability across distributed systems.

## Guidelines

- All timestamps shall be stored in UTC.
- APIs shall return timestamps using the ISO-8601 standard.
- Clients may convert UTC timestamps to their local time zones for display.
- Time zone information shall not be stored as local server time.

## Example

```
2026-07-23T18:30:00Z
```

Using UTC eliminates ambiguity and simplifies communication between distributed services deployed across multiple regions.

---

# 18. UUID Standards

EventHub shall use Universally Unique Identifiers (UUIDs) as the primary identifiers for all externally exposed resources.

## Guidelines

- UUIDs shall be used for resource identifiers.
- UUIDs shall be generated by the application.
- Sequential numeric identifiers shall not be exposed through public APIs.
- UUIDs improve uniqueness and reduce predictability.

## Example

```
GET /api/v1/events/550e8400-e29b-41d4-a716-446655440000
```

Using UUIDs improves security and scalability while avoiding identifier collisions in distributed environments.

---

# 19. File Upload APIs

Some EventHub services may support file uploads, such as event banners or user profile images.

## Guidelines

- File uploads shall use `multipart/form-data`.
- Supported file formats shall be validated.
- Maximum file size shall be configurable.
- Uploaded files shall be scanned and validated before processing.
- File names shall be sanitized before storage.
- Public URLs shall not expose internal storage details.

## Supported Content Types

Examples include:

- image/jpeg
- image/png
- application/pdf

File upload endpoints shall be documented using OpenAPI (Swagger).

---

# 20. OpenAPI / Swagger Standards

All public REST APIs shall be documented using OpenAPI Specification.

Swagger UI shall be used to provide interactive API documentation for developers.

## Documentation Guidelines

- Every endpoint shall include a summary.
- Every endpoint shall include a description.
- Request examples shall be provided where appropriate.
- Response examples shall be documented.
- Error responses shall be documented.
- Required request parameters shall be clearly identified.
- Security requirements shall be documented.
- Deprecated APIs shall be marked accordingly.

Maintaining accurate API documentation improves developer experience and simplifies client integration.

---

# 21. Security Considerations

All EventHub APIs shall follow the security standards defined in the Security Architecture document.

## API Security Guidelines

- All APIs shall be accessible only over HTTPS.
- Protected endpoints shall require JWT authentication.
- Authorization shall be enforced using Role-Based Access Control (RBAC).
- Sensitive information shall never be returned in API responses.
- Input validation shall be performed for every request.
- CORS shall be configured explicitly.
- Security-related events shall be logged for auditing purposes.
- Rate limiting shall be enforced at the API Gateway where appropriate.

Security shall be considered an integral part of API design rather than an afterthought.

---

# 22. Architecture Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| API Style | REST | Industry-standard architectural style |
| Data Format | JSON | Lightweight and widely supported |
| Resource Naming | Plural nouns | Improves consistency and readability |
| API Versioning | URI-based (`/api/v1`) | Explicit and easy to manage |
| Authentication | JWT | Stateless and scalable |
| Authorization | RBAC | Fine-grained access control |
| Resource Identifier | UUID | Globally unique and secure |
| Date Format | ISO-8601 UTC | Standardized across systems |
| Documentation | OpenAPI / Swagger | Interactive API documentation |
| Pagination | Standardized custom response | Avoids exposing framework-specific objects |

---

# 23. References

## Internal Documents

- [System Overview](system-overview.md)
- [Technology Stack](technology-stack.md)
- [Communication Patterns](communication-patterns.md)
- [Deployment Architecture](deployment-architecture.md)
- [Security Architecture](security-architecture.md)
- [Database Architecture](database-architecture.md)

## External References

- REST Architectural Style
- RFC 9110 – HTTP Semantics
- OpenAPI Specification

---

# 24. Version History

| Version | Date | Author | Changes |
|----------|------------|----------------|-----------------------------|
| 1.0 | 23-Jul-2026 | Sowmyaa Shetty | Initial version |