# Changelog — template changes by kit version

Read this when `/harness-upgrade` has references to merge: find the span between the repo's previous `docs/harness/kit-version` and the current one, and merge *these* intents. Every change to `template/` adds an entry here in the same commit (kit convention).

## 0.11.0 — 2026-10-27

- Feature workflow accepts an authorised delegated brief as completed product intake, checks feasibility in scoped inspect, batches independent reads and stops exploration when the implementation path and verification are known. Contradictions return to the decision owner.
- Task learning compares token buckets, model calls and recorded timing lanes alongside acceptance quality and rework. Missing/stale metrics remain unknown; overlapping time lanes are never summed. Integrators route prediction links into the next relevant brief.
- Merge evidence records the bounded efficiency observation and its scope; `none` stays valid and no new telemetry service or full transcript audit is required.
- No files retired and no validation or authority gates weakened.

## 0.10.0 — 2026-10-27

- New `docs/harness/workflows/learn.md` with `/harness-learn` and `$harness-learn` entry points: bounded evidence capture before every task handoff, missing-result catch-up after merge/local closure, source-based deduplication, destination/owner routing, and checking predictions on later relevant tasks. `none` is a valid result; no compulsory rule edit or full transcript audit.
- `AGENTS.md`, feature workflow and merge evidence now route through task learning. Onboarding names the integrator and result location. `HARNESS.md` and probe count delivery and later observation of lessons, including inspect-code calls/tokens when available and quality/rework alongside them.
- Upgrade must merge the learning trigger and evidence field into adapted manuals and forge/handoff templates, preserving historical friction entries. External orchestrators need their own integration; no watcher or post-merge automation is installed by the kit.
- Periodic review retains its cadence and human decision boundaries. Its optional merge-hook section is now explicitly about maintenance reminders, separate from default task learning. Friction entries identify source task/revision in the existing `Friction` field.
- No files retired; installer never-overwrite behavior and validation gates are unchanged.

## 0.9.0 — 2026-10-17

- Onboarding renamed and lightened: `docs/harness/workflows/light-onboard.md`, `/harness-light-onboard` (`.claude/commands/harness-light-onboard.md`), `$harness-light-onboard` (`.agents/skills/harness-light-onboard/SKILL.md`). It asks only what the human alone knows plus choices expensive to reverse, decides the rest as tagged defaults, and confirms everything on one decision sheet (three to five turns). Risk posture and gates are inferred but always shown; scope ceiling, facts-only, and risk prerequisites are unchanged. A re-run reads the newest pillars plan and asks only about changes. The pillars plan gains a "Decided by default" list.
- Retired: `docs/harness/workflows/onboard.md`, `.claude/commands/harness-onboard.md`, `.agents/skills/harness-onboard/SKILL.md`. Delete them on upgrade; move any repo-specific guidance from the old body into `light-onboard.md` first.
- Upgrade workflow: new "Retired kit files" step.
- `AGENTS.md` workflow line points at `light-onboard.md`; domain-gates slot says "inferred at onboarding, confirmed on its decision sheet".
- `HARNESS.md`: pillar intro and mechanism rows drop the Stage B step numbers and the interview wording.
- Review workflow: budgets heading no longer cites onboarding step B5.

## 0.8.0 — 2026-10-08

- New `.agents/skills/<name>/SKILL.md` for all six workflows: Codex entry points (`$harness-onboard`, `$feature`, `$harness-pillar`, `$harness-review`, `$harness-probe`, `$harness-upgrade`), same names as the Claude Code commands, same one-line dispatch to `docs/harness/workflows/<name>.md`. Treat them like `.claude/commands/*.md` on upgrade: kit-owned shims, replace with the reference.
- `AGENTS.md` Workflows section names both entry points and tells any other tool to read the workflow file directly.
- `HARNESS.md` mechanism table: workflow rows now point at the tool-neutral bodies under `docs/harness/workflows/`, not at `.claude/commands/`; new "Workflow entry points per tool" row.
- Upgrade workflow lists `.agents/skills/*/SKILL.md` beside `.claude/commands/*.md` as replace-not-merge shims; onboarding names both entry points.

## 0.7.0 — 2026-10-08

- New `docs/harness/legibility.md`: runtime-legibility skeleton (logs, state, reproduction, one walked-through failure). Onboarding B4 fills it.
- New `docs/harness/merge-evidence.md`: the evidence block every merge carries, with per-forge adapters. Onboarding B6 wires the adapter; `AGENTS.md`'s merge section links it.
- New `docs/harness/examples/verify.md`: `verify` shape per stack, a warning hook, a minimal CI job. Onboarding B3 points at it.
- New workflow `probe` (`/harness-probe`): measure one open bet with a fresh uncoached agent; records a dated `probe — bet #N` friction entry. `HARNESS.md` "How to run a probe" now delegates to it.
- New workflow `upgrade` (`/harness-upgrade`): walks `*.harness-kit` references after re-running init. The five merge/migrate/replace paragraphs moved out of onboarding into it; onboarding opens with "References first".
- `AGENTS.md`: two workflow lines; merge section links the evidence block; working notes route runtime questions to `legibility.md`.
- `HARNESS.md`: thin defaults for mechanical enforcement, legibility, merge philosophy, feedback loop name their files; mechanism table gains probe, upgrade, legibility, merge-evidence rows.

## 0.6.1 — 2026-10-08

- `init`: every existing template file that differs now gets a one-time `<name>.harness-kit` reference (allowlist removed). Expect `docs/harness/friction.md.harness-kit` on the first init after this version — merge the Archive section and budgets (0.6.0), keep every entry.
- Onboarding: "Merge other updated template files" step (now part of the upgrade workflow in 0.7.0).
- Friction protocol: later sessions may edit `Change` when acting on an entry, not only `Outcome`.

## 0.6.0 — 2026-10-08

- Review workflow: five steps (sweep → pattern pass → distil/archive → prune → report); prune gains trim and `Superseded by:`; budgets table; five-check mechanical recipe.
- Friction protocol: closed entries archived to one line under a new `## Archive` section; live-log budget ~120 lines.
- Onboarding B5 agrees budgets; `HARNESS.md` entropy and feedback rows updated.

## 0.5.1 — 2026-08-02

- Onboarding records a scope ceiling; feature code needs an explicitly named feature.

## 0.5.0 — 2026-08-02

- New `docs/harness/risk-profile.md`; risk posture conversation (A3) in onboarding; credible-when column per pillar; risk prerequisites in feature and pillar workflows.

## 0.4.1 — 2026-07-10

- `init`: stale `.claude/commands/*.md` wrappers get references; onboarding replaces them with the thin wrapper.

## 0.4.0 — 2026-07-09

- New review workflow (`/harness-review`) with a concrete cadence.

## 0.3.0 — 2026-07-09

- `AGENTS.md` is the canonical manual; `CLAUDE.md` becomes a bridge. Workflow bodies move to `docs/harness/workflows/`; commands become thin wrappers.

## 0.2.0 — 2026-07-09

- Co-build onboarding (Stage A basics, Stage B one thin layer per pillar); `HARNESS.md` gains the seven pillars; new `/harness-pillar`.

## 0.1.3 and earlier — 2026-07-05 … 2026-07-09

- `/feature` workflow; greenfield purpose interview; initial skeleton.
