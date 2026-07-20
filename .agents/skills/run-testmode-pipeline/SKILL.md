---
name: run-testmode-pipeline
description: Procedure for running the complete blogging pipeline locally using the fake LLM in TEST_MODE.
---

# Run testmode pipeline
1. Ensure the `TEST_MODE` profile is injected correctly (via DI).
2. Run `make test-mode`.
3. Verify that the complete end-to-end pipeline executes locally with the fake LLM, mock tools, and in-memory services.
