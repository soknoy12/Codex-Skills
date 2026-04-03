# Architecture Checklist

Use this checklist to deepen a recommendation or review an existing proposal.

## 1. Problem Frame

- What outcome is the system supposed to enable?
- What are the highest-value user or business flows?
- What must remain true if the system is partially degraded?
- What existing constraints cannot realistically be changed soon?

## 2. Architecture Drivers

Review these drivers and rank the ones that matter most:

- Delivery speed
- Team autonomy
- Scalability
- Availability
- Latency
- Data consistency
- Security
- Compliance
- Cost efficiency
- Operability
- Extensibility

Do not optimize equally for every driver. Make the priority order visible.

## 3. Boundary Heuristics

Use these signals when proposing boundaries:

- Separate components when ownership, scaling, security, or release cadence differs.
- Keep components together when the workflow is tightly coupled and operational simplicity matters more.
- Prefer a modular monolith when the domain is still changing quickly or the team is small.
- Prefer service separation when independent scaling or blast-radius control is clearly required.

## 4. Data Design Questions

- What are the sources of truth?
- Which data needs strong consistency?
- Which data is read-heavy and benefits from derived views or caching?
- What retention, audit, or lineage needs exist?
- What data crosses tenant or trust boundaries?
- What data access patterns drive storage choice?

## 5. Integration Questions

- Which flows require immediate user feedback?
- Which flows can be asynchronous?
- Where would retries create duplicates or side effects?
- Which events should be treated as facts versus implementation details?
- How will consumers evolve without breaking producers?

## 6. Reliability And Operations

- Identify likely failure modes.
- Define graceful degradation behavior.
- Define observability for golden signals and business-critical flows.
- Decide where idempotency is required.
- Decide how backpressure and traffic spikes are handled.
- Decide which dependencies need circuit breaking, timeouts, and retries.

## 7. Security And Governance

- Define trust boundaries.
- Define authentication and authorization points.
- Define secrets handling and key rotation expectations.
- Define tenant isolation strategy if multi-tenant.
- Define audit logging requirements.
- Define data classification or compliance constraints.

## 8. Recommendation Template

Use this compact template when drafting the final answer:

```text
Problem:
Architecture drivers:
Assumptions:

Options considered:
1. ...
2. ...

Recommended architecture:
- Entry points:
- Core components:
- Data stores:
- Integration style:
- Deployment shape:

Why this option:
Risks:
Open questions:
Phased rollout:
```

## 9. Review Red Flags

Watch for these common problems:

- Microservices chosen without a clear scaling or ownership reason
- Event-driven design used where synchronous workflows dominate
- Single database chosen without clarifying access patterns or consistency needs
- Cross-cutting concerns left implicit
- No migration path from current state to target state
- Diagrams that show components but not responsibilities or boundaries
- Architecture that assumes senior operations maturity the team does not have
