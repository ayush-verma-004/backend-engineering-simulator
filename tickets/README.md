# Repository Engineering Tickets Guide

This directory documents the tickets, sprint organization, naming conventions, and workflows for developers contributing to the **Backend Engineering Simulator**.

## Ticket Format
Every engineering ticket in this repository follows a strict structure to resemble issues in a real-world enterprise environment:
1. **Ticket ID**: Unique reference key (e.g. `TSK-001`).
2. **Title**: Concise description of the goal.
3. **Priority**: Criticality level (`Low`, `Medium`, `High`, `Critical`).
4. **Sprint**: Associated Sprint iteration.
5. **Story**: Narrative format describing who wants what and why.
6. **Business Context**: Explains the background business value.
7. **Current & Expected Behaviour**: Clarifies the delta between existing and target code paths.
8. **Acceptance Criteria**: Strict checkboxes mapping completeness requirements.
9. **Technical Notes**: Architecture rules, modules, or dependencies to target.
10. **Hints**: Pointers or clues to guide implementation.
11. **Estimated Difficulty**: Classification (`Easy`, `Medium`, `Hard`).
12. **Learning Objective**: Key software engineering practices or APIs to master by solving the ticket.

---

## Sprint Organization
- **Sprint 0 (Platform Foundation)**: Cross-cutting, technical bootstrapping (Maven, resources, error interceptors, OpenAPI structures, security skeletons).
- **Sprints 1-5 (Core Business Domains)**: User registers, product details catalog, inventory bookings, shopping carts, checkout payments.
- **Sprints 6-9 (Operations Controls)**: Caching layers, Redis storage integrations, database schema migration frameworks.
- **Sprints 10-14 (Enterprise Extensions)**: JWT Token validations, RabbitMQ/Kafka queues, distributed logging/tracing engines.
- **Sprints 15-20 (Production Tuning)**: Gateway configurations, circuit breaking architectures, microservices extraction steps.

---

## Naming Conventions & Branch Setup
- Branch prefix determines the work scope:
  - Feature branches: `feature/TSK-xxx-short-desc`
  - Bug fixes: `bugfix/TSK-xxx-short-desc`
  - Refactoring: `refactor/TSK-xxx-short-desc`
  - Documentation: `docs/TSK-xxx-short-desc`
- Commit messages should comply with **Conventional Commits**:
  - `feat(modules): add user registration service`
  - `fix(platform): correct global error response parsing`
  - `docs(tickets): update readme files`

---

## Contributor Workflow
Contributors follow the standard team pipeline to complete tickets and merge changes:
1. **Selection**: Find an unassigned ticket in the roadmap or issue board.
2. **Planning**: Analyze the requirement, check related files, and write a technical approach.
3. **Coding**: Implement clean, Google-formatted code. Run `mvn spotless:apply` to auto-format.
4. **Testing**: Add MockMvc/Integration tests and run `mvn test` under the `test` profile.
5. **PR Submission**: Open a Pull Request on GitHub using the [PULL_REQUEST_TEMPLATE](file:///e:/Case%20Study%20For%20Backend/backend-engineering-simulator/.github/PULL_REQUEST_TEMPLATE.md).
6. **Code Review**: Address developer comments and fix formatting or logical errors.
7. **Merge**: Peer-approved PRs with successful builds will be squashed and merged to `main`.
