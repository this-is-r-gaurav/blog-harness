---
name: creating-skills
description: |
  Construct new modular skills adhering to established naming, routing, and portability standards. Use this skill when building new procedures, defining standardized domain capabilities, or refactoring existing skill structures.
  Do NOT use for creating application scripts, complex subagents, or multi-purpose utility bundles.
version: 1.0.0
allowed-tools: Write Read
metadata:
  author: this-is-r-gaurav
---

# Creating Skills

## When to use

- Designing a brand new skill folder under `.agents/skills/<directory_name>/`.
- Standardizing a domain-specific capability or repeatable workflow into a reusable, portable asset.
- Refactoring existing skills to adhere to single-responsibility and routing best practices.

## When NOT to use

- Building specialist subagents or modifying orchestration configurations (use `scaffolding-specialists` instead).
- Creating miscellaneous code helpers, general utility scripts, or temporary workspace files.
- Bundling multiple unrelated workflows into a single tool.

## Workflow

1. **Decompose the scope**: Ensure the workflow handles exactly one focused objective that can be summarized in a single sentence. If it spans multiple responsibilities, separate it into distinct skills.
2. **Determine naming**:
   - Use `snake_case` for the directory name under `.agents/skills/` (e.g., `.agents/skills/processing_pdfs/`).
   - Use `kebab-case` in the YAML `name` attribute, preferring gerund phrasing (e.g., `processing-pdfs`).
   - Eliminate vendor prefixes, generic labels (e.g., `utils`, `helpers`), and obscure internal acronyms.
3. **Draft the routing description**:
   - Treat the YAML description as a critical API interface for agent routing decisions.
   - Begin immediately with strong action verbs and explicit trigger phrases rather than passive filler ("Analyze logs when...", not "This skill helps you with...").
   - Add definitive out-of-scope conditions ("Do NOT use for...") to prevent mistaken triggers.
   - Keep it impactful and concise (ideally around 50 words, well within parser token limits).
4. **Scaffold the structure**: Create `<skill_dir>/SKILL.md` using `assets/template.md` as your structural blueprint. Add supplementary folders (`scripts/`, `assets/`, or `references/`) only when necessary.
5. **Ensure portability and reliability**:
   - Keep instructions agnostic of any specific AI engine or runtime implementation so the skill remains universally portable.
   - Maintain semantic versioning in the YAML frontmatter and treat skills as engineered libraries.
   - Add verification methods, eval cases, or tests; ensure skills go through standard PR reviews and domain specialist ownership.

## Examples

- Input: "Create a skill for compressing and archiving build output directories." → Output: Scaffolds `.agents/skills/archiving_builds/SKILL.md` with the YAML name set to `archiving-builds`.

## Output format

- Follow the baseline structure in `assets/template.md` for generating all new skills.

## Anti-patterns to avoid

- Don't write broad descriptions or passive intros; vague summaries lead to under-triggering or improper routing.
- Don't bundle multiple capabilities into one large skill; enforce single-responsibility boundaries.
- Don't couple instructions to proprietary agent runtimes or vendor-specific features.
- Don't bypass formal testing and PR review; skills are foundational dependencies within the agent pipeline.
