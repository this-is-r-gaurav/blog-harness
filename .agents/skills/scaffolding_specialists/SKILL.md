---
name: scaffolding-specialists
description: |
  Scaffold new specialist agent projects, wire uv workspace membership, and configure two-node worker-structurer architecture. Use this skill when creating a new specialist service, configuring blog_agent_kit wrappers, or setting up agent test suites.
  Do NOT use for creating reusable workflow procedures, helper scripts, or modifying Conductor loop checkers.
version: 1.0.0
allowed-tools: Write Read Bash
metadata:
  author: this-is-r-gaurav
---

# Scaffolding Specialists

## When to use

- Creating a new specialist agent project under `services/specialists/` adhering to single-agent-per-project structure (§14).
- Configuring a tool-using specialist into the standardized two-node worker→structurer unit via `blog_agent_kit.build()` (§3).
- Wiring a new specialist service into root uv workspace dependency tracking and Tier-0 evaluations.

## When NOT to use

- Designing reusable development skills or standalone documentation guidelines (use `creating-skills` instead).
- Authoring deterministic loop exit checkers or orchestration loops (use `adding-loop-exit-checkers` instead).
- Writing ad-hoc utility scripts or simple REST backend endpoints outside the agent pipeline.

## Workflow

1. **Scaffold agent directory**: Execute `cd services/specialists && agents-cli create <name>` to generate the single-agent-per-project directory structure (§14).
2. **Register uv workspace member**: Add `services/specialists/<name>` to the root workspace members array in `/pyproject.toml`.
3. **Declare core agent logic**: In `app/agent.py`, DECLARE only: instructions, `output_schema` (importing a validated `blog_contracts` model), tool list, and input contract. Do NOT hand-roll authentication, observability, or HTTP serving code (§14 DRY rule).
4. **Wrap with blog_agent_kit**: Wrap the agent declaration using `blog_agent_kit.build()`, which automatically expands tool-using specialists into the two-node worker→structurer unit (§3) and attaches observability, auth, and schema binding.
5. **Add evaluation dataset**: Create a test suite under `tests/eval/` complete with a deterministic `EvalCase` and fake-LLM fixture (refer to skill `adding-eval-cases`).
6. **Gate verification**: Verify the build by confirming schema-conformance evaluations pass and `make test-mode` succeeds cleanly.

## Examples

- Input: "Create a new image optimization specialist agent." → Output: Scaffolds `services/specialists/image_optimizer`, registers it in `pyproject.toml`, declares contracts and tools wrapped with `blog_agent_kit.build()`, and creates eval fixtures.

## Output format

- Standardized specialist project directory under `services/specialists/<name>` with uv workspace registration, declarative agent wiring, and deterministic evaluation datasets.

## Anti-patterns to avoid

- Don't hand-roll custom authentication, observability tracing, or FastAPI serving servers inside specialist code; rely strictly on `blog_agent_kit` wrapper injection (§14 DRY rule).
- Don't bypass the two-node worker→structurer pattern for tool-using agents (§3).
- Don't allow specialist agents to invoke or communicate directly with peer specialists; all orchestration must flow centrally through the Conductor (§1.2.3/§2.3.1).
- Don't ship a specialist without deterministic eval fixtures and a green `make test-mode` verification run.
