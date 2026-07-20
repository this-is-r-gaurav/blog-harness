# Testing and evals
1. TEST_MODE STAYS GREEN — Ensure `TEST_MODE` stays green at all times.
   CHECK: CI must fail if `TEST_MODE` breaks.
2. DETERMINISTIC-FIRST — Prioritize deterministic evaluations.
   CHECK: Review evaluation suites to ensure deterministic approaches are heavily favored.
3. TIER-0 EVERY COMMIT — Tier-0 evaluations must run on every commit. (§13.6)
   CHECK: Verify CI pipelines execute Tier-0 evaluation.
