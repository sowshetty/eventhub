# Security Architecture

---

## 1. Purpose

This document defines the security architecture of the EventHub platform. It describes the authentication and authorization mechanisms, API protection strategy, credential management, communication security, audit logging, and security best practices adopted across all services.

The objective of this architecture is to ensure that the platform protects user identities, business data, and application resources while maintaining scalability, maintainability, and compliance with modern security standards.

---

## 2. Scope

This document applies to all backend microservices, APIs, infrastructure components, and deployment environments within the EventHub platform.

The architecture covers:

- User authentication
- Authorization and access control
- Token management
- Password security
- API security
- Secure service communication
- Configuration and secret management
- Audit logging
- Security monitoring

Client-side implementation details are outside the scope of this document.

---

## 3. Security Architecture Overview

EventHub follows a layered security model where authentication, authorization, and infrastructure security work together to protect application resources.

```
                    Client Applications
                            │
                            ▼
                    HTTPS / TLS
                            │
                            ▼
                   Kubernetes Ingress
                            │
                            ▼
                   API Gateway
                            │
             JWT Authentication Filter
                            │
             Authorization (RBAC)
                            │
                            ▼
                  Backend Microservices
                            │
        ┌─────────────────────────────────┐
        │                                 │
        ▼                                 ▼

   PostgreSQL                     Infrastructure Services

 Refresh Tokens              Redis / Kafka / Elasticsearch
 User Credentials
```

The API Gateway acts as the primary entry point for client requests and forwards authenticated requests to downstream services.

---

## 4. Authentication

EventHub uses stateless authentication based on JSON Web Tokens (JWT).

Supported authentication features include:

- User Registration
- User Login
- User Logout
- Email Verification
- Forgot Password
- Reset Password
- Change Password
- Refresh Token

Authentication is handled by the Authentication Service.

Successful authentication results in:

- Access Token generation
- Refresh Token generation
- Audit log creation

---

## 5. Authorization

EventHub implements Role-Based Access Control (RBAC).

Supported roles include:

| Role | Description |
|------|-------------|
| SUPER_ADMIN | Full platform administration |
| ADMIN | Administrative operations |
| EVENT_ORGANIZER | Event creation and management |
| CUSTOMER | Event discovery and booking |

Authorization decisions are enforced using Spring Security and validated before business logic execution.

---

## 6. Token Management

The platform uses two types of tokens.

| Token | Purpose | Expiry |
|--------|---------|--------|
| Access Token | API Authorization | 15 Minutes |
| Refresh Token | Access Token Renewal | 7 Days |

### Access Token

- JWT
- Digitally signed
- Stateless
- Contains user identity and roles
- Sent with every authenticated request

### Refresh Token

- Random secure token
- Stored in PostgreSQL
- Associated with a user account
- Can be revoked
- Supports secure logout
- Supports token rotation

Access tokens are never stored in the database.

---

## 7. Password Security

Passwords are never stored in plain text.

Security measures include:

- BCrypt hashing
- Password strength validation
- Secure password reset process
- Password confirmation during registration
- Password change requires current password verification

Future enhancements may include password history enforcement and configurable password policies.

---

## 8. API Security

All APIs are categorized as either public or protected.

### Public APIs

Examples include:

- Login
- Registration
- Forgot Password
- Reset Password
- Health Check

### Protected APIs

All authenticated business operations require a valid Access Token.

Authorization is enforced through Spring Security before the request reaches the application layer.

---

## 9. Communication Security

All external communication must use HTTPS.

Transport Layer Security (TLS) protects:

- Authentication requests
- API communication
- Sensitive user information
- Administrative operations

Plain HTTP is not permitted in production environments.

---

## 10. Configuration and Secret Management

Application configuration is externalized.

Configuration sources include:

- Kubernetes ConfigMaps
- Kubernetes Secrets
- Environment Variables

Sensitive information includes:

- Database credentials
- JWT signing keys
- API keys
- SMTP credentials
- Third-party integration secrets

Sensitive values are never committed to source control.

Future cloud deployments may integrate with AWS Secrets Manager.

---

## 11. Audit Logging

Security-sensitive operations are recorded for auditing purposes.

Examples include:

- User login
- User logout
- Failed login attempts
- Password changes
- Password resets
- Role modifications
- Account status changes
- Token revocation

Audit logs support operational monitoring and security investigations.

---

## 12. Security Monitoring

The platform continuously monitors application security events.

Monitoring includes:

- Authentication failures
- Authorization failures
- Excessive login attempts
- Suspicious request patterns
- Service health
- Security-related application logs

Operational dashboards are provided through Prometheus, Grafana, and Loki.

---

## 13. References

### Internal Documents

- [System Overview](system-overview.md)
- [Technology Stack](technology-stack.md)
- [Deployment Architecture](deployment-architecture.md)

---

### External References

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Application Security Verification Standard (ASVS)](https://owasp.org/www-project-application-security-verification-standard/)
- [RFC 7519 - JSON Web Token (JWT)](https://www.rfc-editor.org/rfc/rfc7519)
- [Spring Security Reference Documentation](https://docs.spring.io/spring-security/reference/)

---

## Version History

| Version | Date | Author | Changes |
|----------|------------|----------------|-----------------------------|
| 1.0 | 23-Jul-2026 | Sowmyaa Shetty | Initial version |