# Skill behavior evaluation scenarios

Use this reference only when reviewing or improving Architecture Guardian itself. These are manual acceptance scenarios, not commands to run against a user's project.

## Scenarios

1. **Small CRUD service with no complex invariants:** identify its actual stack and flow; do not demand aggregates, repositories, CQRS, or extra ports without a concrete reason.
2. **Business workflow with a critical state transition:** trace entry point through policy, persistence, and response; identify who enforces the invariant and what failure could bypass it.
3. **CQRS with an asynchronous projection:** inspect both paths, consistency expectations, duplicate handling, projection recovery, and publication durability; do not equate CQRS with Event Sourcing or separate databases.
4. **Polyglot monorepo:** infer each package's language/toolchain from its own manifests and CI; trace cross-language contracts; do not assume JavaScript tooling or one root package manager governs every module.
5. **Heuristic architecture lint rules:** check effective scope, ignores, aliases, and rule behavior; do not report a rule name or disabled check as proof that source code is defective or correct.
6. **Unfamiliar framework or incomplete requirements:** use local documentation and source evidence, mark unknowns, and avoid inventing conventions or business requirements.

## Behavioral test fixtures and expected outcomes

Use these small fixtures as prompt-based evaluations. Give the agent only the fixture and a request to audit it; compare its response to the expected outcomes rather than matching exact wording.

### A. Go CRUD without evidenced domain complexity

```text
go.mod
GET /products/{id} -> handler -> ProductService.Get -> SQL SELECT -> JSON response
POST /products -> handler validates required name -> SQL INSERT
No product lifecycle rules or cross-record invariants are provided.
```

Expected: identify Go from the module/source evidence; trace the read and
create paths; report that no complex DDD boundary is evidenced. Do not require
an Aggregate, Repository, CQRS, value object, or extra port based only on
Hexagonal Architecture vocabulary.

### B. Java transfer invariant

```text
POST /transfers -> TransferController -> TransferFundsUseCase
The use case loads two Accounts, calls source.withdraw(amount), then
destination.deposit(amount) inside one transaction. Account.withdraw rejects
amounts above the available balance. The repository saves both Accounts.
```

Expected: map the actor, flow, invariant owner, transaction boundary, and
repositories. Do not report the controller or repository pattern itself as a
defect. If the code evidence confirms the transaction and invariant, state
what was checked; do not invent a missing concurrency requirement.

### C. CQRS projection with delivery failure modes

```text
The command commits an Order row, then publishes OrderPlaced directly.
The broker provides at-least-once delivery. The projection consumer adds the
order total every time it receives the event and stores no processed-event
identity. A crash can occur between the database commit and publish.
```

Expected: identify the durable-publication gap and duplicate-application risk
as separate reliability findings; discuss an outbox and idempotent projection
updates; state the need to define visible projection lag. Do not require a
separate read database or Event Sourcing.

### D. Polyglot monorepo

```text
services/catalog/go.mod
workers/recommendations/pyproject.toml
The Go service publishes a versioned JSON event consumed by the Python worker.
There is no root package manager or shared build command.
```

Expected: detect and report the toolchain per component, trace the event
contract across the language boundary, and avoid assuming a single root
package manager. If compatibility behavior is not shown, mark it unverified.

### E. Heuristic lint boundaries

```text
The ESLint flat config has a global ignore for tests and a later test-only
override. Query handlers reject imports matching ../domain and calls to
.save(); import-x/no-cycle is off. Code also uses @domain aliases and update().
```

Expected: report test override/ignore overlap and the narrow query heuristics
as enforcement-coverage risks; note the explicitly disabled cycle check.
Do not infer that production code violates architecture without tracing it.

### F. Unfamiliar framework and missing requirements

```text
The project uses an unfamiliar framework. A class named OrderAggregate has
no visible invariant in the inspected code. No domain requirements or tests
are available.
```

Expected: inspect local conventions/docs if available, mark domain rules as
unknown, and avoid calling the model anemic or requiring a factory solely
from its name.

### G. Inconsistent findings and persistence atomicity

```text
The report summary says 5 confirmed findings and 3 potential risks. The body
contains AG-001 through AG-007, marks AG-007 Confirmed while stating it is not
a runtime defect, and mentions two further risks without finding IDs. It
also recommends replacing delete + insert with one MongoDB bulkWrite to make
the multi-document replacement atomic.
```

Expected: reconcile counts and statuses; move a non-defect capability gap to
optional improvements; number in-scope risks or mark/exclude out-of-scope
observations; do not describe bulkWrite as multi-document atomic. Recommend
a transaction only after checking deployment support, or describe a recovery/
staging design with its actual atomic switch and failure semantics.

### H. Missing business contract, overlapping findings, and latent exposure

```text
A TypeScript application has an AdscriptionName constructor that calls
value.trim().toUpperCase() but discards the result. Existing tests expect the
original casing, and no product requirement says names must be normalized.
An ActiveAdscriptionsFinder calls an unfiltered findAll; a general list also
returns inactive rows, while its read model omits isActive. The module's HTTP
routes and DI registration are commented out. A use case authorizes
Action.Update before deactivating an aggregate; the project also defines
Action.Deactivate, but its role-to-action policy is not inspected. Domain
events are recorded but there are no subscribers or stated consumers.
```

Expected: identify the active-only query mismatch as a source-confirmed defect
and explain that its current exposure is latent while the module is unwired.
Do not call normalization a confirmed business defect without a requirement;
report the discarded expression as a code fact and classify the desired
normalization as unresolved or optional. Consolidate overlapping list/read
model symptoms unless a distinct contract and correction are evidenced.
Report the authorization action mismatch separately from any claim of
privilege escalation, which requires policy/role evidence. Treat event
publication as conditional on consumers or requirements; do not demand a
broker/outbox by default. Rate severity using current reachability and avoid
double-counting one root cause.

## Acceptance criteria

- The stack and scope are stated from evidence, and stack-specific references are loaded only when relevant.
- At least one critical or representative use case is traced end to end when the task scope supports it.
- Findings cite evidence and distinguish confirmed behavior, assumptions, and missing evidence.
- A confirmed defect is tied to an evidenced expected contract; suspicious code alone does not establish product intent.
- Overlapping symptoms are consolidated or their distinct contracts are explained; severity reflects current reachability as well as conditional future impact.
- Pattern recommendations connect to a concrete risk or responsibility and mention a simpler alternative.
- No pattern is required solely because it is named in this skill.
- Commands are recommendations unless the user authorizes execution; unknown effects are surfaced before running them.
- The report omits irrelevant sections and does not imply that uninspected areas passed.
