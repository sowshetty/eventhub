# Authentication Service Architecture

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Authentication Service Architecture |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Authentication Service is responsible for user authentication and authorization within the EventHub platform. It verifies user credentials, issues JWT tokens, manages refresh tokens, and enforces role-based access control (RBAC). It serves as the centralized Identity and Access Management (IAM) component for all microservices.

---

# 2. Responsibilities

The Authentication Service is responsible for:

- User Registration
- User Login
- User Logout
- JWT Access Token Generation
- Refresh Token Management
- Email Verification
- Password Reset
- Token Validation
- Role Assignment
- Authentication Audit Logging

The following responsibilities are **out of scope**:

- Event Management
- Booking Management
- Payment Processing
- Notification Management
- Analytics
- User Profile Management

---

# 3. High-Level Architecture

```text
                Client Applications
                        │
                        ▼
                 API Gateway
                        │
                        ▼
          Authentication Service
        ┌───────────────────────────┐
        │ Registration              │
        │ Login                     │
        │ JWT Generation            │
        │ Refresh Token Management  │
        │ Email Verification        │
        │ Password Reset            │
        └─────────────┬─────────────┘
                      │
         ┌────────────┴─────────────┐
         ▼                          ▼
 PostgreSQL Database         Email Service
         │
         ▼
 Other Microservices
```

---

# 4. Authentication Workflow

### Registration

1. User registers.
2. Password is hashed using BCrypt.
3. User account is created.
4. Verification email is sent.

### Login

1. Validate email and password.
2. Verify account status.
3. Generate JWT Access Token.
4. Generate Refresh Token.
5. Store hashed Refresh Token.
6. Return tokens.

### Access Protected APIs

1. Client sends JWT Access Token.
2. API Gateway validates token.
3. Request is forwarded to the target service.

### Refresh Token

1. Client submits Refresh Token.
2. Validate token.
3. Rotate Refresh Token.
4. Generate new Access Token.
5. Return new tokens.

### Logout

1. Remove stored Refresh Token.
2. Access Token expires naturally.

---

# 5. Database Overview

## Users

| Field | Description |
|--------|-------------|
| id | UUID |
| email | User email |
| password_hash | BCrypt hash |
| role | USER / ORGANIZER / ADMIN |
| status | ACTIVE / INACTIVE |
| email_verified | Boolean |
| created_at | Timestamp |
| updated_at | Timestamp |

## Refresh Tokens

| Field | Description |
|--------|-------------|
| id | UUID |
| user_id | User reference |
| token_hash | Hashed refresh token |
| expires_at | Expiration time |
| revoked | Boolean |

---

# 6. REST API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/v1/auth/register | Register user |
| POST | /api/v1/auth/login | Login |
| POST | /api/v1/auth/refresh | Refresh access token |
| POST | /api/v1/auth/logout | Logout |
| POST | /api/v1/auth/forgot-password | Request password reset |
| POST | /api/v1/auth/reset-password | Reset password |
| GET | /api/v1/auth/verify-email | Verify email |
| GET | /api/v1/auth/me | Current authenticated user |

---

# 7. Security Considerations

- Stateless Authentication
- JWT Access Tokens
- Refresh Token Rotation
- BCrypt Password Hashing
- HTTPS Communication
- Role-Based Access Control (RBAC)
- Email Verification
- Secure Password Reset
- Account Locking after repeated failed login attempts (future enhancement)

---

# 8. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Authentication | Stateless JWT |
| Password Hashing | BCrypt |
| Authorization | RBAC |
| Database | PostgreSQL |
| Refresh Tokens | Stored as hashed values |
| Access Token Expiry | 15 Minutes |
| Refresh Token Expiry | 7 Days |
| Session Storage | None |
| Email Verification | Mandatory |
| Password Reset | Token-Based |

---

# 9. Future Enhancements

- OAuth2 Login (Google/GitHub)
- Multi-Factor Authentication (MFA)
- Redis Token Cache
- Device Management
- Session Management
- Login History
- Audit Dashboard
- Single Sign-On (SSO)

---

# 10. References

- RFC 7519 – JSON Web Token (JWT)
- Spring Security Documentation
- OWASP Authentication Cheat Sheet
- OAuth 2.0 Security Best Current Practice

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 30-Jul-2026 | Initial Authentication Service Architecture |