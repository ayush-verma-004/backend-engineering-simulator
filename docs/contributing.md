# Contributor Onboarding Guide

Welcome to the Backend Engineering Simulator! This guide will help you set up your local development environment and run your first commands.

## Prerequisites

Ensure you have the following installed on your machine:
1. **Java Development Kit (JDK) 21** (Temurin or Oracle LTS recommended)
2. **Maven 3.8+** (Optional, but useful if running globally. The platform module contains wrapper configurations)
3. **MySQL Server 8.x** (Our primary development database)

---

## Local Setup

### 1. Database Setup
Create a local database named `backendsim` in your MySQL instance:
```sql
CREATE DATABASE backendsim;
```
Ensure your database credentials match the configuration in [application-local.yml](file:///e:/Case%20Study%20For%20Backend/backend-engineering-simulator/platform/src/main/resources/application-local.yml). You can also configure environment variables to override the defaults.

### 2. IDE Setup
- **EditorConfig**: Install the EditorConfig plugin for your IDE (IntelliJ IDEA, VS Code, or Eclipse) if it is not supported natively. This automatically aligns formatting rules (tabs, indentations).
- **Lombok**: Make sure the Lombok plugin is installed and annotation processing is enabled in your IDE settings.

---

## Building and Running

Navigate to the `platform` directory to perform build and run actions.

### Compile and Verify
To format, compile the project, and run all automated tests, execute:
```bash
mvn clean spotless:apply test
```

### Start the Application
To run the Spring Boot application locally:
```bash
mvn spring-boot:run
```

Once started:
- **Actuator Health check**: [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)
- **Swagger/OpenAPI Documentation**: [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)

---

## Contributing Process

All additions to this repository are completed by solving engineering tickets.

1. **Find a Ticket**: Select an unassigned task from the roadmap or tickets queue.
2. **Follow the Workflow**: Review [Branching Strategy & Git Workflow](file:///e:/Case%20Study%20For%20Backend/backend-engineering-simulator/docs/branching-strategy.md) for details on code changes, commits, and Pull Requests.
3. **Submit**: Open a Pull Request on GitHub and tag the project owner for code review.
