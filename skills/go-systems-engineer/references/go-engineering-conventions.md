# Go Engineering Conventions

Use this reference when the task needs deeper implementation guidance than the main `SKILL.md` should carry.

## Package Design

Prefer small, cohesive packages with obvious responsibilities.

- Keep public APIs narrow.
- Avoid circular dependencies by keeping dependency direction simple.
- Group by domain or responsibility when it improves readability.
- Do not introduce interfaces by default; add them when multiple implementations, testing seams, or package decoupling truly benefit.

For larger services, a shape like this is often reasonable:

```text
cmd/
  app/
internal/
  config/
  transport/
  service/
  store/
  domain/
  observability/
pkg/        # only for reusable public libraries when truly needed
```

Adjust to the repository's conventions when they are already coherent.

## Error Handling

- Return errors explicitly.
- Wrap errors with useful context.
- Use sentinel errors sparingly and intentionally.
- Keep error messages actionable and easy to trace in logs.
- Avoid panics except for truly unrecoverable startup or programmer errors.

## Context And Cancellation

- Accept `context.Context` for request-scoped work, I/O, background jobs, and long-running operations.
- Pass context through call chains rather than recreating it.
- Do not store contexts in structs.
- Honor cancellation and deadlines when interacting with external systems.

## Concurrency

Add concurrency only when it materially improves throughput, latency, or isolation.

- Prefer the simplest correct pattern.
- Define ownership of shared state clearly.
- Use channels for coordination and pipelines when that improves clarity.
- Use mutexes when shared mutable state is simpler than channel choreography.
- Bound worker pools and background queues.
- Design shutdown and cancellation behavior explicitly.

Avoid goroutine leaks and hidden background work.

## Testing

- Write table-driven tests where they improve clarity.
- Test business logic without over-mocking.
- Prefer black-box tests for package behavior when practical.
- Add integration tests for file system, network, process, or persistence behavior when that behavior matters.
- Keep tests readable and deterministic.

## CLI And Tooling Guidance

For CLIs and internal tools:

- Keep command structure discoverable.
- Print helpful usage and error messages.
- Separate parsing, orchestration, and side effects.
- Use structured output formats only when they materially help automation.
- Default to safe behavior; make destructive actions explicit.

## Skill Authoring Guidance

When building a Codex skill with Go support:

- Keep trigger conditions in the frontmatter description.
- Keep the main instructions compact and procedural.
- Use `references/` for long guides, schemas, or variant-specific material.
- Add Go helper scripts only for validation, normalization, generation, or repetitive parsing that benefits from deterministic execution.
- Include tests for helper scripts when the logic is important.
- Remove placeholder files before packaging.

## Output Expectations

When the user wants generated deliverables rather than direct edits, prefer:

1. Short implementation plan
2. Skill or package name
3. Folder structure
4. Complete contents or created artifacts
5. Validation and packaging notes
6. Follow-up improvements
