# Contributing

Thanks for helping evaluate Architecture Guardian. It is an experimental instruction set; reproducible evidence is more useful than broad claims that an audit was simply good or bad.

## Report a skill evaluation

Use the [skill evaluation issue template](.github/ISSUE_TEMPLATE/skill-evaluation.md). Include, when available:

- Skill version or commit/tag
- Agent product/harness and model identifier
- Project language, framework, and architecture context
- Audit mode and scope
- Sanitized prompt and relevant output excerpts
- Expected behavior, observed behavior, and the specific criterion that passed or failed
- Whether source inspection, tests, or commands were actually performed

Do not upload proprietary source code, credentials, personal data, customer data, or confidential reports. Redact repository names and paths when needed. Keep claims distinguishable from assumptions and avoid presenting model output as verified fact.

## Propose a change

1. Describe the failure mode or improvement and the evidence that motivates it.
2. Add or update a manual fixture in `references/skill-evaluation.md` with expected outcomes.
3. Update the smallest relevant instruction/reference file.
4. Check links, terminology, and consistency between English and Spanish documentation.
5. Record validation performed and any remaining limitations.

The skill must remain language-agnostic. Ecosystem-specific rules belong in conditional references and must not be generalized to unrelated stacks. Do not add executable helpers unless a repeated deterministic task materially benefits from one and its behavior is documented.

## Versioning and releases

Use the repository's annotated Git tags and GitHub Releases as the source of published versions. Follow the prerelease sequence documented in `README.md` and `README.es.md`; update `CHANGELOG.md` for each release. Do not create or move a published version tag to a different commit.
