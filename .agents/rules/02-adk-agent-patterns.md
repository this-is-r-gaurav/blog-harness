# ADK agent patterns
- TOOL-USING specialist = two-node worker→structurer `SequentialAgent` (§3). `output_schema`
  lives on the STRUCTURER only; the worker carries tools and NO `output_schema`.
- TOOL-FREE specialist (Synthesizer) = single `output_schema` node.
- One logical specialist = one Agent Card, one §7 envelope/hop (payload = structurer output),
  one row in the §9.1 "11 specialists". The internal split is invisible to Conductor/Manager.
- LOOP EXIT: `LoopAgent` has NO predicate hook. Exit = a deterministic `BaseAgent` checker,
  appended as the LAST sub-agent inside the LoopAgent, sets `ctx.actions.escalate = True`. NO model call. (§4.4/§4.6)
- Escalate must exit the loop WITHOUT halting the parent SequentialAgent — see M0 spike T-M0.5. (§4.6 caveat)
