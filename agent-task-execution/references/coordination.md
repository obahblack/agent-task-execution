# Capability-aware coordination

At intake, inspect the current environment for persistent file access, execution tools, browser access, delegation and messaging, concurrent jobs, worktree/sandbox isolation, and permission constraints. Record relevant capabilities in the active run, not guesses about provider names. Use only available, authorized operations.

| Available capability | Behavior |
| --- | --- |
| One agent only | Execute Ready tickets sequentially as Solo; no dedicated router. |
| Subagents, sequential only | Delegate a bounded ticket, collect result, then dispatch next. |
| Concurrent subagents and isolation | Run independent Solo tickets concurrently; use Team for a ticket with several coordinated work scopes. |
| Agent teams unavailable | Use bounded subagents for a Team ticket if available; otherwise record Team → Solo fallback and run sequentially. |
| No safe isolation | Serialize edits to shared files; parallel read-only investigation may still help. |
| No persistent sessions | Dispatch finite jobs, save handoffs and evidence, resume from files. |
| No browser or command runner | Perform available checks and mark unmet mandatory checks pending/Blocked. |

A router receives requests, reads the board, selects eligible tickets, assigns workers, monitors progress, reviews evidence, and escalates necessary decisions. It does not implement features. It may maintain coordination metadata. For complex intake, delegate specification work to a worker instead of turning the router into an implementation lead. A watchdog, merger, checker, tester, or bug reproducer is an optional worker responsibility, not a required always-on service.

Workers receive a ticket path, accessible references, explicit scope, work location/base revision, dependency artifact versions, and expected return evidence. Each reads rd.md and eval.md itself. Give each an isolated context; use isolated branches/worktrees when available, or non-overlapping scopes with serialized shared edits. Do not assume that separate context windows isolate files.

For a Team ticket, record work allocation and an integration owner in run.md. Avoid overlapping writers; return the combined result for ticket-level verification. Worker output includes changes, decisions, criterion results, evidence locations/revisions, blockers, and integration instructions. A worker's “done” message is not sufficient to move the board to Done.

Dispatch algorithm: validate graph → select authorized Ready tickets with satisfied dependencies → check resource/file conflicts → claim once → dispatch → consume progress/results → evaluate/integrate → update board → reconsider dependents. Never dispatch blocked or cancelled tickets. Do not start dependent work based on predicted completion.

Monitor through available job/status tools at natural checkpoints. An optional watchdog may inspect last progress, repeated failures, and circular waits; use scheduled polling only if actually supported and authorized. Do not assume a ten-minute service exists. Before stopping/reassigning a stale worker, inspect tool state and preserve its changes. On a suspected dependency deadlock, inspect and correct the graph or escalate the unresolved decision. Inbound user messages should reach the coordinator without making it take over worker implementation.

Platform adapters can map dispatch, status, isolation, browser, and integration to local tools. They must respect platform instructions and user permissions. Do not hardcode Claude commands, models, effort settings, automatic permission modes, Vercel tooling, or cloud residency.
