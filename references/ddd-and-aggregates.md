# DDD and Aggregates

## Entities and Value Objects

Evaluate identity, equality, lifecycle, and business behavior.
Value objects should protect their validity and preferably be immutable.
Equality should follow domain meaning: value objects compare by their values;
entities are distinguished by stable identity and lifecycle. Adapt immutability
to the language and persistence model without weakening invariants.

Do not introduce value objects for every primitive without a domain
reason. Prioritize values with meaningful invariants or semantics.

## Aggregate and Aggregate Root

An aggregate is a consistency boundary, not simply an object graph.

Verify:

- Which invariants must hold atomically?
- Which entity owns those invariants?
- Can callers mutate internal entities without root validation?
- Are cross-aggregate rules handled with appropriate consistency?
- Are aggregates loaded and persisted at suitable boundaries?
- Can concurrent updates violate an invariant, and is the chosen concurrency
  control (locking, versioning, serializable transaction, or another mechanism)
  evidenced and appropriate?

The root must protect mutations that could violate its invariants.
It does not necessarily need to expose every internal entity.

Avoid both oversized aggregates and artificial splitting without
evidence of contention, consistency needs, or domain ownership.

## Repository

Repositories should express meaningful persistence operations for
aggregate roots or domain-specific access needs.

Check whether:

- Domain code imports ORM entities or database clients.
- Persistence mapping is separated where required.
- Queries bypass invariants or aggregate consistency.
- A generic repository obscures useful query semantics.

Do not require a repository for every entity or read-only query.
Distinguish a repository that loads and persists aggregate state from a DAO,
query service, or read-model query optimized for reads. These may coexist;
judge their ownership and behavior rather than their names.

## Criteria and Specification

These terms overlap across libraries, so inspect their actual semantics.

- **Criteria/query object:** describes query constraints such as filters,
  sorting, and pagination. It commonly belongs to an application/read or
  persistence boundary and should not be mistaken for a domain invariant.
- **Specification:** represents a reusable, domain-meaningful predicate or
  eligibility rule. Keep it side-effect-free and independent of persistence
  details when it is domain policy.

Do not require either pattern for a one-off query or boolean expression.
If a specification is translated into a database query, verify the in-memory
and persisted interpretations agree where correctness depends on it.

## Factory

Use factories for complex creation, domain-specific construction,
or cases where valid initialization deserves a named operation.

Simple construction should remain simple.

## Domain services

Use a domain service when domain behavior does not naturally belong
to one entity or value object. Keep orchestration of use cases in
application services.

## Evidence

Cite the actual invariant, mutation path, or dependency involved.
A naming convention alone is not proof of a DDD violation.
