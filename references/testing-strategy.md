# Testing Strategy

Choose verification according to the behavior and risk being addressed.
Map test levels to the project's language and tooling; the categories below
describe purposes, not required framework names or directory structures.

- Domain unit tests: business rules, value objects, and invariants.
- Application tests: use-case orchestration and port interactions.
- Adapter integration tests: database, HTTP, messaging, and vendor contracts.
- Architecture tests: forbidden dependencies and module boundaries.
- Regression tests: previously reproducible defects.
- End-to-end tests: critical user-visible workflows when justified.

A missing test level is a coverage risk, not automatically a product defect.
Tie it to an important use case or invariant and avoid duplicating a test-gap
finding when the same tests already appear as verification for a confirmed
defect. Do not claim a test fails or gives false confidence unless its
assertion, contract mismatch, or execution demonstrates that conclusion.

Mock external boundaries when useful, but do not mock every internal
method or use mocks as proof of architectural correctness.

Prefer the project's existing test runner when execution is authorized.
For infrastructure adapters, prefer real integration tests where
they provide stronger evidence than mocks.

Recommend focused checks first, then the relevant broader suite. Execute
them only under the authorization policy in `SKILL.md`. Report exactly which
checks ran and their outcomes; distinguish unrun recommendations from passes.
