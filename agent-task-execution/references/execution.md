# Execution and evidence protocol

1. **Prepare:** read the ticket and project conventions, verify execution authorization and dependencies, and claim ownership through the board writer. Check for unfinished prior work before retrying. Record the available tools and known verification limitations.
2. **Implement:** keep changes within scope. Record important choices and changed files. Preserve user work. A newly discovered unrelated bug becomes a separate Draft ticket or a report; it does not authorize an unsolicited fix. Do not silently expand or weaken requirements. If the user's outcome needs clarification, block only that work.
3. **Evaluate:** enter Review, run the specified checks, and append actual results with criterion IDs. Evidence identifies the tested revision (commit or stable content digest), environment, inputs, command/action, actual output, exit code when applicable, and artifact path. Screenshots alone do not prove an interaction or backend persistence; exercise the user flow when required. Capture responsive states for relevant viewports. A missing browser means pending browser verification, even if unit tests pass.
4. **Repair:** for failures, preserve the failed attempt, investigate, repair, and rerun the failed and materially affected checks. New changes invalidate prior evidence for affected behavior. Stop repeated unchanged attempts when they yield no new evidence; record a blocker and concrete next action rather than spinning or inventing a pass. Agree a proportional retry limit for costly or externally mutating operations; a ticket is not authorization for such actions.
5. **Integrate:** if workers used branches/worktrees, designate an integrator; inspect diffs, resolve conflicts deliberately, and rerun affected evaluation on the combined artifact. No automatic merging, deployment, or publishing authorization is implied by Team mode.
6. **Finish:** the board writer checks all mandatory criteria against the final artifact. Optional checks cannot block Done. A user-approved exception must quote or link the actual decision and preserve the unmet outcome. Move Review → Done and report implemented result, important files, tests and results, exceptions, and remaining issues concisely. If checks remain pending or failed without an approved exception, report incomplete status plainly.

## Resume after interruption

Read board, specifications, run history, worktree/diff, and evidence. Reconcile the actual artifact with the last tested revision. Reconfirm worker ownership and dependency validity. Resume the next unmet action; do not recreate tickets, discard failures, or rerun unrelated checks solely because context was lost.

## Evaluation integrity

Executors may run their own checks in Solo mode; evidence remains mandatory. With workers, the router examines returned evidence and requests missing or contradictory checks. An independent checker is useful when supported and proportionate, but not a mandatory platform capability. No executor or router can fabricate user approval, test output, browser access, or an independent review.
