# Behavioral validation scenarios

Run these in a disposable project with the skill exposed as instructions. These are behavior tests, not assertions that a host has loaded the skill. Record decisions and generated board/ticket/run artifacts. Do not substitute keyword matching for observing decisions.

| Scenario | Input / environment | Expected invariant |
| --- | --- | --- |
| Simple UI | Change one known CTA label; existing action must remain | One small Solo ticket, exact copy, appropriate rendered/action evidence; no invented redesign |
| Complex feature | Saved items with approved API contract, UI, integration | Independently verifiable tickets, explicit edges, isolated parallel work where available, final integrated check |
| Investigation | Intermittent form failure; cause unknown | Separate evidence from hypothesis; bounded investigation; no fabricated diagnosis |
| Dependencies | UI can use a verified contract while API implementation continues | Contract completion or verified versioned artifact releases UI; integration waits for both implementations |
| Browser required | Fix mobile menu; no browser access | Implementation may proceed; mandatory browser result stays pending, ticket Blocked, no Done |
| Incomplete request | Add authentication; no project convention resolves sign-in method | Ask material question, no invented provider, affected work Blocked, independent work continues |
| Failed evaluation | Mandatory case fails on first run | Preserve failure, repair and rerun affected checks; Done only with current passes or actual approved exception |
| No subagents | Same complex project, single executor | Sequential Solo fallback, same dependencies and evidence rules, no fictitious workers |

Also inspect interrupted ownership recovery, dependency cycles/missing IDs, contract invalidation, integrated revision evidence, and draft-only authorization. Packaging validation does not establish behavioral compliance or real application correctness. Report scenario execution separately from live browser/integration testing.
