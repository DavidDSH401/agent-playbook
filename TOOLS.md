# Tools, execution environments, and memory

Read SYSTEM.md first if it is not already loaded. Read the relevant section before the named operation. Discover current tools and skill locations from the active environment rather than caching a tool catalog here.

## Browser control

- **Automation scope.** Perform browser control only inside the tab group the user designates for automation, without disturbing the user's normal browser use. Do not select, activate, move, close, or navigate tabs outside that group, and leave the active tab and window focus unchanged.

1. Follow the active runtime's browser routing. Choose an available integration that can reach the requested browser, profile, and tab. Where OpenAI's browser integrations apply, use `cua_repl` in Codex to resolve a supplied tab reference or discover built-in Chromium (`iab`) and Chrome's `extension` connection. For a new task either can handle, prefer built-in Chromium.
2. If the applicable integrations cannot perform the task, report the limitation and use the registered `chrome-devtools` MCP when the runtime permits it and it can reach the requested browser and tab. Select the existing target tab when available. Report the blocker if no permitted connection works. Use the command below only for Codex MCP setup within the authorized task.

   ```bash
   codex mcp add chrome-devtools -- npx -y chrome-devtools-mcp@1.13.0 --autoConnect --no-usage-statistics --no-performance-crux
   ```

When diagnosing an absent extension connection, check the running browser, active profile, extension enablement, and native messaging host. For an authorized Linux extension installation check, set `CODEX_CHROMIUM_USER_DATA_DIR` to the actual user data directory for that invocation only. Confirm session connectivity in the browser inventory.

## Structural code exploration and Graphify

- For structural codebase exploration, use the installed `codebase-memory` skill when available. If indexing is available and no indexed graph project matches the repository, run `index_repository` before exploration. Use `search_graph`, `trace_path`, and `get_code_snippet` first; use direct source reads or grep for literals, configuration, verification, and whenever the tool or index is unavailable.
- Check index coverage for every file relied on as evidence. If coverage is incomplete or stale, inspect reported missed source lines directly and qualify conclusions. Scout results are provisional; use task-directed verification for material claims and bounded broader review for exhaustive or negative claims. Check pagination and use exact symbols before tracing paths.
- For `/graphify`, load the installed Graphify skill after the shared instructions and before graph work. Discover its current location and confirm project identity before using graph results.
- When graph or search coverage is insufficient, inspect direct source or other available evidence. Expand investigation when new information requires it; stop when evidence is sufficient to decide.

## Project execution environments

- Run project commands and tests locally by default. Use a remote execution environment only when the user explicitly assigns it for the current task.
- Follow the project's documented entrypoints and toolchain versions. Check versions in the execution environment.
- Do not copy credentials between environments. Follow task and project requirements for budget, identity, data scope, and formal acceptance.

## RTK

- If RTK is installed, follow its integration. Let an active rewrite hook handle supported commands; where no hook rewrites them, invoke `rtk <supported command>` directly. If RTK is unavailable, run the underlying command directly.
- Apply SYSTEM.md's evidence requirement to RTK output, including when a generated runtime guide calls the filtered output complete. Recover required details using the command's documented full-output option, such as `rtk git diff --no-compact`, or the installed version's documented bypass.
- Run RTK meta commands directly. Diagnose a missing or unusable binary with `rtk --version`, `command -v rtk`, and relevant installed help when needed. Do not assume hooks or compression worked without evidence, or run diagnostics on every task.

## Shared Hindsight standard

- Before changing Hindsight configuration, project identity, or knowledge organization, read the design document for the Hindsight deployment selected for the task.
- Use the bank and project-scoping rules configured for the current project. Preserve registered project identities, strict project filters, and document namespaces; reuse existing project folders at any depth.
- Use the MCP server, adapter, and lifecycle hooks documented for the active runtime and Hindsight installation. Do not register Hindsight tools or hooks twice for the same runtime.
- Keep credentials, databases, active sessions, and environment-specific backend/tunnel settings on their original machine. New long-lived MCP processes load changed modules; do not claim existing sessions reloaded without checking.
