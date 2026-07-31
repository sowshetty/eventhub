# Configuration Server Architecture

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Configuration Server Architecture |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Configuration Server centralizes application configuration for all EventHub microservices. It enables consistent configuration management, environment-specific settings, and simplifies maintenance across the platform.

---

# 2. Responsibilities

- Centralized configuration management
- Environment-specific configuration
- Externalized application properties
- Configuration versioning
- Dynamic configuration updates (future)

---

# 3. High-Level Architecture

```text
                 Git Repository
                        │
                        ▼
          +---------------------------+
          |  Configuration Server     |
          +-------------+-------------+
                        │
      ┌─────────────────┼─────────────────┐
      ▼                 ▼                 ▼
Authentication      User Service     Event Service
     ▼                 ▼                 ▼
Booking Service   Payment Service  Notification Service
```

---

# 4. Workflow

1. Service starts.
2. Service requests configuration from Configuration Server.
3. Configuration Server loads properties from Git Repository.
4. Configuration is returned to the requesting service.
5. Service starts using the retrieved configuration.

---

# 5. Technology

- Spring Cloud Config Server
- Git Repository
- Spring Boot

---

# 6. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Configuration Storage | Git Repository |
| Configuration Access | Spring Cloud Config |
| Environment Support | Dev / QA / Prod |
| Configuration Format | YAML |

---

# 7. Future Enhancements

- Configuration Encryption
- Dynamic Configuration Refresh
- Vault Integration
- Kubernetes ConfigMaps & Secrets

---

# 8. References

- Spring Cloud Config Documentation
- Spring Boot External Configuration

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Configuration Server Architecture |