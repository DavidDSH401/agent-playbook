# Issue tracker: GitHub

Use the GitHub repository designated for the task. If none is specified, identify the intended tracker from the checkout's remotes and fork relationship.
Use the gh CLI with `--repo OWNER/REPO` after verifying the target.

## Operations

- Read issues with gh issue view, including relevant comments and labels.
- Create issues with a specific title and --body-file for multiline text.
- Apply or remove the labels defined in triage-labels.md.
- Confirm a required explanation was posted before closing an issue.
- If a write times out, check whether it succeeded before retrying.

Use native GitHub sub-issues and dependencies when available.
Otherwise record `Part of #<parent>` and `Blocked by: #<number>` explicitly.
Use the installed CLI's documented syntax or the GitHub API rather than
assuming version-specific flags.

## Pull requests as a triage surface

**PRs as a request surface: no.**

## Skill instructions

"Publish to the issue tracker" means create a GitHub issue here.
"Fetch the relevant ticket" means read the issue and relevant discussion.

For wayfinding, use a map issue labelled `wayfinder:map` and linked child
issues. Record ticket type with `wayfinder:<type>`. Check that the labels exist and
create missing labels only when authorized. Select an unassigned,
unblocked child before claiming work; record the outcome before closing it.

Tracker configuration does not require creating tickets for routine edits.
Follow SYSTEM.md and GIT.md for task scope, authorization, and delivery.
