---
name: agent-task-execution
description: Specify and execute actionable work through file-based tickets, dependency-aware coordination, and evidence-backed evaluation. Use for agent-native task execution or maintaining an internal task board; not external issue-tracker integration.
---

# Agent Task Execution

Use `tasks/<ticket-id>/rd.md` as the outcome specification and `eval.md` as the independent completion contract. Keep status in `tasks/board.json` and execution evidence in each ticket's `run.md`. Paths are relative to the user's project, not this skill. Never modify the supplied examples as a live board.

## Intake and specification

1. Read the request, applicable project instructions, relevant code, tests, and supplied references before specifying work. Preserve exact identifiers and separate observations from hypotheses. Do not invent scope, user decisions, owners, dates, metrics, or technical causes.
2. Reuse a matching existing ticket instead of duplicating it. Allocate stable unique IDs under a single board writer. Size tickets to independently verifiable deliverables; keep a simple change in one ticket. A complex feature may need a specification worker before implementation tickets can be made Ready.
3. Copy [rd.md](assets/rd.md), [eval.md](assets/eval.md), and [run.md](assets/run.md) into each new ticket directory. Replace prompts with facts; omit irrelevant optional sections. A tiny change may need only a few requirements and checks. Give requirements `R1…` and criteria `E1…`; every requirement needs mandatory verification, and each mandatory check must trace to a requirement or stated constraint.
4. Validate the pair: an agent without this chat can understand the result, locate references, and perform each check. Record unresolved material questions and block only affected work. Investigations can be Ready with an unknown cause when their evidence and stopping condition are clear. Do not guess product decisions to unblock implementation.
5. Register the ticket using [board and dependencies](references/board.md). Draft means execution is not yet authorized. An existing request to implement authorizes moving to Ready when clear; do not ask for approval again. A request to draft tickets alone does not authorize implementation.

## Execute, evaluate, complete

Read [execution protocol](references/execution.md) before running or resuming a ticket. Claim only Ready tickets with satisfied dependencies. Read both specification files and record ownership before work. Keep modifications in scope and log decisions, changed files, checks, and failures in `run.md`.

Move to Review when implementation is ready for evaluation. Run the mandatory checks from `eval.md`; writing code, unchecked checkboxes, and worker confidence are not evidence. Repair failures and repeat affected verification. Never erase earlier failures. Mark Done only when each mandatory check passes against the final artifact or has an explicit, scoped exception approved by the user. Missing tools or inaccessible environments leave verification pending and the ticket Blocked, not Done. Preserve unmet outcomes in the completion report even when waived.

## Choose capabilities, not providers

Read [coordination](references/coordination.md) for routing, workers, teams, isolation, and fallback. Inspect actual available tools and permissions; do not infer capabilities from a model name. Default to Solo. Team is useful for independently scoped parallel work only when tools and authorization permit it. With no delegation, execute sequentially and record that fallback. A dedicated router coordinates and reviews; it never implements worker deliverables. In a single-agent environment there is no dedicated router: the executor performs the same lifecycle serially.

The portable protocol requires only reading and writing text files. If persistent files are unavailable, return a clearly labeled file bundle and a board snapshot for the user to save; do not claim it was persisted. Optional platform adapters may map tool calls, never change completion rules or require cloud services, provider-specific commands, permission bypasses, or particular models.

## Reference and usage

- Start: “Use this skill to fix the mobile navigation in this project.”
- Resume: “Execute ticket-003 from tasks/board.json and verify its eval.md.”
- Coordinate: “Route the Ready tickets using the available workers.”
- Load [examples](references/examples.md) for a complete dependency graph and realistic tickets.
- Load [validation scenarios](tests/scenarios.md) when testing or adapting the skill.
- See [validation results](tests/validation-results.md) for tested behavior and limits.
- Read [design provenance](references/provenance.md) for source choices and portability limits.

For Codex, place this folder in its configured skill directory. For other agents, expose SKILL.md as custom instructions and preserve its relative resources; native skill discovery and invocation syntax vary. This package is repository-local until installed. No provider adapter is required.
