# Task learning at delivery

## Problem and evidence

The 2026-10-27 audit of plantrip PLA-104 (PR #29, merged revision `46928b2d4059e315cb7593316f7a6c57c95a7e6b`) found that the orchestrator recorded the UI-test dark-screenshot limitation in project memory while repository instructions still gave older guidance. A design-source path was known to the orchestrator but the worker searched for it again. The target lacked the kit's reading map and friction mechanisms, so this is not evidence that a fully installed workflow failed; the kit nevertheless lacked a default delivery-time capture path. Its periodic review existed, but post-merge wiring was explicitly optional.

## Decision

Add one tool-neutral learning workflow with matching per-tool shims. The implementer captures a bounded result before handoff; the integrator catches missing/new evidence after merge or local closure. Existing handoff, review and usage summaries are the inputs. Task/PR plus revision and theme identify repeated events. No new state store, watcher, runtime dependency or automatic rule editor.

Route project facts to the relevant doc, harness friction to the log, and unfinished product work to an owned follow-up. A later relevant task observes a linked prediction. The periodic review still owns pattern promotion and archiving under its existing authority boundaries. `none` is a normal result; a successful merge is not proof a harness change saved work.

Onboarding/upgrade must name the integrator and merge the trigger into the real handoff record, not merely install a workflow file. External orchestrators need a separate closure adapter; installing this kit does not create one. This includes handling both local merges and external merge notifications without double capture.

## Prediction and validation

After upgrade, the next three completed tasks should each carry a learning result, any finding should have a durable destination or owned follow-up, and repeating one closure event should add no duplicate entry. The next relevant task should cite evidence for a prior prediction rather than mark a prompt edit successful on merge. Inspect improvements are compared with calls/tokens/context when available and with missed behavior/rework; metrics not recorded remain unknown.

Installer tests exercise upgrading adapted manuals/evidence and retaining friction history; the existing template suite checks wrapper and path consistency. These checks establish packaging only. Live task behavior and an orchestrator adapter remain unmeasured/unimplemented in this change.
