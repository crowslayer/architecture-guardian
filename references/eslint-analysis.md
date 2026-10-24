# ESLint configuration analysis

Use this reference when ESLint is present, when the user shares an ESLint configuration, or when lint rules are used as evidence for architectural boundaries.

## Discover configurations without assuming a format

Identify the installed ESLint version, package manager/workspaces, lint scripts, and every configuration file that can apply to the target package and file. Support flat config (`eslint.config.js`, `.mjs`, `.cjs`, `.ts` where supported), legacy `.eslintrc*` formats, shared configs, and workspace/package-local configs. Do not infer the active config from a pasted file alone.

Inspect the actual config chain and how each entry applies: `files`, `ignores`, `extends`, plugins, parsers, parser options, settings/resolvers, rule severity/options, and overrides. In flat config, account for ordered config objects and matching patterns; in legacy config, account for `overrides`, `extends`, and directory resolution. Check whether the installed ESLint version supports the syntax and CLI options being used.

Recommend the repository's lint command and ESLint's effective-config output (`--print-config <representative-file>`; config inspector where available). Inspect representative files from relevant classes, such as production source, tests, command/query handlers, domain, adapters, and composition roots. Execute commands only under the authorization policy in `SKILL.md`. Do not claim an override applies without confirming that the file is included and not ignored.

## Read rules as evidence, not architecture

For each relevant rule, record its effective severity, target files, and actual protection. Distinguish:

- A diagnostic produced by ESLint from a manually inferred design concern.
- A configured rule from an effective rule applied to the file.
- A rule that detects a syntax/name heuristic from one that validates dependency semantics.
- A disabled rule, ignored file, unmatched override, missing plugin, resolver limitation, or unavailable type information from a passing architectural check.

Architecture rules from `boundaries`, `import`/`import-x`, `no-restricted-imports`, selectors, or custom plugins can be valuable. Verify their element/path definitions, aliases, resolver behavior, and test coverage. Name-based rules (for example `*QueryHandler.ts` or a call to `.save()`) can miss alternate names/APIs and can flag legitimate cases. Confirm findings in source and runtime paths before reporting them.

Check for contradictory or ineffective policy: a file matched by an override but excluded by `ignores`; broad ignores that omit production or test code; later flat-config entries overriding earlier rules; query rules that cover only one relative import depth; aliases not recognized by the resolver; dependency-cycle checks explicitly disabled; or boundary defaults that leave files unclassified. These are coverage risks to explain, not automatic proof of a code defect.

## Evaluate coverage and trade-offs

Summarize which architectural constraints are enforced, which are not enforced, and where enforcement is heuristic. Prefer source-level evidence for actual violations and tests for important boundaries. Do not require a particular plugin, parser, style guide, folder layout, or flat/legacy format.

Preserve the repository's conventions during refactors. Do not disable rules, widen ignores, or weaken type-aware linting merely to silence a diagnostic. If a rule conflicts with a valid design, explain the exact effective rule, consider a compliant implementation first, then propose the smallest scoped change with its trade-off and verification.
