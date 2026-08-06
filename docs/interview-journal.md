# EventHub Interview Journal

> Interview preparation notes based on concepts implemented during the EventHub project.

**Project:** EventHub – Enterprise Cloud-Native Event Management Platform

**Author:** Sowmyaa Shetty

---

# Chapter 1 - Maven & Spring Boot Fundamentals

## Q1. What is Maven?

### Answer

Maven is a build automation and dependency management tool for Java projects. It manages dependencies, compiles source code, runs tests, packages applications, and provides a standard project structure.

---

## Q2. What is POM?

### Answer

POM stands for **Project Object Model**. It is the `pom.xml` file that defines project metadata, dependencies, plugins, Java version, and build configuration.

---

## Q3. What is a Parent POM?

### Answer

A Parent POM provides common project configuration that child projects inherit. In Spring Boot, `spring-boot-starter-parent` supplies dependency versions, plugin configuration, compiler settings, and default build behavior.

---

## Q4. What is the difference between `dependencyManagement` and `dependencies`?

### Answer

`dependencyManagement` defines dependency versions but does not add them to the project.

`dependencies` actually downloads and adds the required libraries to the application.

---

## Q5. What is a BOM (Bill of Materials)?

### Answer

A BOM is a special Maven POM that centrally manages compatible versions of related libraries. Spring Cloud uses a BOM to ensure all Spring Cloud modules work together correctly.

---

## Q6. What is a transitive dependency?

### Answer

A transitive dependency is a library automatically downloaded because another dependency requires it. Maven resolves these dependencies automatically.

---

## Q7. What is IoC (Inversion of Control)?

### Answer

IoC is a design principle where the Spring Framework manages object creation and lifecycle instead of the application creating objects manually.

---

## Q8. What is Dependency Injection?

### Answer

Dependency Injection is a technique where Spring automatically provides required objects (dependencies) to a class instead of the class creating them.

---

## Q9. What does `@SpringBootApplication` do?

### Answer

`@SpringBootApplication` combines three annotations:

- `@Configuration`
- `@EnableAutoConfiguration`
- `@ComponentScan`

It enables configuration, auto-configuration, and component scanning for a Spring Boot application.

---

## Q10. Why do we use `application.yaml`?

### Answer

`application.yaml` externalizes application configuration from source code. YAML provides a cleaner and more readable hierarchical structure than traditional properties files.

---

## Q11. Why does Eureka Server use `register-with-eureka: false` and `fetch-registry: false`?

### Answer

Because the Discovery Server hosts the service registry itself. It does not register with another Eureka server or fetch a registry from one.

---

## Spring Cloud Config – Interview Notes

### Q1. Why do we use Spring Cloud Config Server?

**Answer:**

Spring Cloud Config Server centralizes application configuration in a Git repository, allowing multiple microservices to share and manage configuration from a single location without rebuilding application code.

---

### Q2. What is the role of `spring.config.import`?

**Answer:**

`spring.config.import=configserver:http://localhost:8888` tells the application to fetch its configuration from the Config Server during startup before loading the application context.

---

### Q3. How does Config Server identify which configuration file to load?

**Answer:**

Config Server uses the value of `spring.application.name`. For example:

```yaml
spring:
  application:
    name: discovery-service
```

loads:

```text
discovery-service.yaml
```

from the configuration repository.

---

### Q4. Why is configuration stored outside the application?

**Answer:**

Externalized configuration allows centralized management, environment-specific settings, version control, and configuration changes without modifying application code.

---

## API Gateway – Interview Notes

### Q1. Why do we use an API Gateway in Microservices?

**Answer:**

API Gateway acts as the single entry point for client requests. It routes requests to the appropriate microservices and provides centralized capabilities such as authentication, logging, rate limiting, and request routing.

---

### Q2. Why is API Gateway a Config Client?

**Answer:**

API Gateway loads its configuration from Spring Cloud Config Server using:

```yaml
spring:
  config:
    import: "configserver:http://localhost:8888"
```

This keeps configuration externalized and centrally managed.

---

### Q3. How does API Gateway register with Eureka?

**Answer:**

API Gateway uses the Spring Cloud Eureka Client dependency. During startup, it connects to Eureka Discovery Server using the configured `defaultZone` and registers itself so other services can discover it.

---

### Q4. Why did Spring Initializr generate `spring-cloud-starter-gateway-server-webmvc` instead of the older Gateway dependency?

**Answer:**

Spring Boot 4.x generates the Spring MVC variant of Spring Cloud Gateway. It is suitable for applications built using the traditional Spring MVC programming model and integrates well with Spring Data JPA and blocking database access.

---
