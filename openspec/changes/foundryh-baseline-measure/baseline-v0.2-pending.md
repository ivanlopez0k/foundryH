---
baseline: v0.2-pending
change: foundryh-baseline-measure
local_only: true
---

# Baseline v0.2 pending: T2 measured row (T1 pending, T3 narrated)

Scope guards (read before using): every claimed P1–P6 cell holds a counter or
`n/a` with exactly one tag (`[measured]`, honest miss, or `[narrated]` for T3).
Counters only — no token totals. No SAP/servicios rows (out of scope). Pack
verification strings are downstream intents: record them in run order, never
execute them at the harness root. Local-only: no push, no remote mutation, no
archive edit, no schema edit. v0.2 HOLD (D4): no `baseline/v0.2` publish until
T1 lands with tag, window, and branch evidence.

## Counter table

| Baseline | Task | Path / harness | P1 hit+fallbacks | P2 files | P3 attempts | P4 size vs 400 + chained | P5 early-stop | P6 forecast | Notes |
|---|---|---|---|---|---|---|---|---|---|
| v0.2-pending | T2 | liviano docs-clarity micro-edit, this change (`lightweight-generic@0.1.0`) | miss + 3 fallback scans, allowed (codegraph optional, warn) [measured] | 12 files [measured] | 1 attempt + 1 tool retry [measured] | 225 vs 400, chained N [measured] | n/a (no commands executed) [measured] | Y (forecast 60-150, Low, single PR in tasks.md) [measured] | branch `measure/t2-docs-clarity` from clean tree `7c6ea39`; window = acquire-to-settle history only; P6 nuance: forecast from SDD tasks discipline, not the liviano pack default (`tokenForecastRequired` false) |
| v0.2-pending | T1 | ERP-touching change, deferred (`erp-dotnet-angular@0.1.0`) | pending | pending | pending | pending | pending | pending | trigger: next genuine ERP contract/spec change; `.codegraph/` init at T1 with gitignore decision, index cost in T1 P1/P2 per #29-C4; no staged fill |
| v0.2-pending | T3 | no-harness control | n/a, fallback scans unbounded without ledger [narrated] | n/a, files re-read without record [narrated] | n/a, retries unlogged [narrated] | n/a, size estimated, chaining unknown [narrated] | n/a, nothing recorded [narrated] | n/a, forecast presence unknown [narrated] | counterfactual control: same change ad-hoc without harness; never counted, never measured |

Tag-audit scope: T1 `pending` cells claim no counter and carry no tag by design
(no fill exists to tag). The tag audit covers claimed cells only: every claimed
P-cell must carry exactly one tag; a claimed counter without a tag fails.

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

## Intent ledger (recorded in order, zero executed at root)

- Liviano (`lightweight-generic@0.1.0`): `npm test` -> `npm run lint`,
  failFast false.
- Executed at harness root: pack commands none (measurement-only git/grep/read
  ops only). Pushed to remote: nothing.

## Pins

- Core `gentle-ai@2.7.0`; team-4 single-writer / single-PR / 400-gate; liviano
  lens (`lightweight-generic@0.1.0`, codegraph optional, failFast false,
  `tokenForecastRequired` false); P1–P6 definitions per #29 steps 1–8; intents
  recorded in order; zero root executions; local-only.

## Sources (all read-only; archives untouched)

- Protocol/template: `archive/2026-09-17-foundryh-token-research/research.md`
  (section 5 template + steps 1–8) and v0.1 `baseline-fill.md` (tag-split
  precedent, 74-line P4 recount method).
- T2 edit: `PLANNING.md` (title orthography + proxy-counter disambiguation of
  the pending bullet) and `INFORMACION.md` (title orthography) on branch
  `measure/t2-docs-clarity`, liviano lens.
- Closed archives (`2026-09-17-foundryh-baseline-fill/`, token-research):
  read-only sources; never edited (verified via scoped git status/diff).

## v0.2 hold gate (D4)

- T2 data stays pending in this change dir. `baseline/v0.2` publication is
  BLOCKED until T1 is measured with passing tag, window, and branch evidence.
- T1 trigger watch documented only in this attempt — no T1 execution.
- T3 stays narrated indefinitely; no solicited T3 run.
