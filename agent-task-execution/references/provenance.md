# Source and design decisions

Inspected reference: `skills/create-task-tickets/SKILL.md` in the supplied repository. Preserved intent fidelity, exact identifiers, observable criteria, scoped questions, and implementation freedom. Adapted its human-developer tickets into self-contained internal execution records. Unlike its tracker output, this protocol maintains a local board and separate requirements/evaluation files. Independent deliverables can be split even when integration later depends on them; shared-file collisions are managed explicitly.

The user's supplied video notes describe a router with isolated workers, rd.md/eval.md tickets, a task board, optional watchdog, merger/checker/tester/reproducer roles, and subagent fallback. Those architectural ideas inform this package. The video itself and its reported timing/model comparisons were not independently verified; no performance claim or DeepSeek product requirement is made here.

The notes' provider-specific models, commands, auto permission mode, cloud runtime, fixed watchdog interval, and browser tool are intentionally optional. Out-of-scope bug fixing described in the notes does not enlarge a user's authorization. Solo means one executor, which may be the current agent or a delegated worker; it does not require subagents.

This package provides instructions and file contracts, not an autonomous background daemon, distributed queue, or provider integration. Readiness and evidence checks are performed by the agent; native discovery, concurrent execution, persistent workers, and browser tools depend on the host. A syntactically valid board never proves an implementation correct.
