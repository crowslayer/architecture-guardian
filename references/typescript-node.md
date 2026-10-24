# TypeScript and Node.js

Read this reference only when the inspected project uses TypeScript and/or
Node.js. Apply TypeScript-specific checks only to TypeScript code and runtime
checks only to Node.js. It supplements the language-agnostic architecture
guidance; it does not define requirements for other stacks.

Inspect the actual runtime, module system, tsconfig, package manager,
and framework before making recommendations.

Check:

- Strict typing and unsafe any usage.
- Correct null and undefined handling.
- Narrowing and validation of untrusted input.
- Clear separation of domain types and transport/database DTOs.
- Explicit error contracts and preservation of error causes.
- Unnecessary framework dependencies in domain modules.
- ESM/CommonJS compatibility and import conventions.
- Resource cleanup, transaction boundaries, and async error handling.
- Circular imports and excessive module coupling.

Do not use `any` as a shortcut when `unknown` and validation are
appropriate. Do not add wrappers around every primitive or function.

Avoid recommending a specific framework, ORM, or validation library
without understanding the existing stack.

Do not alter compiler settings globally merely to silence errors.
When enabling stricter options in a legacy codebase, propose a staged
migration and identify likely compatibility issues.

## Dependency graph checks

Prefer an existing project command for dependency-cruiser. If the tool and
configuration are already present but no command is defined, discover the
actual source and config paths and recommend a direct invocation such as
`depcruise <source-paths> --config <config> --output-type err`. Do not add a
wrapper script or install the tool. If unavailable, inspect imports manually
and report that automated graph validation was unavailable.
