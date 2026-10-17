# Light onboarding — ask only what the human alone can answer

Date: 2026-10-17.
Status: accepted; implemented in v0.9.0. Supersedes the "the human confirms every decision; nothing is wired silently" rule of [`2026-07-09-cobuild-onboarding.md`](./2026-07-09-cobuild-onboarding.md) for onboarding. `/harness-pillar` keeps its one-question-at-a-time co-build.
Origin: the kit owner found `/harness-onboard` too heavy in use. Counting its turns: A2 asks four questions plus the scope ceiling, A3 five risk questions plus a baseline per exposure, and each of B1–B7 is a conversation or a confirmation — twenty to thirty human turns, several of them only "confirm you understood" (B5, B7). The 2026-10-16 re-onboarding of mihu also rebuilt every stage from `docs/plans/` by hand because the workflow had no path for an already-onboarded repo, and asked again what was recorded.

## Decision

Rename onboarding to **light onboarding** (`docs/harness/workflows/light-onboard.md`, `/harness-light-onboard`, `$harness-light-onboard`) and replace "confirm every decision" with a question rule:

- **Ask** only for facts the human alone holds (purpose, users, non-goals, outside constraints, decisions already made) and for choices that are expensive to reverse and turn on their preference (platform, primary datastore, hosting, one deployable or several, identity provider).
- **Decide** everything else as a recorded default: stack details, module layout, tooling, `verify`, budgets, merge path, legibility stubs, reading map.
- **Show** every decision once, on one tagged decision sheet (`asked` / `inferred` / `default`); the human strikes what is wrong, the rest stands.
- **Re-run** reads the newest pillars plan and asks only about what changed since.

Target: three to five human turns. The closing pillars plan gains a **Decided by default** list so a later session revisits a default without asking again.

The workflow also asks for a development model fit for parallel agents — module boundaries, shared hot files and their rule, contracts with a drift check, end-to-end slices — recorded only where it applies.

## What does not get lighter

- Product facts are never invented; a default is how to build, never what the product is.
- Recorded commands were executed; versions were checked.
- Risk is inferred, never defaulted down: posture and every gate always appear on the sheet with evidence, and uncertainty takes the higher posture. Elevated/critical prerequisites still block feature breadth.
- The scope ceiling stays, default `harness + runnable foundation`.

## Why rename instead of edit in place

The owner asked for the new name. `init` never deletes, so repos onboarded before 0.9.0 keep `onboard.md` and its two wrappers beside the new set. The upgrade workflow gains a **Retired kit files** step: the changelog names retired files, and upgrade deletes them after moving any repo-specific guidance. Only re-onboarding used the old files, so removing them takes nothing an onboarded repo runs day to day; this record clears the "removing a mechanism onboarded repos depend on" gate.

## Rejected

- Keep both workflows: two onboarding entry points that drift apart, and nobody knows which one is current.
- Drop the risk conversation entirely: risk is the one area where a wrong silent default is expensive, so it moves from five questions to one sheet section that is always shown.

## Prediction (close in the friction log)

The next onboarding run with `/harness-light-onboard` reports five human turns or fewer, still ends with a passing `verify`, a risk profile with posture and baselines, and domain gates; and a re-run on an onboarded repo asks no question already answered in `docs/plans/`.
