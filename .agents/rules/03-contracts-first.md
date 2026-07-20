# Contracts first
1. SINGLE SOURCE OF TRUTH — All payload schemas are defined in `blog_contracts`. No service redefines a payload schema.
   CHECK: Ensure all models are imported from `blog_contracts` instead of being redefined locally.
2. BUMP SCHEMA VERSION — Any breaking change requires bumping the `SCHEMA_VERSION` in `blog_contracts`.
   CHECK: Review breaking changes for a version bump.
3. REJECT UNKNOWN VERSIONS — Manager must reject unknown versions. (§6.6)
   CHECK: Verify Manager's validation logic includes a check for known schema versions.
