# Spring Boot Conventions

Use this reference when the task needs a fuller implementation checklist or a concrete package template.

## Recommended Package Shape

For a typical feature or module, prefer a structure like:

```text
src/main/java/com/example/app/
  config/
  controller/
  dto/
  exception/
  mapper/
  domain/
  repository/
  security/
  service/
```

Test packages should mirror the production layout under `src/test/java`.

If the project already uses feature-based packaging, preserve that pattern when it is coherent.

## Feature Implementation Checklist

When building a new feature, consider whether it needs:

- Request and response DTOs
- Validation annotations
- Mapper layer
- Service layer with transaction boundaries
- Repository queries or specifications
- Domain entities and enums
- Flyway migration
- Exception types and controller advice handling
- Security rules and method or endpoint authorization
- OpenAPI annotations
- Logging, metrics, and health implications
- Unit and integration tests
- Docker or environment configuration updates

## API Conventions

- Use nouns for resources and consistent endpoint naming.
- Return `201 Created` for successful creates.
- Return `204 No Content` for successful deletes or idempotent operations with no body.
- Return `400 Bad Request` for validation failures.
- Return `404 Not Found` when a requested resource does not exist.
- Return `409 Conflict` when business invariants or uniqueness constraints fail.
- Return `401` or `403` correctly depending on authentication versus authorization failure.

Prefer explicit DTOs over exposing entities directly.

## JPA Guidance

- Keep entities focused on domain state.
- Avoid bidirectional relationships unless they are clearly helpful.
- Prefer lazy loading by default and fetch joins or entity graphs where needed.
- Guard against N+1 query issues in list and detail endpoints.
- Keep repository interfaces simple; move business orchestration into services.

## Flyway Guidance

- Add a migration for every schema change.
- Name migrations clearly and keep them deterministic.
- Include indexes, foreign keys, and uniqueness constraints when they are part of the domain model.
- Keep schema evolution backward-compatible when rolling deployments matter.

## Security Guidance

- Fail closed by default.
- Protect mutating endpoints explicitly.
- Keep token parsing, authentication setup, and authorization rules separate from business logic.
- Never trust client-supplied identity or tenant context without server-side verification.

## Testing Guidance

- Unit-test core business logic and validation-heavy branches.
- Use integration tests for persistence behavior, transaction behavior, and security rules.
- Use Testcontainers for PostgreSQL-backed integration tests when the repository already supports it or the feature depends on real database behavior.
- Avoid brittle tests that mirror implementation details too closely.

## Output Expectations

When the user wants generated code rather than direct repository edits, prefer:

1. Implementation plan
2. File tree
3. Complete file contents
4. Test summary
5. Run instructions
6. Follow-up improvements

When working inside a real repository, prefer making the changes directly and summarizing them clearly.
