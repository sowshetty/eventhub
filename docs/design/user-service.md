# User Service Design

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | User Service Design |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The User Service manages user profile information and preferences. It is responsible only for profile-related operations and delegates authentication and authorization to the platform security components.

---

# 2. Responsibilities

- Create user profile
- View user profile
- Update user profile
- Manage profile picture
- Manage user preferences

**Out of Scope**

- User Login
- User Registration
- Password Management
- JWT Generation
- Email Verification

---

# 3. High-Level Architecture

```text
            Client
               │
               ▼
         API Gateway
               │
      JWT Validation
               │
               ▼
         User Service
               │
               ▼
            user_db
```

---

# 4. Security Flow

### Authentication

- JWT is validated by the API Gateway.
- Authentication is managed by the Authentication Service.

### Authorization

User Service authorizes operations using JWT claims.

Examples:

- USER can update only their own profile.
- ADMIN can access all user profiles.

---

# 5. Database Overview

**Database**

`user_db`

**Primary Table**

| Table |
|--------|
| user_profiles |

---

# 6. API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /api/v1/users/me | Get logged-in user profile |
| PUT | /api/v1/users/me | Update own profile |
| GET | /api/v1/users/{id} | Get user by ID (Admin) |

---

# 7. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Database | PostgreSQL |
| Authentication | JWT |
| Authorization | RBAC |
| Communication | REST |
| Profile Ownership | User Service |

---

# 8. Future Enhancements

- Profile Image Upload
- Address Management
- User Preferences
- Social Login Profile Sync

---

# 9. References

- Spring Boot Documentation
- Spring Data JPA Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial User Service Design |