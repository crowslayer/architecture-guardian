# CQRS

Read this reference when the code separates commands from queries, uses command/query handlers, maintains read projections, or someone proposes CQRS.

## Establish whether CQRS is present and useful

CQRS separates the model or path used to change state from the model or path used to read it. It can be useful when write rules and read needs differ materially, or when independent scaling, ownership, or performance needs justify the extra coordination.

Do not equate CQRS with separate databases, microservices, messaging, event sourcing, or a handler class for every operation. A single process and database can have clear command/query separation. Do not recommend CQRS solely because a codebase has classes named `Command` and `Query`.

Trace real call paths and state effects. Names, folders, ESLint selectors, and interfaces are clues, not proof.

## Command path

Trace inbound request -> command -> handler/use case -> domain behavior -> persistence and transaction boundary. Check that:

- Commands express intent and are validated at the appropriate boundary.
- Business invariants are enforced in the domain or responsible policy, not only in controllers or handlers.
- A command has a clear success/failure contract and transaction boundary.
- Writes do not silently bypass aggregate rules through direct ORM or repository updates when those rules must hold.
- Retries, duplicate submissions, and idempotency are addressed where transport or callers can repeat commands.

Do not require an aggregate or repository for every command; assess the consistency and ownership requirements.

## Query path

Trace inbound request -> query -> handler -> read model/projection -> data source. Check that:

- Queries do not cause business state changes or publish command-like side effects.
- Read models return only the required data and do not expose persistence/vendor types across boundaries without a reason.
- Read-side access does not accidentally mutate state through shared ORM entities or implicit persistence behavior.
- Query-side use of domain logic is evaluated by actual responsibility; do not ban all domain imports mechanically if the design intentionally shares pure policies or value semantics.

Read models may use projections or direct optimized queries without loading write aggregates when that is safe for the use case. A separate read database is an option, not a requirement.

## Consistency and operations

When writes update projections asynchronously or use separate stores, inspect:

- The atomicity gap between committing a write and publishing its event (consider an outbox when loss is possible and durability matters).
- Eventual-consistency expectations, acceptable projection lag, and user-visible behavior after a command.
- Duplicate delivery, idempotent projection updates, ordering, retries, poison messages, and replay/rebuild procedures.
- Schema/version compatibility and ownership of event contracts.
- Monitoring for failed consumers and projection lag.

Avoid prescribing distributed transactions or event sourcing without concrete requirements.

## Tests and evidence

Match tests to the guarantees: command invariant tests, handler orchestration tests, query result tests, persistence/projection integration tests, and retry/idempotency/consistency tests where applicable. State which guarantees are not verified.

Report a CQRS finding only with a concrete path, state effect, violated boundary, or credible failure scenario. Separate a confirmed defect from an architectural trade-off or optional improvement. Recommendations should describe benefit, complexity, simpler alternatives, and how to verify the change.
