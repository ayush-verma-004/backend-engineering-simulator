# Database Migrations

This folder is prepared for database schema migrations.

Future sprints will integrate **Flyway** (e.g. at Sprint 9).
When Flyway is active, all SQL DDL migration files (e.g., `V1__init_schema.sql`, `V2__add_user_table.sql`) must be placed in this directory.

Rules for migrations:
1. File naming pattern: `V<Version>__<Description>.sql` (note the double underscores).
2. SQL scripts should be database-agnostic where possible, targetting the primary database dialect (MySQL).
3. Once a migration script is merged, it MUST NOT be modified. Any schema adjustment requires a new versioned migration.
