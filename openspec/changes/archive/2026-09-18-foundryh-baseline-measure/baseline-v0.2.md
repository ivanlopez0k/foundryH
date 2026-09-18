---
baseline: v0.2
change: foundryh-baseline-measure
local_only: true
---

# Baseline v0.2: T2 + T1 measured rows (T3 narrated)

Scope guards (read before using): every claimed P1–P6 cell holds a counter or
`n/a` with exactly one tag (`[measured]`, honest miss, or `[narrated]` for T3).
Counters only — no token totals. No SAP/servicios rows (out of scope). Pack
verification strings are downstream intents: record them in run order, never
execute them at the harness root. Local-only: no push, no remote mutation, no
archive edit, no schema edit. v0.2 RELEASED (D4): both rows passed the verify
hand-check (tag, window, branch evidence per row); published as OQ-4 input
with no savings claim.

## Counter table

| Baseline | Task | Path / harness | P1 hit+fallbacks | P2 files | P3 attempts | P4 size vs 400 + chained | P5 early-stop | P6 forecast | Notes |
|---|---|---|---|---|---|---|---|---|---|
| v0.2 | T2 | liviano docs-clarity micro-edit, this change (`lightweight-generic@0.1.0`) | miss + 3 fallback scans, allowed (codegraph optional, warn) [measured] | 12 files [measured] | 1 attempt + 1 tool retry [measured] | 225 vs 400, chained N [measured] | n/a (no commands executed) [measured] | Y (forecast 60-150, Low, single PR in tasks.md) [measured] | branch `measure/t2-docs-clarity` from clean tree `7c6ea39`; window = acquire-to-settle history only; P6 nuance: forecast from SDD tasks discipline, not the liviano pack default (`tokenForecastRequired` false) |
| v0.2 | T1 | ERP contract edit, this branch (`erp-dotnet-angular@0.1.0`) | 1 miss + 2 scans, init in-window [measured] | 11 files [measured] | 1 attempt + 1 tool retry [measured] | 184 vs 400, chained N [measured] | n/a (no commands executed) [measured] | Y (forecast 50-130, Low, single PR in tasks.md) [measured] | branch `measure/t1-erp-contract` from clean tree `4190433`; window = acquire-to-settle history only; legacy `stackDetails.notes` removed, `migrationCare.notes` canonical intact, schema-valid; `.codegraph/` init local-only, gitignored, cost in P1/P2 per #29-C4 |
| v0.2 | T3 | no-harness control | n/a, fallback scans unbounded without ledger [narrated] | n/a, files re-read without record [narrated] | n/a, retries unlogged [narrated] | n/a, size estimated, chaining unknown [narrated] | n/a, nothing recorded [narrated] | n/a, forecast presence unknown [narrated] | counterfactual control: same change ad-hoc without harness; never counted, never measured |

Tag-audit scope: both T2 and T1 rows are measured; every claimed P-cell
carries exactly one tag. A claimed counter without a tag fails.

## Attempt window (acquire-to-settle only)

- Acquire: orchestrator-acquired, work-unit `measure-t2-pending` (reported 3/800).
  Settle: pending — orchestrator settles; sdd-apply never acquires or settles.
- Freeze: P1–P3 frozen at this pending-table write. Post-freeze verification
  commands (tag greps, numstat, status) are audit evidence listed in
  `apply-progress.md`, excluded from P-counts by this stated rule.
- Pre-acquire reads: none counted (fresh attempt; every counted op below is
  in-window tool history of this attempt).
- P1 scans counted (3): (1) Read dir-listing of
  `openspec/changes/archive/2026-09-17-foundryh-baseline-fill/`, (2) Glob
  `openspec/changes/foundryh-baseline-measure/**/*`, (3) `Get-ChildItem
  openspec/changes`. Targeted Reads of known paths and git VCS ops are not
  sweeps. No `codegraph_explore` call: miss, allowed under liviano optional
  (warn) — no structural question existed (all paths known).
- P2 files counted (12 distinct): measure `tasks.md`, `design.md`,
  `proposal.md`, delta `specs/sync-baseline/spec.md`; `work-unit-commits`
  `SKILL.md`; `PLANNING.md`; `INFORMACION.md`; canonical
  `openspec/specs/sync-baseline/spec.md`; archive `archive-report.md`,
  `baseline-fill.md`; token-research `research.md`; `openspec/config.yaml`
  (via shell read).
- P3 counted: 1 work-unit attempt + 1 tool retry (`head` unrecognized in
  PowerShell 5.1 during branch listing, recovered via `git status`/`git log`).
  All 3 doc edits applied first try; no edit retries.
- P4 counted (attempt-authored only): tracked doc mods (numstat adds+dels on
  `PLANNING.md` + `INFORMACION.md`) + 2 lines per flipped tasks checkbox (11
  flips) + full new-file line counts of this pending file and
  `apply-progress.md`. Prior-phase base content (proposal/design/delta/tasks
  body) is context, not this attempt's authorship — itemized separately in
  `apply-progress.md` with the full-branch numstat for context.

## T1 attempt window (acquire-to-settle only, candidate A)

- Acquire: orchestrator-acquired, work-unit `measure-t1-erp-contract`
  (request `t1-apply-20260918-01`, token `sha256:6e36…ae8d94`, max 3 attempts /
  800 lines, untracked-scope exclude). Settle: pending — orchestrator settles;
  sdd-apply never acquires or settles.
- Freeze: T1 P1–P3 frozen at this T1-row write. Post-freeze verification
  commands (tag greps, numstat, status, branch) are audit evidence listed in
  `apply-progress.md`, excluded from T1 P-counts by this stated rule.
- Pre-acquire reads excluded: Step-2 locator reads (tasks/spec/design/proposal,
  existing apply-progress, schema, config, Engram #51, HEAD status/log) plus
  T1-A planning M body (proposal/spec/tasks planning deltas) are context, not
  counted. Every counted op below is in-window tool history of this attempt.
- T1 P1 scans counted (1 miss + 2 scans): (1) `codegraph_explore`
  `stackDetails notes migrationCare` → miss, no index (forced per candidate-A
  design); (2) root `Get-ChildItem -Force` listing (1 scan); (3) post-init
  `codegraph_explore` with `projectPath` → indexed query (no relevant code —
  JSON keys are not code symbols, honest). `gentle-ai codegraph init`
  built `.codegraph/codegraph.db` in-window; index cost charged to T1 P1/P2
  per #29-C4. Targeted Reads of known paths and git VCS ops are not sweeps.
- T1 P2 files counted (11 distinct): `tasks.md`, delta
  `specs/sync-baseline/spec.md`, `design.md`, `proposal.md`,
  `apply-progress.md` (existing, merged), this pending file, `foundry.json`,
  `foundry.schema.json` (read-only reference), `.gitignore`,
  `openspec/config.yaml` + `.codegraph/codegraph.db` (created, local-only,
  gitignored).
- T1 P3 counted: 1 work-unit attempt + 1 tool retry (`gentle-ai codegraph
  --help` usage error, recovered via `gentle-ai codegraph init --cwd`
  syntax). Genuine edit + gitignore decision applied first try; no edit
  retries.
- T1 P4 counted (attempt-authored only): tracked mods numstat adds+dels on
  `foundry.json` + `.gitignore` + this pending file + `apply-progress.md`
  (tasks.md numstat excluded — 7 flips counted separately at 2 lines each) +
  7 tasks flips x2. Prior-phase planning body excluded as context, with
  full-branch numstat reported in `apply-progress.md` for transparency.

## Intent ledger (recorded in order, zero executed at root)

- Liviano (`lightweight-generic@0.1.0`): `npm test` -> `npm run lint`,
  failFast false.
- ERP (`erp-dotnet-angular@0.1.0`, T1 candidate A): `dotnet test` ->
  `ng test` -> `ng lint`, failFast true. Recorded in order, never executed
  at the harness root (measurement-only git/grep/read/edit ops only).
- Executed at harness root: pack commands none (measurement-only git/grep/read
  ops only). Pushed to remote: nothing.

## Pins

- Core `gentle-ai@2.7.0`; team-4 single-writer / single-PR / 400-gate; liviano
  lens (`lightweight-generic@0.1.0`, codegraph optional, failFast false,
  `tokenForecastRequired` false); P1–P6 definitions per #29 steps 1–8; intents
  recorded in order; zero root executions; local-only.
- T1 ERP lens (`erp-dotnet-angular@0.1.0`, codegraph required, failFast true,
  `tokenForecastRequired` true); same P1–P6 definitions; ledger
  `dotnet test` -> `ng test` -> `ng lint` in order; single-writer single-PR
  on `measure/t1-erp-contract`; zero root executions; local-only, no push.

## Sources (all read-only; archives untouched)

- Protocol/template: `archive/2026-09-17-foundryh-token-research/research.md`
  (section 5 template + steps 1–8) and v0.1 `baseline-fill.md` (tag-split
  precedent, 74-line P4 recount method).
- T2 edit: `PLANNING.md` (title orthography + proxy-counter disambiguation of
  the pending bullet) and `INFORMACION.md` (title orthography) on branch
  `measure/t2-docs-clarity`, liviano lens.
- Closed archives (`2026-09-17-foundryh-baseline-fill/`, token-research):
  read-only sources; never edited (verified via scoped git status/diff).

## v0.2 release record (D4)

- D4 hold RELEASED at archive time: both rows passed the verify hand-check
  (tag, window, branch evidence per row). This file is the `baseline/v0.2`
  publication: T2 measured (P4 225 vs 400) + T1 measured (P4 184 vs 400) +
  T3 narrated, counters only, no token totals, no SAP rows, no savings claim.
  OQ-4 input. Local-only, no push.
- T1 trigger watch closed by the candidate-A ERP contract edit landed on
  `measure/t1-erp-contract` with branch evidence.
- T3 stays narrated indefinitely; no solicited T3 run.
