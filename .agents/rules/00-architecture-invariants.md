# Architecture invariants (non-negotiable)
1. BOUNDED REFINEMENT — every agent-to-agent loop is an ADK `LoopAgent` with an explicit
   `max_iterations`. No `while True`, no unbounded recursion. (§1.2.1)
   CHECK: grep for LoopAgent → every instance passes max_iterations; no hand-rolled agent loops.
2. STRUCTURED EVERYTHING — every hop is a §7 envelope; loop exits read typed fields
   (`approved`, `position_shift`), never free-text. (§1.2.2)
   CHECK: no exit checker parses model prose; all read Pydantic fields.
3. CENTRALIZED MEDIATION — leaf specialists never import or call each other. Only the
   Conductor dispatches. (§1.2.3, §2.3.1)
   CHECK: import-linter contract — `services.specialists.*` may not import each other.
4. CONTRACTS ARE SHARED — no service redefines a payload schema; all import `blog_contracts`. (§2.3.2)
5. CONDUCTOR IS STATELESS between requests except via the Working-State store. (§2.3.3)
6. NO ENV BRANCHING in app/agent code — environment differences live only in DI wiring. (§2.4)
