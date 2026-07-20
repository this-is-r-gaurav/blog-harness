---
name: adding-loop-exit-checkers
description: |
  Implement deterministic loop exit checkers to terminate LoopAgents in bounded refinement cycles without model calls. Use this skill when designing loop exit rules, setting escalation thresholds, or asserting convergence conditions in iterative pipelines.
  Do NOT use for creating tool-using specialist agents or implementing LLM-driven decision predicates.
version: 1.0.0
allowed-tools: Write Read Bash
metadata:
  author: this-is-r-gaurav
---

# Adding Loop Exit Checkers

## When to use

- Designing a deterministic exit condition to stop an iterative `LoopAgent`.
- Enforcing bounded refinement thresholds or convergence checks in orchestration blocks.
- Escalating execution out of a loop when iteration limits or failure criteria are reached.

## When NOT to use

- Building tool-using specialist agents or general sequential workflow nodes.
- Writing probabilistic or model-dependent evaluation criteria for control flow.

## Workflow

1. **Subclass BaseAgent**: Create a Python class inheriting directly from `BaseAgent`.
2. **Implement deterministic checks**: Write purely deterministic verification logic without making any model or external API calls.
3. **Inspect state**: Read existing session state and typed envelope payload values directly from `ctx`.
4. **Handle exit or escalation**: To terminate the loop and escalate, set `ctx.actions.escalate = True`.
5. **Set output contracts**: Ensure the checker explicitly sets required typed fields on the context or output schema.
6. **Verify with assertions**: Write unit tests and eval fixtures using deterministic assertions to prove exit behavior.

## Examples

- Input: "Create a loop exit checker that stops iteration once the content validation score hits 1.0 or 3 iterations are reached." → Output: Creates a `BaseAgent` subclass checking `ctx` for the iteration count and score, setting `ctx.actions.escalate = True` when conditions are met.

## Output format

- Python module defining a `BaseAgent` subclass with deterministic logic and associated deterministic evaluation tests.

## Anti-patterns to avoid

- Don't make LLM calls or network requests inside a loop exit checker; exit evaluations must remain purely deterministic (PDD §4.4/§4.6).
- Don't rely on untyped dictionaries or ad-hoc strings for state check exits; always read and write structured schema fields (§1.2.2).
- Don't create unbounded refinement loops without an unconditional hard termination fallback (§1.2.1).
