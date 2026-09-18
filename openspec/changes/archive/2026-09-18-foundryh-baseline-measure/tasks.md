# Tasks: FoundryH Real-Counter Baseline v0.2

## Review Workload Forecast

| Field | Value |
|-------|-------|
| Estimated changed lines | 50–130 (T1-A slice only) |
| 400-line budget risk | Low |
| Chained PRs recommended | No |
| Suggested split | Single PR |
| Delivery strategy | ask-on-risk |
| Chain strategy | pending |

Decision needed before apply: No
Chained PRs recommended: No
Chain strategy: pending
400-line budget risk: Low

### Suggested Work Units

| Unit | Goal | Likely PR | Focused test command | Runtime harness | Rollback boundary |
|------|------|-----------|----------------------|-----------------|-------------------|
| 1 | T2 measured row pending + audits (done, 4190433) | PR 1 (single, done) | `grep -c "[measured]" baseline-v0.2-pending.md` | N/A — measurement-only, no runner | Delete change dir |
| 2 | T1-A candidate-A measured row + audits, D4 hold kept | PR 2 (single) | `grep -c "[measured]" baseline-v0.2-pending.md` | N/A — measurement-only, no runner (`strict_tdd: false`) | Checkout master, delete branch, restore foundry.json/.gitignore, drop local .codegraph/, no publish |

_Threat matrix: N/A per design (measurement-only) — no RED tasks._

## Phase 1: Clean Tree (D3)

- [x] 1.1 Commit or stash drifts/renames/untracked evidence; verify `git status` clean before branching
- [x] 1.2 Record baseline-fill archive state from `archive/2026-09-17-foundryh-token-research/research.md` (read-only); no archive edits

## Phase 2: T2 Collection

- [x] 2.1 Create T2 branch `measure/t2-docs-clarity` from clean tree, single-writer single-PR
- [x] 2.2 Apply genuine docs-clarity debt micro-edit on `PLANNING.md` and `INFORMACION.md` under `lightweight-generic@0.1.0`
- [x] 2.3 Create `openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md` with T2 P1–P6 counters, acquire-to-settle window, pins (`gentle-ai@2.7.0`), intent ledger; T1 `pending`, T3 `[narrated]`

## Phase 3: Audits and Hold Gate

- [x] 3.1 Tag audit: every P-cell exactly one tag; grep pending table for untagged cells, totals, SAP rows
- [x] 3.2 Window audit: hand-check ledger acquire/settle timestamps vs counted history; pre-acquire reads excluded
- [x] 3.3 Branch audit: `git branch`, `git status`, `git diff --numstat -- . ":!.atl" ":!.codegraph"` scoped and clean
- [x] 3.4 Enforce v0.2 hold: keep T2 pending in change dir; block `baseline/v0.2` publish until T1 measured

## Phase 4: T1 Deferral Plan (no execution)

- [x] 4.1 Document T1 trigger (next genuine ERP contract/spec change under `erp-dotnet-angular@0.1.0`) plus `.codegraph/` init plan with P1/P2 cost in pending notes
- [x] 4.2 Confirm `openspec/specs/sync-baseline/spec.md` (read-only) unchanged; v0.2 provenance rule deferred to publish

## Phase 5: T1-A Setup + Genuine Edit

- [x] 5.1 Verify D3 clean tree at 4190433 via git status; commit/stash drifts, keep .atl/ untracked-only
- [x] 5.2 Create branch measure/t1-erp-contract from clean master, single-writer single-PR
- [x] 5.3 Remove legacy stackDetails.notes line in `foundry.json`; keep canonical migrationCare.notes, schema-validate vs `foundry.schema.json:104-107` (read-only)
- [x] 5.4 Init `.codegraph/` in-window with `.gitignore` decision; charge index cost to T1 P1/P2 per #29-C4

## Phase 6: T1-A Collection + Audits + Hold

- [x] 6.1 Flip T1 pending→measured row in `baseline-v0.2-pending.md`: P1–P6 counters, window, pins, ledger
- [x] 6.2 Run tag audit (one tag/cell, counters-only), window audit (acquire-to-settle), branch audit (scoped numstat)
- [x] 6.3 Verify D4 hold (no baseline/v0.2 publish); confirm canonical `openspec/specs/sync-baseline/spec.md` (read-only) untouched
