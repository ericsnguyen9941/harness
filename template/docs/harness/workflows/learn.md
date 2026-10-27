# Task learning workflow

Run before handing off any task or pull request, including a blocked or abandoned task. When a merge or task-close event arrives, the integrator checks this result and runs the missing part once. This is a short check on work already done; periodic harness maintenance stays in `docs/harness/workflows/review.md`.

## 1 — Check existing evidence

Use the task's handoff, review findings and bounded usage summary when available. Read only the evidence needed to identify a misleading instruction, missing locator, repeated failed approach, unnecessary reading or another obstacle a future task could avoid. Missing usage is unknown, not zero; do not open full transcripts, rerun tests or launch a new investigation just to fill this check.

Identify the task or PR and the revision the evidence covers. Look for its existing learning result and any linked friction entries first. A repeated merge/close notification reuses that result; a later revision with new findings checks only the new evidence. For each theme, record the same task's friction once. Separate tasks repeating a theme remain separate evidence for the review's pattern pass.

## 2 — Check linked predictions

Check only open predictions linked by this task, its reading-map entry or its handoff. When the current task supplies later evidence, use that evidence to update its `Outcome`: improved, unchanged or inconclusive, with the task/revision and observation. Keep untested predictions open; a merged prompt edit alone is not proof of better behavior. Broader pattern promotion and archiving stay in the periodic review.

For an efficiency change, compare model calls, separate input/cache-read/cache-write/output tokens and context, and recorded timing alongside review findings, missed behavior and rework. Match scope, size, model/effort, environment and measurement coverage; otherwise report not comparable. Task age includes idle time; prompt elapsed, tool elapsed and decision/handback waits may overlap, and summed invocation durations may include parallel work. Never add these lanes or call unallocated time model latency. High cache-read alone does not prove repeated file reading. Use existing bounded usage summaries and mark open-task observations provisional; absent or stale data stays unknown. Count docs only as supporting evidence: one shell call may read many files, and fewer reads can mean insufficient verification. A missing metric stays unknown. Run a dedicated `docs/harness/workflows/probe.md` only when the remaining uncertainty warrants a separate task.

If there is no new reusable learning, record any prediction outcome you updated, then record `Learning: none — <task/PR and revision>` in the existing handoff or merge evidence and stop. Do not add an empty friction entry or create a rule to satisfy the workflow.

## 3 — Route what was learned

For each concrete finding, choose its destination:

- **Project knowledge:** correct the relevant feature doc, runbook or source pointer within the task's authorized scope. Keep the always-loaded manual as the reading map; put local implementation detail in the doc for that area. Runtime-specific observations name the setup and uncertainty.
- **Harness friction:** append an entry to `docs/harness/friction.md` using its format. Put the task/PR, revision and a concise evidence pointer in `Friction`; `Change` names the destination or says `none yet`. A proposed change has a measurable `Prediction`; with no change yet, state what evidence would justify one. Keep `Outcome: open` until a later task or probe supplies evidence. An instruction that exists but was not followed is different from an instruction that is missing.
- **Product work still missing:** use the project's task tracker or backlog with an owner and a reference in the handoff. Recording a lesson does not turn failed acceptance into a pass.

A factual correction within the existing contract can accompany the task. A new standing rule, gate change or wider repair follows the project's decision authority and `docs/harness/workflows/review.md`; capture the proposal without expanding the current task or waiting for that maintenance to finish. For each open prediction, record the baseline evidence and measurement scope, identify the next relevant task or area and put a short link in its existing task record, area doc or handoff so the next worker can find it without reading the whole friction log. If that routing is outside your authority, record its owner as a follow-up. The integrator carries the relevant prediction and known facts into that next brief; the next worker checks only linked predictions. A lesson stored only in an orchestrator's memory must name the repo pointer or future brief that will deliver it to the next worker.

If the branch has already merged, prepare any repository correction on a new branch through the normal review path. If you cannot write that repository, hand the finding and destination to its owner and record it as a follow-up, not as a completed correction. Do not rewrite the merged branch or publish a tracker item/message without the project's authorization.

## 4 — Leave a bounded result

Record one result in the existing handoff or merge evidence, with at most three finding lines:

```text
Learning: captured | follow-up — <task/PR and revision>
- <obstacle> → <corrected file or friction entry>; next check: <observable behavior>
- <remaining action, if any> → <owner and backlog/PR reference>
```

Choose `captured` when every finding has a durable destination and no routing action remains; it does not mean a proposed fix is proven. Choose `follow-up` when an owner still needs to receive or implement a correction. Group related findings; link an existing report if there are more than three, rather than dropping them. The result is complete when each finding has evidence and a destination or an owned follow-up.

## Ownership and event delivery

The implementer owns the check before handoff. The integrator (human or orchestrator) owns catch-up after a merge or accepted local task; onboarding names that role and the existing place the result lives. A watcher or CI adapter may notify the integrator of missing results, deduplicating by task/PR and merge revision. The template installs instructions, not a watcher: if an orchestrator closes tasks without reading repository instructions, wire this check into its handoff/closure path separately. No adapter automatically promotes rules, archives entries or changes acceptance criteria.
