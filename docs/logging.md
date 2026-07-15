# Logging Architecture & Philosophy

This document outlines the logging philosophy, log levels, naming conventions, and the future observability/tracing roadmap for the **Backend Engineering Simulator**.

## Logging Philosophy

Logs are the primary eyes and ears of a software engineer in production. Our logging design follows three rules:
1. **Actionability**: A log statement must contain enough context for an engineer to act on it. Avoid noise logs like `Entering method foo()` or `Exiting method foo()`.
2. **Standardization**: All logs must follow standard patterns to enable parsing by log collectors (e.g. Logstash, FluentBit).
3. **Security-First**: Never print sensitive data (passwords, JWTs, personal identification data, credit card numbers) in log files.

---

## Log Levels

We strictly enforce the usage of log levels:

| Level | Usage Description |
| :--- | :--- |
| **ERROR** | Serious failures that require immediate attention (e.g., database connection down, third-party API outage). Always includes the stack trace. |
| **WARN** | Unexpected occurrences that are not critical but warrant investigation (e.g., high response latency, invalid client configurations). |
| **INFO** | Business-significant events (e.g., database updates completed, application boot success, external call initiated). |
| **DEBUG** | Detailed diagnostic data useful during local development and testing. Excluded from production logs. |
| **TRACE** | Fine-grained messages showing step-by-step logic. Extremely noisy, only enabled in debugging scenarios. |

---

## Logger Naming Conventions

- Always utilize SLF4J's `LoggerFactory.getLogger(ClassName.class)` or Lombok's `@Slf4j` annotation.
- Never use `System.out.println` or `Throwable.printStackTrace()`.

---

## Distributed Tracing & Request IDs (Future Strategy)

To debug distributed transactions or trace a user's request path across the system, the platform is structured to support correlation and tracing in future sprints.

### 1. Request IDs
- Every request entering the system should be assigned a unique `X-Request-ID` (UUID) at the Gateway/Filter layer.
- This ID is loaded into Logback's **MDC (Mapped Diagnostic Context)**.
- The Logback pattern will automatically prepend the Request ID to every log line printed during that thread's lifecycle.

### 2. Correlation IDs
- For transactions that span multiple services (e.g. Orders talking to Payments via HTTP/Messaging), a `X-Correlation-ID` is passed in request headers.
- If a service receives a Correlation ID, it propagates it to outbound requests. If none exists, it generates one.
- This allows engineers to trace a transaction's journey across the entire service ecosystem.

### 3. Logback Layouts
- **Local Console Logs**: Clean, colored, and human-readable format.
- **Production Logs**: JSON format. Structured attributes (including Request ID, Correlation ID, Logger Name, Log Level, Timestamp) are printed as keys, allowing ELK or Grafana Loki to index them efficiently without regex parsing.
