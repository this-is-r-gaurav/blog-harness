# Python uv workspace
1. UV WORKSPACE MEMBERS & NAMING — All packages and services must be part of the single `uv` workspace. The workspace root `pyproject.toml` should explicitly list package and service directories (e.g., `services/conductor`, `services/specialists/*`) rather than blind globs like `services/*` to avoid matching container directories. Furthermore, package distribution names in `pyproject.toml` must align with module directory names under `src/` for `uv_build` (e.g., `name = "bff"` for `src/bff/`).
   CHECK: Check `[tool.uv.workspace] members` in root `pyproject.toml` and verify package names match `src/` module folders.
2. IMPORT DIRECTION — Top-level components like Conductor or Manager can import packages (`blog_contracts`, etc.) and specialists, but packages must not import services. Specialists must not import each other.
   CHECK: Review imports. No cycles.
3. EACH SPECIALIST OWNS ITS DEPENDENCIES — Each specialist has its own `pyproject.toml` (and `uv.lock` if appropriate) for isolated dependencies. (§14)
   CHECK: Ensure each directory under `services/specialists` has a `pyproject.toml`.
