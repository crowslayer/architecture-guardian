# Changelog

Notable user-facing changes to Architecture Guardian are recorded here.

## [Unreleased]

## [0.1.0-alpha.2] - 2026-10-24

- Refined defect classification against missing requirements and conflicting tests.
- Added guidance to consolidate overlapping findings and rate severity using current runtime reachability.
- Clarified how to report authorization action mismatches without claiming an unverified privilege escalation.
- Added regression fixture H for missing business contracts, duplicate findings, and latent exposure.
- Updated English and Spanish validation notes and added a structured evaluation feedback issue template.
- Known limitation: fixture G partially passes in Cursor; the report still ambiguously presents MongoDB `bulkWrite` as an alternative to atomic multi-document replacement.

## [0.1.0-alpha.1] - 2026-10-24

- Initial alpha release of the polyglot architecture audit flow.
- Added domain discovery, use-case tracing, and references for Hexagonal/Clean Architecture, DDD, CQRS, event-driven design, ESLint, testing, and severity.
- Added behavioral fixtures A–G.
- Known limitation: fixture G exposed inconsistent finding counts/statuses and ambiguous MongoDB atomicity guidance; the follow-up alpha addresses count/status consistency, but the `bulkWrite` wording remains to be corrected.
