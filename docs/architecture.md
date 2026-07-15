# Platform Architecture

This document describes the architectural philosophy, structure, and technical layout of the **Backend Engineering Simulator** platform module.

## Architectural Philosophy

Unlike typical sandbox or tutorial projects, this repository simulates a real-world enterprise codebase. The platform architecture is guided by the following principles:

1. **Simplicity Over Abstraction**: We avoid premature abstractions. We do not use complex layered architectures (such as Clean Architecture, Hexagonal, or DDD patterns) during the early stages of development.
2. **Production Readiness**: Every component is built to mimic a real system, including logging, security, standard exception handling, and tracing.
3. **Contributor Friendliness**: The repository is designed to be easily understandable for new developers. Onboarding should require minimal time.

---

## Package Organization

The platform implements a flat, specialized package structure under the root package `com.backendsim.platform`. This layout groups common capabilities cleanly and allows contributors to quickly locate relevant platform infrastructure.

- **`common/`**: Contains globally accessible constant definitions, common models, and system-wide objects.
- **`config/`**: Contains Spring Boot configuration classes (e.g., Jackson configuration, CORS setups, WebMvc parameters, and OpenAPI configuration).
- **`exception/`**: Houses the base exception hierarchy (`BaseException`, `BusinessException`, etc.) and the centralized `GlobalExceptionHandler`.
- **`logging/`**: Houses request logging filters, tracing interception code, and MDC utility wrappers.
- **`response/`**: Contains standard API response templates (`ApiResponse`, `ApiError`, `ValidationError`).
- **`security/`**: Configures Spring Security filters and permissions.
- **`utils/`**: Utility helper classes containing static methods for common operations.
- **`validation/`**: Custom validation annotations and validator implementations.

---

## Modular Monolith Structure

To keep deployment and testing simple, the project is organized as a modular monolith. 

- The `platform` module serves as the technical foundation (cross-cutting concerns).
- Business capabilities (e.g., User Management, Products, Orders) will be introduced in future sprints as independent packages under `com.backendsim.modules`.
- Business packages will import and consume platform utilities but should remain decoupled from each other to simplify eventual microservice migration.
