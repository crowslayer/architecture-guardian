# Domain discovery and use-case tracing

Read this reference for architecture audits, reviews, or refactors that cross business or system boundaries. It applies regardless of language, framework, or deployment model.

## Discover the domain from evidence

Use available sources in proportion to the task: product requirements, user stories, acceptance criteria, domain glossary, architecture decisions, API/event contracts, database schema, tests, and implementation. Start from business outcomes and state transitions, not class names or directory layout.

Identify only what the evidence supports:

- Actors, external systems, triggers, and business capabilities.
- Important use cases and their observable outcomes.
- Business terms, entities, value objects, lifecycle states, and invariants.
- Ownership of data and policy across modules, bounded contexts, or services.
- Consistency and transaction expectations, including cross-boundary work.
- Errors, authorization rules, retries, duplicate requests, and side effects where relevant.

Separate documented requirements, behavior demonstrated by code/tests, and assumptions. When requirements are absent, do not invent them. State which invariant or business expectation could not be confirmed. Ask only when that uncertainty blocks a safe change; otherwise continue with explicit assumptions and scope limits.

DDD is most useful when the system has meaningful business rules, lifecycle, or consistency boundaries. For simple CRUD or infrastructure-focused components, say that DDD constructs are not relevant or not evidenced instead of manufacturing aggregates, repositories, or bounded contexts.

## Select flows to trace

Trace a manageable, risk-based sample:

- For an audit, select critical state-changing and read flows, external integrations, and flows with security, money, inventory, identity, or other high-impact invariants.
- For a code review, trace changed behavior and neighboring callers, persistence, and consumers.
- For a refactor, trace the target behavior and its existing transaction, error, and compatibility contracts before editing.

Do not map every endpoint if several share the same path. Explain how representative flows were selected and what was outside scope.

## Trace one use case end to end

For each selected use case, record the evidence-backed path using the names and concepts present in the project. The terms below are conceptual roles; a language or architecture may express them differently.

1. **Trigger:** actor, scheduled job, message, CLI invocation, or system event; include the entry point.
2. **Request:** input, validation, authorization, and command/query intent where applicable.
3. **Application behavior:** orchestration, transaction boundary, policy coordination, and result/error contract.
4. **Domain behavior:** state transition, responsible entity/value object/policy, and invariant checked or potentially bypassed.
5. **Ports or equivalent contracts:** dependencies required by the use case, who owns each contract, and whether a concrete outer detail leaks inward.
6. **Adapters and effects:** database/API/queue/filesystem calls, mapping, emitted events, and external side effects.
7. **Completion and failure:** persisted outcome, returned response, rollback/compensation, retry/idempotency behavior, and consistency visible to callers.

Use exact file/function/symbol locations when available. Mark a step `unknown` or `not observed` when evidence is missing. Do not fill a gap with a likely-sounding framework convention.

## Evaluate the trace through Hexagonal and Clean Architecture

Follow dependencies and runtime control flow separately. A dependency diagram alone cannot prove which operation runs; a call graph alone cannot prove that business policy is independent.

For each flow, check:

- Does an inbound boundary translate external input into an internal request?
- Does application/domain policy depend on stable abstractions or on volatile transport, framework, persistence, or vendor details?
- Are output contracts owned by an appropriate inner component, with concrete implementations wired at an outer boundary or equivalent composition point?
- Are transactions and persistence mappings located where the chosen architecture expects them?
- Can core business behavior be exercised without starting unrelated external infrastructure, where that independence is a design goal?
- Do cross-module or cross-service calls preserve ownership and avoid exposing internal models accidentally?

Treat these as questions about dependency and change boundaries, not demands for one folder per ring, interface per class, or a ports-and-adapters naming scheme. Report the concrete direction, boundary, and resulting risk.

## Findings from incomplete traces

A missing link is not automatically a violation. Classify it as:

- **Confirmed:** source, tests, runtime configuration, or execution shows a concrete violation or defect.
- **Potential:** the trace exposes a plausible risk, but requirements or runtime behavior are not available to confirm it.
- **Not assessed:** the flow or system area was outside scope or evidence was unavailable.

Tie each recommendation to a use case and failure/maintenance scenario. Prefer the smallest correction that protects the required behavior and boundary.
