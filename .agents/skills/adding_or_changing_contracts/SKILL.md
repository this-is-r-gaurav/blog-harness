---
name: adding-or-changing-contracts
description: |
  Add or modify shared Pydantic v2 model contracts for inter-agent communication within the blog_contracts package. Use this skill when defining structured envelopes, updating schemas for specialist input/output, or bumping contract schema versions.
  Do NOT use for defining ad-hoc local data classes in application or service code.
version: 1.0.0
allowed-tools: Write Read Bash
metadata:
  author: this-is-r-gaurav
---

# Adding or Changing Contracts

## When to use

- Defining a new Pydantic model for structured inter-agent communication or envelope messaging.
- Updating field types, validation constraints, or enums on an existing schema in `blog_contracts`.
- Bumping the shared `SCHEMA_VERSION` when making breaking alterations to pipeline data structures.

## When NOT to use

- Creating localized utility data structures or private helper classes within standalone scripts.
- Redefining or duplicating schema models directly inside specialist agent or service app code.

## Workflow

1. **Edit model definitions**: Add or update Pydantic v2 models in `packages/blog_contracts/src/blog_contracts/models.py` (or the appropriate subdomain module).
2. **Enforce shared import rule**: Verify that all consuming agent and service modules import directly from `blog_contracts`; never redefine models in service code (§2.3.2).
3. **Validate field constraints**: Apply accurate field typing and Pydantic validators (e.g., enum validation, length limits, cardinality checks) aligning with PDD §7 and §13 specifications.
4. **Manage versioning**: If a breaking modification is made to an existing contract, increment `SCHEMA_VERSION` in `packages/blog_contracts/src/blog_contracts/__init__.py`.
5. **Update dependent evals**: Synchronize corresponding test fixtures and eval datasets in `packages/blog_evals` or `tests/`.
6. **Verify conformance**: Run `make eval-tier0` or run `pytest` on `blog_contracts` to confirm schema validation and serialization round-trips succeed cleanly.

## Examples

- Input: "Add a word_count integer field with a minimum value of 100 to the BlogDraft contract." → Output: Updates `BlogDraft` in `models.py` with `Field(..., ge=100)`, increments `SCHEMA_VERSION` if breaking, updates affected fixtures, and executes tests.

## Output format

- Validated Pydantic v2 model definitions in `packages/blog_contracts`, synchronized eval fixtures, and passing Tier-0 conformance tests.

## Anti-patterns to avoid

- Don't define or duplicate schema contracts inside specialist service directories or application code; single source of truth resides solely in `blog_contracts` (§2.3.2).
- Don't alter existing contract fields silently without assessing breaking impacts and updating `SCHEMA_VERSION`.
- Don't skip updating test fixtures and running `make eval-tier0` when schema constraints change.
