# Main Agent and Subagent context bridge

Use a task record for authorized delegation. The Main Agent maintains the business context as it evolves. Subagents use the same record to request missing information and read answers. Keep live records in authorized task storage and out of commits by default. Verify each destination may receive the information and share only what the task needs.

## Role prompts

Apply the Main Agent prompt when coordinating. Include the Subagent prompt in each task brief you send.

**Main Agent**

> When a Subagent raises a material choice they cannot resolve, evaluate the evidence, decide within the user's authorization, and give the rationale, plan, and concrete next step.

**Subagent**

> Decide routine, reversible details within your assignment. Verify material claims against the best available sources and raise evidence-backed objections when a material discrepancy remains. After checking the record and sources, ask the Main Agent for a decision or plan when material uncertainty blocks a dependent step.

## Main Agent

1. Before dispatch, prepare the task record with the business goal, relevant domain terms and rules, confirmed decisions, constraints, and acceptance criteria. Cite authoritative sources and label unresolved assumptions. If the task permits shared storage, use a path accessible across the relevant worktrees to authorized participants only. Give each Subagent the exact path or include the record in the authorized brief. Point to this guide or include its relevant instructions.
2. As new business details, decisions, or corrections emerge, append them promptly. Identify any earlier entry a correction supersedes. Notify affected Subagents of changes that affect their work through the runtime's available communication channel.
3. Review requests when notified, at coordination checkpoints, and before accepting a deliverable. Append an `Answer` with the matching request ID. Provide the confirmed fact and its source, or record the chosen option, rationale, and plan. Notify the requester. Keep the request open while evidence or required user input is pending. Use the ordinary clarification workflow when the user must decide or supply information.

## Subagent

1. Read the task record before starting, when notified of an update, and before resuming work that depended on an open request.
2. Check the record and your sources before raising a request. Append a `Request` with a task-unique ID formed from your assignment and a sequence number. State the question or objection, what you checked, and the decision or plan you need to proceed. If a matching request is open, refer to its ID. Notify the Main Agent, continue independent work, and pause the dependent step until the answer resolves the request.

## Shared record

Use Markdown headings `## Context <topic>` for business facts and decisions, `## Request <id>` for questions and objections, and `## Answer <id>` for confirmed facts and decisions. Append complete entries using a method that preserves concurrent writes. When shared writes are outside the task scope, unavailable, or unsafe, send the entry through the authorized runtime channel or return it in the handoff. The Main Agent records it where the task permits and relays relevant updates to Subagents without file access.
