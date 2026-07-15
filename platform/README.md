# Platform Foundation Module

This module contains the cross-cutting, reusable backend foundation for the **Backend Engineering Simulator**. It serves as the baseline for all subsequent functional business modules (e.g. Users, Products, Orders).

## Core Capabilities Included

1. **Standardized REST API Envelope**: All API endpoints return a unified JSON layout containing fields like `success`, `data`, `error`, and `timestamp` (see [ApiResponse](file:///e:/Case%20Study%20For%20Backend/backend-engineering-simulator/platform/src/main/java/com/backendsim/platform/response/ApiResponse.java)).
2. **Unified Base Exception Hierarchy**:
   - `BaseException` (abstract parent)
   - `BusinessException` (logical violations)
   - `InfrastructureException` (system connection/integration failures)
   - Pre-configured HTTP mappings (e.g. `ResourceNotFoundException` maps directly to HTTP `404`).
3. **Centralized Error Interceptor**: Intercepts validation errors (`@Valid`), custom business failures, and internal server errors, turning them into standard JSON structures via [GlobalExceptionHandler](file:///e:/Case%20Study%20For%20Backend/backend-engineering-simulator/platform/src/main/java/com/backendsim/platform/exception/GlobalExceptionHandler.java).
4. **Spring Security Integration**: Ready for OAuth2/JWT extensions; initialized as "permit all" for Sprint 0.
5. **OpenAPI & Swagger Documentation**: Auto-generates interactive API docs available at `/swagger-ui/index.html`.
6. **Unified Logging Profile**: Custom SLF4J/Logback configurations separating local console prints from JSON-ready files suitable for cloud log engines.

---

## Technical Stack

- **Java 21** (LTS)
- **Spring Boot 3.3.x**
- **Maven**
- **MySQL** (Primary Database Connection)
- **Lombok** (Boilerplate mitigation)
- **Spotless** (Automatic Google Java Format formatting checks)

---

## Quick Start

### Build and Test
Make sure MySQL database `backendsim` is running locally before booting:
```bash
mvn clean spotless:apply test
```

### Run Locally
To boot the application:
```bash
mvn spring-boot:run
```

Once running, verify connectivity:
- Swagger Documentation: [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
- OpenAPI JSON Spec: [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)
- Actuator Health: [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)
