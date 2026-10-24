# Architecture Guardian — Audit Report

## 1. Executive summary

- Project:
- Detected architecture:
- Scope:
- Overall assessment:
- Assessment scope and lenses applied:
- Confirmed findings:
- Potential risks:
- Optional improvements:
- Checks executed:
- Lint/static-analysis configuration(s) and representative file classes inspected (if applicable):

## 2. Architecture and domain overview

Summarize the detected architecture and stack, key business capabilities,
bounded contexts/modules, external actors/systems, and material assumptions.
Include only what evidence supports; omit details that do not apply.

## 3. Representative use-case traces

List the selected use cases and why they were selected. For each, summarize:
trigger/entry point -> application behavior -> domain invariant/state change
-> boundary/port -> adapter/effect -> result/failure/consistency.
Link each step to source evidence. Mark missing steps as unknown or not observed.

## 4. Findings

### [AG-001] [Severity] Title

- **Category:** Architecture / Hexagonal / DDD / CQRS / EDA / SOLID / Reliability / Pattern
- **Confidence:** High / Medium / Low
- **Affected use case/boundary:** (when identifiable)
- **Location:** `path/to/file.ext:line-line` (when available)
- **Status:** Confirmed defect / Potential risk / Optional improvement / Resolved

**Evidence**

Describe the observed code, contract, dependency, or validation behavior.
Separate facts from assumptions and cite locations.

**Risk**

Explain the concrete failure scenario or maintenance cost.

**Recommendation**

Describe the smallest appropriate correction.

**Verification**

List regression tests or checks that would verify the correction; distinguish
recommended, executed, passed, failed, and not run.

## 5. Dependency boundaries

- Forbidden dependencies:
- Circular dependencies:
- Framework leakage:
- Unverified boundaries:

## 6. Domain model (when relevant)

- Aggregate boundaries:
- Business invariants:
- Value objects and entities:
- Repository and Factory design:
- Domain and application services:
- Criteria/query objects versus domain Specifications:
- CQRS command/query paths and consistency guarantees (if applicable):

## 7. Events and integration (when relevant)

- Event ownership:
- Transaction and publication behavior:
- Idempotency and retries:
- Contract compatibility:
- Read-model/projection lag, retries, idempotency, and rebuild behavior (if applicable):

## 8. Pattern recommendations (when relevant)

Include only observed or justified candidate patterns. For each, state the
problem solved, expected benefit, trade-off, and simpler alternatives.

## 9. Prioritized recommendations

Order by impact and confidence. Separate necessary corrections from optional
improvements; do not add work solely to make the design more pattern-complete.

## 10. Validation results

| Check             | Result                | Notes |
| ----------------- | --------------------- | ----- |
| Type checking / compilation | PASS / FAIL / NOT RUN |       |
| Lint / static analysis      | PASS / FAIL / NOT RUN |       |
| Architecture      | PASS / FAIL / NOT RUN |       |
| Unit tests        | PASS / FAIL / NOT RUN |       |
| Integration tests | PASS / FAIL / NOT RUN |       |
| Build             | PASS / FAIL / NOT RUN |       |

## 11. Scope and limitations

Document unassessed flows, missing evidence, unexecuted checks, stack-specific
limitations, assumptions, and risks that need human review. Omit irrelevant
sections instead of filling them with generic text.

Before delivery, make sure the executive summary counts match the findings
and optional improvements below. Do not count unnumbered observations or
classify an acknowledged non-defect as confirmed.
