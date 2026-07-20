---
name: add-loop-exit-checker
description: Procedure for creating a deterministic loop exit checker in ADK to stop LoopAgents.
---

# Add loop exit checker
1. Create a subclass of `BaseAgent`.
2. Implement deterministic logic (no model calls) inside the checker.
3. Access context via `ctx`.
4. To exit the loop and escalate, set `ctx.actions.escalate = True`.
5. Ensure the checker sets typed fields on the context/output appropriately.
6. Test using deterministic assertions.
