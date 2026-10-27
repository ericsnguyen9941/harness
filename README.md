# harness-kit

Onboard any repository onto an agent-development harness: the repo patterns proven (and still being proven) in the signalv2 experiment — thin operating manual, hard gates, reading map, feature docs, friction log with prediction→outcome discipline, definition of done, merge philosophy.

The kit splits onboarding along the judgment line:

- **`init.ts` (deterministic)** copies the skeleton — never overwrites, stamps a version, and tells you the one next step.
- **`/harness-light-onboard` (agent, judgment)** asks you only what you alone know — what the project is for, who uses it, what is already decided, and the few choices that are expensive to reverse — then decides everything else as recorded defaults and shows them, with the inferred risk posture and gates, on one decision sheet you correct once. It then builds a **thin default layer** for all seven pillars — verified commands, domain gates, a reading map pointing only at docs that exist, and a runnable definition of done. Three to five turns of your time. Thickening a pillar later is `/harness-pillar`'s job.

## Install & onboard — one command

Requirements on any machine: `bun` and `git`. Then, from anywhere:

```bash
curl -fsSL https://raw.githubusercontent.com/nguyenngocanh94/harness/main/onboard.ts | bun - /path/to/target-repo
```

The first run clones the kit into `~/.cache/harness-kit`; later runs reset it to the published head, so every machine installs the latest kit automatically (offline falls back to the cached copy with a staleness warning). When it finishes, open the target repo in your agent tool and run the onboarding workflow (`/harness-light-onboard` in Claude Code, `$harness-light-onboard` in Codex; other tools read the same body from `docs/harness/workflows/light-onboard.md`) — the skeleton is installed, the adaptation happens there.

Convenience alias for your dotfiles:

```bash
alias onboard='curl -fsSL https://raw.githubusercontent.com/nguyenngocanh94/harness/main/onboard.ts | bun -'
# then, inside any repo:
onboard .
```

Equivalent from a local clone:

```bash
git clone https://github.com/nguyenngocanh94/harness.git
bun harness/onboard.ts /path/to/target-repo
```

Overrides: `--repo=<git-url>` or `HARNESS_KIT_REPO` (fork/mirror), `--ref=<branch>`, `HARNESS_KIT_CACHE` (cache location), `--force` (onboard a non-git directory).

`init.ts` remains the underlying installer — `onboard.ts` is bootstrap-only and never touches the target itself.

## What lands in a target

| File | Role |
| --- | --- |
| `AGENTS.md` | operating manual scaffold, canonical — read by every AGENTS.md-aware tool (Codex, Cursor, Copilot, Gemini CLI, Aider, Zed, …); generic core verbatim, `TODO(harness)` slots |
| `CLAUDE.md` | bridge to `AGENTS.md` (symlink, or an `@AGENTS.md` shim) so Claude Code reads the manual too — created by init |
| `HARNESS.md` | the experiment map: principles, the seven pillars, mechanism inventory, seeded bets, probe protocol |
| `docs/harness/friction.md` | the learning loop — protocol header, zero entries |
| `docs/harness/risk-profile.md` | risk-aware onboarding record — exposure, non-negotiable baselines, and evidence required before feature work |
| `docs/features/_template.md` | per-feature doc template (invariants, verify-as-command) |
| `docs/harness/legibility.md` | runtime-legibility skeleton — logs, state, reproduction, one walked-through failure |
| `docs/harness/merge-evidence.md` | the evidence block every merge carries, plus per-forge adapters |
| `docs/harness/examples/verify.md` | the `verify` entry point by stack, a warning hook, a minimal CI job — examples, not mechanisms |
| `docs/harness/workflows/{light-onboard,feature,pillar,learn,review,probe,upgrade}.md` | tool-neutral workflow bodies — the single source any agent follows |
| `.claude/commands/{harness-light-onboard,feature,harness-pillar,harness-learn,harness-review,harness-probe,harness-upgrade}.md` | thin Claude Code entry points that delegate to the workflow bodies |
| `.agents/skills/{harness-light-onboard,feature,harness-pillar,harness-learn,harness-review,harness-probe,harness-upgrade}/SKILL.md` | thin Codex skill entry points (`$harness-light-onboard`, …) that delegate to the same workflow bodies |
| `docs/harness/kit-version` | stamp for update tracking (the only file init ever rewrites) |

If any template file already exists, init leaves it untouched and drops a `<name>.harness-kit` reference copy next to it when the published template differs. The upgrade workflow (`/harness-upgrade`) walks those references: manuals and workflow bodies are merged, `.claude/commands/*.md` and `.agents/skills/*/SKILL.md` wrappers are *replaced* (kit-owned dispatch shims — an old-kit wrapper can shadow the current workflow body), logs and templates take the structural change only. A repo onboarded by an older kit (a real `CLAUDE.md`, no `AGENTS.md`) is detected as a migration: init leaves `CLAUDE.md` alone, drops `AGENTS.md.harness-kit`, and the upgrade workflow moves the content into `AGENTS.md` and installs the bridge.

## Updating an onboarded repo

Re-run `init.ts` — it copies files added by newer kit versions, creates references for every changed template file, refreshes the stamp, and never overwrites adapted content. Then run `/harness-upgrade` in the repo; `CHANGELOG.md` here lists what moved between any two versions. Template changes always bump `VERSION` and add a changelog entry.

## The feedback loop

Every task runs a bounded `/harness-learn` check before handoff, including blocked or abandoned work. It uses the existing handoff/review/usage evidence, allows `none`, routes findings to the relevant doc or friction log, and gives remaining work an owner. The integrator catches up after merge or local closure only when the result is missing or new evidence arrived; later relevant tasks check predictions. Periodic `/harness-review` still owns pattern promotion and archiving.

Onboarding and upgrade name the integrator and the existing place the result lives. The kit ships instructions and entry points, not an automatic merge watcher: an external orchestrator must connect its own handoff/closure path. No full transcript audit or mandatory rule edit on each merge.

Every onboarded repo keeps its own friction log. Entries about the kit's templates (not the repo's domain) get ported back to this repo's `docs/harness/friction.md` with the usual prediction→outcome discipline. Learnings flow: repos → kit → all future onboardings.

## Maturity — honest note

The patterns come from a live experiment (signalv2) whose bets are **still open** — hub-and-spoke routing, thin-manual sufficiency, prompt-level gates, and prediction honesty are being measured, not proven. Each onboarding is itself a probe; expect to feed friction back.

Risk changes the meaning of “thin.” A low-impact library may start with prompt-level gates, while a multi-tenant system handling financial, health, identity, credential, or other sensitive data needs mechanical controls before feature breadth. Onboarding records that posture in `docs/harness/risk-profile.md` and makes risk-driven prerequisites explicit rather than waiting for friction to prove the obvious.

Onboarding also records a scope ceiling. It stops after the harness or runnable foundation by default; product-feature code begins only when the human explicitly names that feature and routes it through the feature workflow.
