# Observability mandatory
1. EVERY AGENT INSTALLS OBSERVABILITY — Every agent must install `blog_observability`.
   CHECK: Ensure `install_observability` or similar is called for all agents in the Conductor graph.
2. CORRELATION ID — A full correlation ID must be set. (§11.2)
   CHECK: Verify correlation ID is present in logs.
3. UNINSTRUMENTED IS DEPLOY-BLOCKER — Any uninstrumented service acts as a deploy-blocker. (§11.9)
   CHECK: Verify all services are fully instrumented before deployment.
