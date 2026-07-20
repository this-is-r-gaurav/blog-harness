---
name: scaffold-specialist
description: Procedure to create a new specialist agent in the project, wire it up to the workspace, and write basic tests.
---

# Scaffold a new specialist
1. `cd services/specialists && agents-cli create <name>`   # single-agent-per-project (§14)
2. Add `<name>` to the root uv workspace members in /pyproject.toml
3. In app/agent.py, DECLARE only: instruction(s), output_schema (a blog_contracts model),
   tool list, input contract. Do NOT hand-roll auth/observability/serving. (§14 DRY rule)
4. Wrap via blog_agent_kit.build(): expands tool-using specialists into the two-node
   worker→structurer unit (§3), installs observability + auth + output_schema binding.
5. Add tests/eval/ dataset (EvalCase + fake-LLM fixture — see skill add-eval-case).
6. Gate: `make test-mode` green; schema-conformance eval passes for this agent.
