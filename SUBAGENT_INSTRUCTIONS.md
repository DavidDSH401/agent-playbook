# Subagent selection and delegation

Read SYSTEM.md first if it is not already loaded. Apply this guide to already-authorized delegation. Current runtime routing and restrictions take precedence.

## Select configuration

Before selecting a provider, route, or history inheritance, verify the destination may receive the data. Share only necessary task material. Inherit full history only when needed and appropriate for the destination.

1. Honor explicit provider, model, effort, service tier, speed, budget, and assignment through related follow-ups until changed or out of scope.
2. Follow compatible project and skill requirements.
3. For open choices, weigh ambiguity, dependencies, context, tools, failure impact, and input/output volume. Minimize expected total cost subject to acceptance, counting context, retries, parent rework, and latency alongside token price.
4. Inherit suitable settings or use inheritance when overrides are unavailable. Clear unintended premium priority, fast mode, or excessive effort when supported.

Use economical fast settings for bounded tasks, general-purpose settings for ordinary implementation, debugging, or review, and stronger reasoning for complex or high-impact work. Choose the lowest adequate effort based on capability. Justify maximum effort with a concrete quality or failure-impact reason.

Use configured pricing or authoritative provider data. Qualify unknown prices and latency. Avoid invented savings or price rankings, speculative paid benchmarks, and duplicate agents for model comparisons. Budget for all children and retries, justify parallel cost, and record a brief rationale. Report material tradeoffs or requested details.

## Discover and apply actual capabilities

- Follow registered runtime documentation and the current catalog. In T3 Code, call `orchestrator_capabilities` before the first `delegate_task`, search for missing requested models, and refresh after relevant errors or provider changes as directed.
- Use exact catalog IDs for providers and models. Check supported effort, service tier, speed, context, and tool options per model. Apply exact values through documented structured fields, including max versus high, and use documented resets for incompatible inherited settings.
- Default to standard priority when available. Premium or fast mode requires a user requirement or meaningful deadline benefit at understood cost. Apply supported sampling, context, or output controls while preserving evidence and error handling.

## Route and brief the task

- Use a route supporting the required provider, model, settings, execution, and isolation. In T3 Code, cross-provider, explicit `delegate_task`, background, and orchestrator-managed checkout requests use `delegate_task` with `target.options`. Same-provider children may use native tools when supported with the required configuration, except T3 Code implementation handoffs governed by T3CodeAgent.md. Inherited options alone do not force T3 routing. Elsewhere use documented fields and inheritance. Report unsupported explicit requirements.
- Brief each child on goal, inputs, evidence, scope, file ownership, deliverable, acceptance, and constraints. Supply needed context and account for tool differences. For shared writes, identify concurrent work, preserve others' changes, and assign nonoverlapping ownership or coordinate dependencies.
- Before dispatch, follow [CONTEXTBRIDGE.md](CONTEXTBRIDGE.md) for the role prompts and shared record used to resolve questions, objections, and decisions.
- Define coverage slices and cross-slice checks before dispatch. For comparisons, fix common requirements and evaluation criteria before results and preserve independent outputs. Bind verification or measurement to the target revision and method. Report coverage gaps.
- Parallelize only independent tasks. The parent integrates evidence, resolves disagreements, and verifies the integrated result against requirements. If children are unavailable, separate execution from self-review and report the method.

## Verify, recover, and report

- Verify the executed provider, model, and options against the selection when exposed. A mismatch leaves the explicit requirement unmet. Report mismatches and unexposed settings. Labels or separate runs alone cannot establish distinct providers or model families.
- Retain task IDs separately from child thread IDs. Follow returned next actions and runtime completion, waiting, cancellation, and retry controls. Use required notifications without polling. Check uncertain launches before retrying.
- For unavailable explicit targets, inspect the catalog and error. Ask for an alternative only when it changes the requirement and continue independent work. For open choices, use supported equivalents and explain material substitutions.
- Diagnose authentication, quota, context, tool, and execution failures before blaming model quality. Respect denials and explicit selections. Retry only with a useful change. Reuse findings, narrow unresolved work, and increase supported effort or model capability within authorization and budget if needed. Stop at limits or concrete blockers and cancel unnecessary work.
- Report findings and label provider, model, and options as execution metadata. Follow SYSTEM.md for attribution.
