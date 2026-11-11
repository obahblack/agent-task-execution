# <ticket-id> — Evaluation

## Mandatory criteria
| ID | Requirement | Observable pass condition | Procedure and environment | Required evidence |
| --- | --- | --- | --- | --- |
| E1 | R1 | <Specific expected result> | <Inputs, setup, action/command, expected output> | <Output/log/screenshot/artifact path and revision> |

Include functional, edge, regression, browser/responsive, performance, and accessibility checks only as relevant to the requested outcome. Define supported viewports from project context or label representative checks as agent-selected. Do not invent target devices or performance budgets.

## Optional improvements
<Clearly non-blocking checks, or omit.>

## Completion rule
All mandatory criteria must pass against the final artifact. Record executions in run.md with criterion IDs, artifact revision, procedure, actual result, and evidence. An exception requires the user's explicit approval, rationale, scope, and residual issue; inability to run a check is not a pass. Specification changes require synchronized rd.md/eval.md updates and renewed affected checks. Never weaken a criterion merely to make a failing implementation pass.
