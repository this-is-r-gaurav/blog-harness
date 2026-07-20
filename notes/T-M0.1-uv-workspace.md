# T-M0.1 — Stand up the uv workspace monorepo
_2026-07-20 · outcome: DONE_

## What I did
- Scaffolded the core package skeletons (`blog_contracts`, `blog_platform`, `blog_observability`, `blog_agent_kit`, `blog_evals`) and service skeletons (`conductor`, `optimizer`, `bff`, `notification`) under standard `src/` layouts (§14).
- Configured root `pyproject.toml` workspace members and `[tool.uv.sources]` mappings with `{ workspace = true }`.
- Confirmed `uv sync` resolves cleanly and `import blog_contracts` works across root and member packages.

## Issues faced & how I fixed them
- Issue: `uv sync` failed with missing `pyproject.toml` in `services/specialists` → Cause: glob pattern `services/*` matched container directory `services/specialists` → Fix: listed specific service packages explicitly in root `pyproject.toml` members along with `services/specialists/*`.
- Issue: `uv_build` failed to build service packages → Cause: package names like `bff-service` expected `src/bff_service/__init__.py` instead of `src/bff/__init__.py` → Fix: aligned distribution names in service `pyproject.toml` files with their import module names (`conductor`, `optimizer`, `bff`, `notification`).

## Deviations from PDD / this plan
- None

## Rules / skills feedback
- ADD/CHANGE .agents/rules/01-python-uv-workspace.md: Note that workspace members in root `pyproject.toml` should list specific service directories rather than `services/*` to avoid matching container directories like `services/specialists`, and package distribution names must align with `src/` folder module names for `uv_build`.

## Follow-ups for later tasks
- T-M0.2 (`blog_contracts`) can now define Pydantic models cleanly on top of this scaffolded workspace structure.
