---
name: add-eval-case
description: Procedure for creating a new deterministic evaluation case and fake LLM fixture for CI.
---

# Add eval case
1. Create a fake LLM fixture that triggers the desired behavior (e.g. convergence, blocking error, escalation).
2. Write a deterministic `EvalCase` targeting the test scenario.
3. Wire the evaluation into Tier-0 (so it runs every commit).
4. Run `make eval-tier0` to ensure it passes.
