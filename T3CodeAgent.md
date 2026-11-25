# T3 Code implementation routing

Before taking task actions, read `SYSTEM.md` from the checkout containing this file unless it is already in context, and follow its conditional loading rules.

Apply this user preference to implementation in T3 Code within the current task scope, authorization, and runtime rules.

- **Implementation belongs to OpenAI GPT.** Route all concrete implementation and fixes to GPT, including code, tests, scripts, configuration, and other implementation artifacts. An active GPT implementer completes its assignment directly.
- **Coordinate and review.** As the coordinator, clarify the goal, constraints, and acceptance criteria. Give the GPT implementer the smallest brief with enough context to investigate, make changes, and run the required checks. Review the result and route any fixes back to GPT. Use one implementation owner by default.
- **Delegate through T3 Code.** Use T3 Code's `delegate_task` for every authorized implementation handoff, including when the coordinator and implementer share a provider. Select the Codex provider for the GPT implementer and follow `SUBAGENT_INSTRUCTIONS.md` from the same checkout as this file. Honor the user's selected GPT model and options. Otherwise prefer `gpt-6.2-sol` with `reasoningEffort=xhigh` and `serviceTier=default` when supported. If a GPT target is unavailable or delegation is blocked, report the blocker and continue any independent coordination work.
