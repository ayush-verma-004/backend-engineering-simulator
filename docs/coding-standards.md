# Coding Standards & Guidelines

This document outlines the coding standards, style guidelines, and code practices enforced on this project. All code submitted in Pull Requests must comply with these guidelines.

## Code Style Enforcement

We use the **Spotless Maven Plugin** configured with **Google Java Format** to automatically enforce formatting standards.

- Do not spend time manually formatting files.
- To format your code automatically before committing, run:
  ```bash
  mvn spotless:apply
  ```
- The CI pipeline will execute `mvn spotless:check`. Any PR with formatting violations will fail the build immediately.

---

## Language & Framework Rules

### Java 21 Features
Leverage modern Java 21 syntax where appropriate:
- Use **Records** for simple data-carrier objects (DTOs, simple payload templates).
- Use pattern matching for `switch` and `instanceof`.
- Use text blocks for multiline strings (e.g. database schemas, JSON payloads in tests).
- Utilize standard collection factory methods (e.g., `List.of()`, `Map.of()`).

### Lombok Usage
Lombok is configured to reduce boilerplate, but should be used carefully:
- Prefer `@Data` only on mutable classes (if any).
- For immutable structures, use `@Value` or standard Java Records.
- Prefer explicit constructor injection over `@Autowired` (or use Lombok's `@RequiredArgsConstructor` on Spring components).
- Avoid placing `@EqualsAndHashCode` on JPA entities unless you define natural business keys.

### Spring Boot Best Practices
- **No Field Injection**: Always use constructor injection.
- **Validation**: Validate all incoming DTO payloads using standard validation annotations (`@NotNull`, `@NotBlank`, `@Size`, etc.) in controller signatures.
- **REST Endpoints**:
  - Always return HTTP responses wrapped in the standard `ApiResponse` envelope.
  - Follow correct REST verbs and HTTP status codes (e.g. `201 Created` for creations, `204 No Content` for empty responses, `404` for missing resources).

---

## Clean Code Principles

- **Readability First**: Code is read much more often than it is written. Keep methods small and focused.
- **Self-Documenting Code**: Choose descriptive names for variables, methods, and classes. Avoid names like `temp`, `data`, or `obj`.
- **Minimal Comments**: Only add comments to explain *why* something is done, never *what* the code is doing. If code requires comments to explain its operation, it should be refactored.
- **No Dead Code**: Do not commit commented-out code blocks or unused imports. Spotless automatically cleans unused imports.
- **No Placeholder TODOs**: Do not leave random `// TODO` comments in the codebase. All tasks should be tracked as formal issues or tickets.
