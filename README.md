# Architecture Guardian

**A language-agnostic Agent Skill for evidence-based software architecture audits.** It discovers the stack and domain, traces use cases, and evaluates boundaries, invariants, dependencies, and design choices without requiring patterns by default.

[Español](README.es.md) · **Alpha** · [MIT License](LICENSE) · [Report feedback](.github/ISSUE_TEMPLATE/skill-evaluation.md)

> This project is experimental. Audit quality depends on the agent, model, repository context, and tools available. Verify findings against source code and project requirements.

## What it does

- Audits Hexagonal and Clean Architecture, DDD, CQRS, event-driven systems, SOLID, and relevant patterns across languages and technologies.
- Discovers domain concepts from requirements, contracts, tests, and code, then traces representative use cases through their effects and failure paths.
- Separates confirmed defects, potential risks, assumptions, unknowns, and optional improvements.
- Recommends existing project checks without installing dependencies or running commands automatically.
- Includes no executable scripts. Its manual behavioral fixtures live in [references/skill-evaluation.md](references/skill-evaluation.md).

## Quick start

Copy the **entire `architecture-guardian` directory**, including `SKILL.md`, `references/`, and `templates/`, into a skills directory recognized by your agent. See the platform-specific locations below. Then ask the agent to audit a repository in Audit mode, or explicitly request Review or Refactor mode.

Example prompt:

```text
Use Architecture Guardian in Audit mode. Discover the stack and domain,
trace the main use cases, and report evidence-backed architectural findings.
Do not execute commands or modify files.
```

## Platform support

Agent Skills portability is about the format and instructions. It does not mean every model or product automatically discovers the skill, reads its references, or supports the same tools. Installation paths and feature availability can change.

| Platform | Documented loading path or method | Behavioral validation in this project |
| --- | --- | --- |
| OpenCode | `.opencode/skills/architecture-guardian/` or `~/.config/opencode/skills/architecture-guardian/` | Not yet recorded |
| Claude Code | `.claude/skills/architecture-guardian/` or `~/.claude/skills/architecture-guardian/` | Not yet recorded |
| Claude.ai | Import a ZIP of the skill when Skills are available to the account | Not yet recorded |
| Gemini CLI | `.gemini/skills/architecture-guardian/` or `.agents/skills/architecture-guardian/` | Not yet recorded |
| Codex | `.agents/skills/architecture-guardian/` in a supported user or project scope | Not yet recorded |
| DeepSeek Deep Code | `.deepcode/skills/architecture-guardian/` or `~/.agents/skills/architecture-guardian/` | Not yet recorded |
| Cursor | Depends on the agent's skill discovery and project configuration | Two field runs on one TypeScript/MongoDB project; regression G partially passes |

The platform paths above are based on vendor documentation, not end-to-end tests of this skill. Other products from Anthropic, Google, OpenAI, or DeepSeek are not covered merely because they share a model provider.

Official documentation: [Agent Skills specification](https://agentskills.io/specification) · [OpenCode](https://docs.opencode.ai/docs/skills/) · [Claude Code](https://code.claude.com/docs/en/skills) · [Gemini CLI](https://geminicli.com/docs/cli/using-agent-skills/) · [ChatGPT Skills](https://help.openai.com/en/articles/20001066-skills-in-chatgpt) · [OpenAI Skills API](https://developers.openai.com/api/docs/guides/tools-skills) · [Codex](https://developers.openai.com/blog/skills-agents-sdk) · [DeepSeek Deep Code](https://api-docs.deepseek.com/quick_start/agent_integrations/deepcode/)

## How to evaluate

1. Provide a representative repository or a fixture from `references/skill-evaluation.md`.
2. Record the skill version, platform, model, project stack, scope, and relevant output.
3. Check evidence, finding/status/count consistency, severity rationale, and whether uninspected areas remain explicitly unknown.
4. Do not treat a recommendation as verified behavior. Confirm claims against source, tests, documentation, or authorized checks.
5. When a defect appears, add a regression fixture before changing the skill and rerun affected scenarios.

Architecture guidance is portable; commands, conventions, and static-analysis rules must match the detected stack. When evidence or ecosystem knowledge is missing, the agent should say so instead of inventing rules.

## Validation status

- **Structure:** `quick_validate.py` passed with Python 3.11 and PyYAML 6.0.3 in the prior validation run.
- **Manual fixtures:** A–F passed a manual self-evaluation against their expected outcomes. This is not an independent multi-model/platform evaluation.
- **Cursor field evaluation:** two runs on one TypeScript/MongoDB application improved finding counts, statuses, and optional-improvement classification. The second report still ambiguously offered MongoDB `bulkWrite` as an alternative to an atomic multi-document replacement. Fixture G therefore **partially passes**; see [the evaluation criteria](references/skill-evaluation.md).

## Versioning

This repository distributes instructions and references rather than a runtime package. Releases are identified by Git tags and GitHub Releases; the skill itself has no executable version field.

Use Semantic Versioning with prerelease identifiers:

- `v0.1.0-alpha.1`: first public alpha.
- `v0.1.0-alpha.2`, `v0.1.0-alpha.3`: subsequent alpha feedback and fixes.
- `v0.1.0-beta.1`: feature set is stable enough for broader validation.
- `v1.0.0`: intended workflow and compatibility claims have acceptance criteria and have been validated sufficiently for a stable release.

For each release, update `CHANGELOG.md`, create an annotated tag on the reviewed commit, and publish matching notes as a GitHub prerelease until `v1.0.0`.

## Contributing

Use the [contribution guide](CONTRIBUTING.md). Please do not include proprietary source code, credentials, customer data, or other sensitive project information in public audit feedback.
