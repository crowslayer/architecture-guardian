# Event-Driven Architecture

## Event types

Distinguish:

- Domain events: facts meaningful inside a bounded context.
- Integration events: facts published across process or service boundaries.
- Commands: requests to perform an action, not facts that already happened.

## Reliability checks

Investigate:

- Is an event emitted before the business transaction commits?
- Can a consumer process the same event more than once?
- Can a crash lose a message between database commit and publication?
- Are retry policies bounded and are failed messages observable?
- Are event contracts versioned and compatible?
- Does correctness depend on event ordering?

## Outbox and idempotency

Recommend an outbox when durable publication must be coordinated
with a database transaction and direct dual writes could lose events.

Recommend idempotent consumers when duplicate delivery is possible
or the transport provides at-least-once delivery.

Do not prescribe distributed transactions, event sourcing, or a message
broker without a requirement that justifies the complexity.

## Testing

Verify business event creation, transaction behavior, consumer
idempotency, retry behavior, and contract compatibility as relevant.
