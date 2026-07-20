# Manager guardrail
1. FLAG + LOG BELOW HIGH-CONFIDENCE — Any structural injection detected without high confidence should only be flagged and logged, not stripped.
   CHECK: Ensure manager logic adheres to confidence thresholds.
2. STRIP ONLY HIGH-CONFIDENCE STRUCTURAL INJECTION — Only strip high-confidence structural injection.
   CHECK: Verify redaction logic tests for this.
3. NEVER STRIP READER-FACING QUOTED TEXT — Do not alter quotes or reader-facing prose. (O-6, §6.3)
   CHECK: Verify via eval suites.
