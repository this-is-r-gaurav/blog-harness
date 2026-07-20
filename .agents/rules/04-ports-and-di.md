# Ports and DI
1. GCP ADAPTER + TEST_MODE FAKE — Implement one GCP adapter and one `TEST_MODE` fake per port.
   CHECK: Ensure every port has both implementations available.
2. DI FACTORY ONLY — The DI factory is the only place environment variables (like `TEST_MODE`) are read.
   CHECK: `grep -r "TEST_MODE"` should only yield results in the DI factory (and tests). No `if TEST_MODE:` allowed in app/agent code. (§2.4)
