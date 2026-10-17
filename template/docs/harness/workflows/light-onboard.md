# Light onboarding workflow

You are onboarding this repository onto the harness installed by harness-kit.
The skeleton files already exist. Light onboarding builds a thin default layer for every pillar (`HARNESS.md`, "The seven pillars" — read it first), but the human answers only what they alone can answer. You decide everything else, write it down as a default, and show it once on a single decision sheet the human corrects.

Target: three to five human turns. A question the human did not need to answer is cost, not care.

## The question rule

Ask the human only for:

1. **Facts only they hold** — what the project is for and who uses it, what it will deliberately not do, constraints from outside the repo (existing services, hosting, team, deadlines, contracts, law), and decisions already made.
2. **Choices that are expensive to reverse and turn on their preference** — platform, primary datastore, hosting, one deployable or several, identity provider.

Everything else you decide: stack details, module layout, test/lint/format tools, `verify`, review budgets, merge path, legibility stubs, reading map. Each is a **default** — recorded as your choice, cheap to change, visible on the sheet.

Never ask what the repo, `docs/plans/`, or an earlier answer already tells you. When you must ask, put every question you need into one message.

The spine that does not get lighter:

- **Never invent product facts.** A default is a choice about how to build, never a claim about what the product is. Purpose and behavior come from the human or the code.
- **Facts only in what you write.** Every recorded command was executed by you, now, successfully. Every doc you point at exists. Every version you name was checked against a manifest or registry.
- **Risk is never defaulted down.** You infer the risk posture, but it always appears on the sheet with its evidence; when unsure, take the higher posture. Missing elevated/critical prerequisites block feature breadth, exactly as `docs/harness/risk-profile.md` says.
- **Scope ceiling.** Default `harness + runnable foundation`. Feature-specific domain code, schemas, endpoints, UI flows, or MCP tools only if the human names and confirms a first feature; later features go through `docs/harness/workflows/feature.md`.
- **Thin is risk-adjusted.** No CI, heavy lint, or architecture rules unless the risk posture makes them prerequisites; route those through `docs/harness/workflows/pillar.md`.
- Work on a branch (`harness-light-onboard`); one commit at the end, carrying evidence. Friction you hit goes in `docs/harness/friction.md`.

---

## Step 1 — Read (no questions)

- **References first.** If `init` dropped any `<name>.harness-kit` file, run `docs/harness/workflows/upgrade.md` before anything else.
- **Already onboarded?** If `docs/plans/*-harness-pillars.md` exists, read the newest one and the decision records it links. Find what changed since (git log from that plan's commit, new manifests, new modules). Only changes reach the sheet; nothing already recorded is asked again.
- **Inventory.** Manifests (`package.json`, `composer.json`, `go.mod`, `Package.swift`, `build.gradle`, `Cargo.toml`, `pyproject.toml`, …), CI configs, Makefiles, READMEs, source layout. Run the candidate test/lint/build commands now to learn which actually work.
- Decide: **does the repo tell you what it is?**

## Step 2 — Ask (one message, at most one follow-up)

- **Purpose legible:** state in 2–4 sentences what you read the project to be and its stack, then ask in the same message: is this right, and what is already decided that the repo does not show yet (hosting, constraints, things it must never do)?
- **Greenfield:** one open message — what it does and for whom, what it will deliberately not do, and anything already decided (platform, stack, hosting, existing services, constraints).

Then at most one follow-up message, only for holes in the two question categories, bundled. If the human does not know, record `unknown — owner: <human>` and move on; a gap is not a reason for another round.

## Step 3 — Decide (no questions)

Draft each item and tag it `asked` (from the human), `inferred` (derived from their answers), or `default` (your choice).

1. **Stack.** Greenfield: propose one. Prefer, in order: what the human already runs; mainstream, well-documented tools agents know well; static types; tests that run headless from the CLI in seconds.
2. **Development model for parallel agents.** Record only what applies; a single-module repo gets one line.
   - Module boundaries — units one agent can change without touching another's files.
   - Shared hot files (project files, route or DI registries, lockfiles, migrations, generated code) and the rule for each: one owner, append-only, or generated and never hand-edited.
   - Contracts between parts (API spec, shared types, events): which side is the source of truth, and the check that fails when code drifts from it.
   - Work is sliced end to end (one user-visible behavior across all parts), not layer by layer.
3. **Verify.** One entry point (shapes in `docs/harness/examples/verify.md`), typecheck → lint → test, runnable headless; note its expected runtime.
4. **Risk posture.** Classify from the purpose through the exposures in `docs/harness/risk-profile.md`: sensitive data; multi-user isolation; money, external, or destructive effects; existing obligations; blast radius. Name the non-negotiable baselines.
5. **Domain gates.** Derived from the exposures, each phrased as a stop-and-confirm trigger an agent can recognize.
6. **Plain defaults.** Reading map; legibility (existing repo: from the code; greenfield: the open questions); review budgets as shipped in `docs/harness/workflows/review.md`; merge path as in `AGENTS.md`, with the evidence adapter for the forge in `git remote`; feedback loop as seeded; scope ceiling `harness + runnable foundation`.

## Step 4 — The decision sheet (one message)

Send one sheet grouped as: product, stack, development model, verify, risk posture and gates, plain defaults, unknowns with owners, scope ceiling. One line per decision, each tagged. Risk posture and every gate always appear in full, even when all are inferred.

Ask once: correct any line; anything not struck stands. Apply the corrections. A correction to a product fact or an expensive choice may need one follow-up; anything else you just apply and mention in one line — do not re-send the sheet for approval.

## Step 5 — Build (no more questions)

- `AGENTS.md`: what it is, stack, architecture (or delete the section), reading map, conventions grounded in code (including the development-model rules that hold now or that the foundation creates), domain gates, commands (each executed), verification.
- `docs/harness/risk-profile.md`: posture, exposures, baselines, evidence, unknowns.
- `verify`: wired, run to pass, then a deliberately broken test makes it fail; restore.
- `docs/harness/legibility.md` and the forge adapter from `docs/harness/merge-evidence.md`.
- Runnable foundation, if the ceiling includes it: only what makes `verify` meaningful and lays down the module boundaries. No product behavior.
- Greenfield, or the stack or development model changed: a decision record `docs/plans/<today>-foundation.md`.

Stop and ask only if building would cross a hard gate or contradicts something the human said.

## Closing

1. Run `verify`. Include its real output.
2. Write `docs/plans/<today>-harness-pillars.md`: the seven-pillar table (thin layer built, why it meets the credible-when criterion, how to thicken), risk prerequisites separate from optional thickening, and a **Decided by default** list — each default and where to change it — so a later session revisits it without asking again.
3. Commit the `harness-light-onboard` branch.
4. Report: files created or adapted and every `TODO(harness)` slot still open; the pillar table; how many human turns the run used; the three self-check answers — did I make any doc stale (fixed?); did I hit friction (logged?); what did I not attempt.

If the scope ceiling excludes feature implementation, stop here.
