# AGENTS.md — start here

## What this is (one paragraph)
An autonomous, human-in-the-loop pipeline that turns a plain-text idea into a
media-rich, SEO-optimized blog (single post or series), produced by 11 specialist
agents orchestrated by one Conductor, mediated by one Manager, on Google ADK + GCP.

## The 5 invariants you must never break (full list: .agents/rules/00)
1. Bounded refinement — every loop is a LoopAgent with max_iterations. (PDD §1.2.1)
2. Structured everything — every hop is a §7 envelope; exits read typed fields. (§1.2.2)
3. Centralized mediation — specialists never call each other; only the Conductor. (§1.2.3/§2.3.1)
4. Contracts are shared — import blog_contracts; never redefine a schema. (§2.3.2)
5. No env branching in app/agent code — differences live only in DI wiring. (§2.4)

## Core architecture map
Conductor (ADK SequentialAgent of Loop/Parallel blocks)  →  11 specialists
Manager = callbacks on every node (guardrail + log + tool-cache), NOT a proxy (§6.2)
Optimizer = offline job over the episodic log (§8)
Two-node build: tool-using specialist = worker(tools)→structurer(output_schema) (§3)
Loop exit = deterministic BaseAgent checker sets escalate; LoopAgent has no predicate (§4.4/§4.6)

## Where to look
| Need | Go to |
|---|---|
| Design authority (the "why") | PDD.md |
| Build runbook (the "how/when") | IMPLEMENTATION_PLAN.md |
| Always-on invariants | .agents/rules/ |
| Repeatable procedures | .agents/skills/ |
| What was built + lessons per task | notes/ (chronological, one file per task) |
| Contracts (single source of truth) | packages/blog_contracts/ |

## Build & test
make dev | make test-mode | make eval-tier0    (full list: IMPLEMENTATION_PLAN.md Appendix A)

## The one rule that keeps everything working
Keep TEST_MODE green before wiring any GCP path. No task ships without its notes/ closeout note.
