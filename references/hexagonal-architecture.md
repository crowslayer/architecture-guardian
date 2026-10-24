# Hexagonal and Clean Architecture

Use dependency direction and policy boundaries as the shared evaluation
criteria. These architectures use related ideas but do not require identical
layer names, folder structures, or diagrams. Map the project's own concepts
to business policy, application/use-case orchestration, delivery boundaries,
and infrastructure boundaries before judging it.

## Dependency rule

Business policy must not depend on delivery or infrastructure details
when the project intends to isolate its domain and application layers.

A typical dependency direction is:

Domain <- Application <- Inbound adapters / composition
Infrastructure implements application-owned output ports.

In Clean Architecture terminology, entities and use cases are commonly
inside framework, delivery, and persistence details. In Hexagonal Architecture,
the same boundary is often described through ports and adapters. Treat this as
a conceptual mapping, not a mandate to create a separate layer for every term.

The composition root may import concrete implementations and wire
them together. This is not a violation by itself.

Place a port in the innermost component that owns the need it represents.
Do not move a technical contract into the domain merely to make an import
graph look inward. Logging is usually an application/runtime concern or an
outer cross-cutting adapter; keep domain policy free of logging unless the
domain behavior itself requires an auditable business record.

## Review checklist

- Does domain code import HTTP, database, queue, or framework packages?
- Do use cases depend on concrete database clients?
- Are output ports owned by the application or domain layer as appropriate?
- Do inbound adapters translate external input into application requests?
- Do outbound adapters translate internal contracts into vendor APIs?
- Are persistence models leaking into domain invariants?
- Can domain tests run without starting external infrastructure?

## Findings

Report confirmed dependency violations with exact import evidence.

Do not require an interface for every class.
Introduce a port when it represents a meaningful boundary, a required
substitution, or a dependency inversion that improves the design.

Do not require one folder per layer if the project has another clear,
consistent modular structure.

## Refactoring guidance

1. Identify the policy currently coupled to infrastructure.
2. Define the smallest stable contract at the appropriate inner layer.
3. Implement the contract in an outer adapter.
4. Wire the concrete implementation at the composition root.
5. Test the policy independently and test the adapter at its boundary.
6. Verify the dependency graph and behavior.
