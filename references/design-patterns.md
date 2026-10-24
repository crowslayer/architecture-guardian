# Design Patterns

Evaluate patterns based on the problem they solve, not their presence.

## Repository and Unit of Work

Use when persistence boundaries, aggregate loading, or transaction
coordination require explicit abstractions. Avoid generic wrappers
that merely rename ORM operations.

## Factory and Abstract Factory

Use for complex valid construction or families of interchangeable
objects. Avoid factories that only delegate to a trivial constructor.

## Adapter

Use to translate external contracts into internal contracts.
Keep vendor-specific models and errors from leaking unnecessarily.

## Decorator

Use for composable cross-cutting behavior such as metrics, caching,
or carefully defined authorization. Verify ordering and error semantics.

## Strategy

Use when interchangeable algorithms or policies are genuinely needed.
Prefer a simple conditional when there is no meaningful variation.

## Specification

Use for reusable, domain-meaningful predicates. Avoid creating a
framework for simple one-off boolean expressions.
For read filters, sorting, or pagination, consider a Criteria/query object
at the query boundary instead; do not encode transport filters as domain
specifications without a domain rule.

## Anti-corruption layer and process coordination

Use an anti-corruption layer to translate a foreign model or contract when
direct coupling would leak external concepts into the domain. A small Adapter
may be enough; do not build a second domain model without a real boundary.

Use a process manager or Saga for a long-running workflow that coordinates
multiple independently committed steps and needs explicit progress, retries,
or compensation. Compensation is a new business action, not a database
rollback. Prefer a direct application service for a short local transaction.

Use Event Sourcing only when the event history must be the authoritative
source of state and the business needs justify replay, versioning, and
operational complexity. Publishing events or using CQRS does not imply
Event Sourcing.

## Observer and Mediator

Evaluate lifecycle management, hidden coupling, execution order,
and error propagation. Avoid implicit communication when direct calls
are clearer and sufficient.

## Dependency Injection

Use explicit composition and dependencies. Do not require a DI
container for small applications without a demonstrated benefit.

## Rule for recommendations

For each proposed pattern, state:

1. The current problem.
2. Why the simpler alternative is insufficient.
3. The expected benefit and trade-off.
4. How the change will be tested.

## Pattern selection rule

Classify each pattern as **observed**, **candidate**, **not applicable**, or
**unknown**. Recommend a pattern only after tracing a concrete responsibility
or failure scenario. Keep architectural styles, principles, design patterns,
and implementation tactics distinct. A pattern's presence is not evidence
of quality, and its absence is not a defect by itself.
