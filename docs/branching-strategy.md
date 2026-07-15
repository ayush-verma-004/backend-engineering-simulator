# Branching Strategy & Git Workflow

To maintain a clean and trackable commit history, all contributors must follow this branching strategy and Git workflow.

## Branch Naming Conventions

All development must be done on branch names that start with a prefix indicating the ticket type, followed by the ticket identifier:

*   **Feature Branches**: `feature/TSK-xxx-short-description`
*   **Bug Fix Branches**: `bugfix/TSK-xxx-short-description`
*   **Refactoring Branches**: `refactor/TSK-xxx-short-description`
*   **Documentation Branches**: `docs/TSK-xxx-short-description`

### Examples
- `feature/TSK-001-bootstrap-platform`
- `bugfix/TSK-042-fix-validation-response`

---

## The Workflow

The repository simulates a real collaborative environment. Direct pushes to the `main` branch are blocked. The following flow must be followed:

```
[Main Branch]
     │
     ├───► Create branch (e.g. feature/TSK-001)
     │         │
     │         ├───► Make local commits (Semantic commits)
     │         │
     │         ├───► Run local checks (mvn spotless:check test)
     │         │
     │         └───► Push branch and open Pull Request
     │                   │
     │                   ├───► CI Pipeline executes automated tests
     │                   │
     │                   ├───► Peer Code Review
     │                   │
     │                   └───► Squash and Merge to Main
     ▼
[Updated Main]
```

### 1. Work Allocation
- Make sure you are assigned to a ticket (e.g. `TSK-001`).
- Pull the latest changes from `main`.
- Create your working branch locally:
  ```bash
  git checkout -b feature/TSK-001-bootstrap-platform
  ```

### 2. Commit Message Standard
Commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
- `feat(platform): add global exception handler`
- `fix(security): resolve cors wildcard issue`
- `docs(logging): document naming conventions`
- `test(validation): add tests for email validator`

Include the Ticket ID in the commit body:
```
feat(platform): add global exception handler

- Add RestControllerAdvice to intercept platform exceptions
- Map custom exceptions to standard ApiResponse payload

Ref: TSK-001
```

### 3. Local Verification
Before pushing, ensure that your code compiles, matches formatting rules, and passes all tests:
```bash
mvn clean spotless:apply test
```

### 4. Pull Requests
- Push your branch to GitHub.
- Open a Pull Request from your branch to `main`.
- Fill out the Pull Request template completely.
- Address any comments or requests for changes raised during the Code Review phase.
- Once approved and CI checks pass, the PR will be **Squashed and Merged** into the `main` branch.
