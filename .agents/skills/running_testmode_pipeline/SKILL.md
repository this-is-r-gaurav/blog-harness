---
name: running-testmode-pipeline
description: |
  Execute the end-to-end blogging pipeline locally in TEST_MODE using fake LLMs, mock tools, and in-memory services. Use this skill when verifying multi-agent orchestration, validating dependency injection wiring, or gating code changes before shipping.
  Do NOT use for deploying to live GCP environments or invoking real AI provider endpoints.
version: 1.0.0
allowed-tools: Read Bash
metadata:
  author: this-is-r-gaurav
---

# Running Test-Mode Pipeline

## When to use

- Running the complete multi-agent pipeline locally without triggering real LLM API calls or cloud costs.
- Verifying Conductor orchestration, specialist agent transitions, and Manager mediation offline.
- Gating and testing application or pipeline modifications before attempting any GCP path wiring or commits.

## When NOT to use

- Testing against live LLM models or production GCP cloud services and real infrastructure.
- Running isolated unit tests or single syntax linters (prefer focused `pytest` or ruff commands instead).

## Workflow

1. **Verify DI profile wiring**: Verify that the `TEST_MODE` configuration profile and dependency injection container are configured to use in-memory adapters and mock tools without environment branching in app code (§2.4).
2. **Execute pipeline**: Launch the test-mode runner from the project root by executing `make test-mode`.
3. **Inspect convergence and logs**: Monitor the terminal execution to confirm the Conductor orchestrates all specialist steps to completion using fake LLM responses and structured envelope exchanges.
4. **Check guardrails**: Ensure no network calls or external cloud dependencies fail during execution.

## Examples

- Input: "Verify that our changes to the SEO structurer don't break the local pipeline." → Output: Executes `make test-mode` and confirms end-to-end multi-agent convergence with mock services.

## Output format

- Console execution log demonstrating successful offline multi-agent pipeline convergence and green test verification.

## Anti-patterns to avoid

- Don't add conditional environment branching (`if env == 'test': ...`) inside specialist or application code; all behavioral differences must live strictly in DI wiring (§2.4).
- Don't attempt to wire or test live GCP cloud paths until `TEST_MODE` is confirmed green and passing locally.
- Don't ignore pipeline escalation warnings or mock schema validation errors during offline test runs.
