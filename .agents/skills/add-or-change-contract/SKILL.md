---
name: add-or-change-contract
description: Procedure for adding or modifying a Pydantic model contract for inter-agent communication.
---

# Procedure: Add or modify a contract
1. Modify or add the Pydantic v2 model in `packages/blog_contracts/src/blog_contracts/models.py` (or corresponding module).
2. All models must be imported from `blog_contracts`, never redefined in service code (§2.3.2).
3. Ensure Pydantic field types and validation (e.g. enum validation, field limits, cardinality checks) accurately represent PDD §7 and §13 specifications.
4. If a breaking change is made to an existing contract, bump `SCHEMA_VERSION` in `packages/blog_contracts/src/blog_contracts/__init__.py`.
5. Update or add corresponding tests and eval fixtures in `packages/blog_evals` or `tests/`.
6. Run `make eval-tier0` or `pytest` on `blog_contracts` to confirm contract conformance round-trips cleanly.
