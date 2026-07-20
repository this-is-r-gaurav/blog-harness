---
name: adding-eval-cases
description: |
  Create deterministic evaluation cases and fake LLM fixtures for continuous integration in Tier-0 evals. Use this skill when adding tests for newly scaffolded agents, validating contract conformance, or verifying pipeline convergence and error escalation behaviors.
  Do NOT use for general Unit testing of utility scripts or running end-to-end integration tests with live cloud endpoints.
version: 1.0.0
allowed-tools: Write Read Bash
metadata:
  author: this-is-r-gaurav
---

# Adding Eval Cases

## When to use

- Adding a deterministic evaluation case for a specialist agent or pipeline workflow.
- Creating a fake LLM fixture to simulate specific test scenarios (e.g., convergence, blocking error, escalation).
- Wiring a new eval case into Tier-0 CI execution.

## When NOT to use

- Writing standard pytest unit tests for utility functions or helper modules.
- Testing against live LLMs or external GCP cloud services.

## Workflow

1. **Create the fixture**: Create a fake LLM fixture that triggers the desired target behavior (such as convergence, blocking error, or loop escalation).
2. **Write the EvalCase**: Author a deterministic `EvalCase` targeting the specific test scenario and contract conformance.
3. **Wire into Tier-0**: Configure and wire the evaluation into Tier-0 so it automatically executes on every commit.
4. **Verify execution**: Run `make eval-tier0` via terminal to verify the evaluation executes and passes cleanly.

## Examples

- Input: "Add an eval case for the structurer node on schema validation failure." → Output: Creates a fake LLM fixture simulating an invalid schema response, authors an `EvalCase` asserting error handling or escalation, and verifies via `make eval-tier0`.

## Output format

- Deterministic `EvalCase` definitions and corresponding JSON/Python fake LLM fixture files wired into the Tier-0 evaluation suite.

## Anti-patterns to avoid

- Don't invoke live LLMs or make network calls within Tier-0 evaluation cases; all responses must be deterministically simulated via fake fixtures.
- Don't skip running `make eval-tier0` before submitting changes.
- Don't test multiple disparate scenarios within a single unstructured eval case; maintain granular, focused test objectives.
