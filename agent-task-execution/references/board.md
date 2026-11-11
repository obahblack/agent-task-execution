# Board and dependency contract

`tasks/board.json` is the sole status registry. `rd.md` and `eval.md` remain authoritative for requirements and verification. `run.md` holds history, not a second mutable status field. Use one coordinator as board writer; solo execution uses the executor. Workers report updates to that writer. For manual multi-session work, nominate a writer before editing; do not pretend file writes supply distributed locking. Write a complete valid JSON replacement atomically when the filesystem permits. Reconcile interrupted writes before dispatching more work.

```json
{
  "schema_version": 1,
  "tickets": [
    {
      "id": "ticket-001",
      "title": "Define the login API contract",
      "status": "Ready",
      "mode": "Solo",
      "assigned_agent": null,
      "path": "tasks/ticket-001",
      "depends_on": [],
      "blocker": null
    }
  ]
}
```

Required fields are shown. IDs and paths are unique, stable, project-relative; each path contains rd.md, eval.md, run.md. `assigned_agent` is an actual worker identifier or null; it conveys no invented person. `mode` is Solo (one executor) or Team (multiple collaborating executors). Several Solo tickets may run concurrently. `blocker` is null or a concrete reason and next action. Optional fields such as `updated_at` must contain actual recorded facts.

## Status transitions

- Draft → Ready: execution authorized, requirements/evaluation consistent, decisions resolved, dependencies satisfied.
- Draft/Ready → Blocked: a material question, unsatisfied dependency, or unavailable prerequisite prevents work. Record the reason.
- Ready → In Progress: prerequisites rechecked, worker claims ownership, work context recorded.
- In Progress → Review: deliverable prepared, ready to verify; this does not imply checks passed.
- Review → In Progress: an evaluation fails and repair can proceed. Retain failure evidence.
- Any active status → Blocked: progress needs input, tools, or dependencies; relinquish or explicitly retain assignment.
- Blocked → Draft: authorization still missing. Blocked → Ready: blocker resolved and authorized; resumed work claims again.
- Review → Done: every mandatory criterion has current pass evidence or an explicit user-approved exception.
- Done → Ready/Blocked: a reopened outcome or invalidated prerequisite requires rework; preserve history and invalidate affected dependent evidence.

Unassigned or crashed In Progress tickets do not automatically become safe to retry. Inspect their work and confirm no active worker before reassigning. Keep transition reasons and ownership changes in run.md. Do not drop a ticket to hide cancellation; record the user's cancellation and retain a Blocked ticket with “cancelled by user; no dispatch” unless the project explicitly extends the schema.

## Dependency edges

`depends_on` contains objects:

- Completion edge: `{"ticket":"ticket-001","condition":"done"}`. Satisfied only while that ticket is Done.
- Artifact edge: `{"ticket":"ticket-001","condition":"artifact","reference":"tasks/ticket-001/contract.md","version":"v1","criterion":"E1"}`. Satisfied only when the named artifact/version exists and its producing criterion has pass evidence for that version in run.md. A path existing alone is insufficient. A waiver does not silently satisfy an artifact edge; obtain an explicit revised dependency decision.

Reject missing ticket IDs, self-dependencies, and cycles before dispatch. Evaluate prerequisites transitively, including upstream invalidation. Prefer a small separate contract ticket when it makes coordination simpler. List ordering is not a dependency. Shared mutable files or incompatible integration work need sequencing or isolated branches and a merge owner even without a product dependency.

An upstream change invalidates consumers that rely on its changed contract or behavior. Pause affected dispatch, record the reason, and rerun affected integration checks. Unrelated tickets continue. For concurrent writers that cannot be isolated, serialize work. Completion requires verification of the integrated artifact, not just isolated worker branches.
