# Severity Rubric

## Critical

Confirmed issue likely to cause severe security exposure, data loss,
or widespread production failure.

## High

Confirmed or strongly evidenced issue that breaks a core invariant,
creates a serious reliability risk, or blocks a critical workflow.

## Medium

Meaningful coupling, testability, or maintainability problem with
a concrete impact or a credible recurring failure scenario.

## Low

Localized improvement with limited risk and modest expected benefit.

## Severity considerations

Assess user-visible impact, blast radius, duration, recoverability, and the
system of record. Loss of a rebuildable cache or projection is not equivalent
to loss of canonical business data; explain its operational impact before
assigning High or Critical severity.

When describing persistence reliability, verify the actual store and driver
semantics. Do not infer multi-record atomicity from a single method call,
bulk API, repository name, or batch request. State whether atomicity applies
to one record, a whole transaction, or neither, and include deployment
prerequisites when a transaction is recommended.

## Confidence

High: directly demonstrated by code, tests, or execution.

Medium: supported by code evidence but dependent on assumptions
about runtime behavior or business requirements.

Low: plausible concern requiring additional evidence.

Do not increase severity because a design violates a named pattern.
Do not label speculative improvements as defects.

For each finding, separate severity from confidence. If a concern
cannot be tied to an actual risk, report it as an optional improvement.
