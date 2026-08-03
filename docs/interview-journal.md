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