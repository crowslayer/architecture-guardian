# Architecture Principles

Evaluate SOLID, cohesion, coupling, encapsulation, and simplicity in context.

- SRP: identify unrelated reasons for a module to change.
- OCP: identify recurring changes that repeatedly require editing stable policy.
- LSP: detect implementations that violate their documented contracts.
- ISP: detect clients forced to depend on irrelevant operations.
- DIP: detect high-level policy coupled to volatile implementation details.
- High cohesion: keep closely related responsibilities together.
- Low coupling: minimize unnecessary knowledge between modules.
- Encapsulation: protect invariants and implementation details.

Do not report a violation based only on class size, method count,
inheritance, or the absence of an interface.

Before proposing an abstraction, identify at least two meaningful
responsibilities, implementations, or change scenarios it serves,
unless a concrete domain or testing requirement justifies it.

Prefer local, comprehensible designs over speculative extensibility.
