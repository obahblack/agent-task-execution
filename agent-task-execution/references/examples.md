# Example project and smaller tickets

The complete fictional login project is in [example-project/tasks/board.json](../assets/example-project/tasks/board.json). Each of its five ticket directories contains rd.md, eval.md, and run.md. This is a draft fixture, not evidence that login has been implemented. All project facts are explicitly example assumptions.

Execution waves after authorization and source resolution:

1. ticket-001: verify the contract.
2. ticket-002 API and ticket-003 interface: run concurrently as independent Solo tickets against that verified contract in separate workspaces.
3. ticket-004: integrate after both are Done; evaluate the combined artifact.
4. ticket-005: verify regression behavior after integration.

With one agent, use the same graph sequentially. A product dependency does not require a Team ticket. For collaboration inside a ticket, use Team and record scopes and integration ownership. A contract embedded in a still-active API ticket can instead use an artifact edge as defined in board.md; do not wait for the full API when only its verified contract is needed.

## Simple UI request

Input: “On /pricing, change the CTA from Submit to Start free trial.”

One Solo ticket. R1: the CTA on /pricing reads “Start free trial” and retains its existing action. E1: render /pricing, locate that CTA, confirm exact text, and activate it to confirm its existing action. Inspect existing source before defining the action. No invented redesign or mandatory team. A runtime/browser check remains pending if unavailable; source inspection alone cannot establish behavior.

## Unknown-cause investigation

Input: “Find why profile upload sometimes fails with Upload failed.”

One bounded investigation ticket can be Ready without knowing the cause: gather supplied reproduction details, inspect the upload path, and identify a reproducible cause or document reproduction attempts, logs, hypotheses, and the precise missing data. Do not silently promise a fix when asked only to investigate. Evaluation requires traceable observations and a supported diagnosis or the agreed inconclusive investigation outcome. If the request also asks for a fix, a diagnostic report alone cannot satisfy completion of that fix.

## Materially incomplete request

Input: “Add authentication.”

Inspect existing authentication and product conventions first. If desired sign-in method and protected behavior remain unknown, create a Draft specification and ask the smallest questions that determine those outcomes. Record Blocked for execution while waiting; do not choose a provider or invent registration requirements. Independent unrelated Ready tickets can continue.
