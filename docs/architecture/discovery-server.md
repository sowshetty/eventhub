# Discovery Server

| **Project** | EventHub – Event Management Platform |
|--------------|--------------------------------------|
| **Document** | Discovery Server |
| **Version** | 1.0 |
| **Status** | Final |
| **Author** | Sowmyaa Shetty |

---

# 1. Introduction

The Discovery Server enables automatic service registration and discovery within the EventHub microservices ecosystem. It eliminates hardcoded service URLs and allows services to locate each other dynamically.

---

# 2. Responsibilities

- Register microservices
- Maintain service registry
- Enable service discovery
- Support dynamic scaling
- Remove unavailable service instances

---

# 3. High-Level Architecture

```text
          Authentication Service
                  │
          User Service
                  │
          Event Service
                  │
          Booking Service
                  │
          Payment Service
                  │
          Notification Service
                  │
                  ▼
         +----------------------+
         |   Discovery Server   |
         +----------------------+
                  ▲
                  │
             API Gateway
```

---

# 4. Workflow

1. Service starts.
2. Service registers with Discovery Server.
3. API Gateway discovers available services.
4. Requests are routed dynamically.
5. Unavailable instances are removed automatically.

---

# 5. Technology

- Spring Cloud Netflix Eureka
- Spring Boot
- REST Communication

---

# 6. Architecture Decisions (ADR)

| Decision | Choice |
|----------|--------|
| Discovery | Eureka Server |
| Registration | Automatic |
| Registry | Centralized |
| Communication | REST |
| Scaling | Dynamic |

---

# 7. Future Enhancements

- Kubernetes Service Discovery
- Consul Support
- Multi-Region Discovery

---

# 8. References

- Spring Cloud Netflix Eureka
- Spring Cloud Documentation

---

# Version History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 31-Jul-2026 | Initial Discovery Server Architecture |