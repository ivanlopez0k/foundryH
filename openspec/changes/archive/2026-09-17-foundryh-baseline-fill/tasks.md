# Tasks: Fill baseline/v0.1 with honest counters

## Review Workload Forecast

| Field | Value |
|-------|-------|
| Estimated changed lines | 60–90 (one new file) |
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
| 1 | Create tagged T1/T2/T3 `baseline-fill.md`, local-only | Single PR | `grep -c "\[measured\]\|\[reconstructed from #35\]\|\[narrated\]" baseline-fill.md` + manual tag checklist | N/A — declaration-only fill, no runner synthesis, intents recorded not executed | Delete `openspec/changes/foundryh-baseline-fill/baseline-fill.md` |

## Phase 1: Recount sources

- [x] 1.1 Recount T2 P4 as 74 lines (64+10) via `wc -l` on `openspec/changes/archive/2026-09-17-foundryh-token-research/baseline.md` (read-only) and `git diff --stat` on `foundry.schema.json` (read-only)
- [x] 1.2 Confirm T2 P6 forecast present by grepping forecast in `openspec/changes/foundryh-baseline-fill/specs/sync-baseline/spec.md` (read-only); confirm P5 zero executions observed

## Phase 2: Create fill

- [x] 2.1 Create `openspec/changes/foundryh-baseline-fill/baseline-fill.md` with T1/T2/T3 table where each P1–P6 cell carries exactly one tag
- [x] 2.2 Fill T1 as same-harness ERP-lens proxy in `openspec/changes/foundryh-baseline-fill/baseline-fill.md`: P1 miss = policy VIOLATION + init hint, Notes state `same-harness proxy`
- [x] 2.3 Fill T2 verified row in `openspec/changes/foundryh-baseline-fill/baseline-fill.md`: P4 `74 vs 400, chained N [measured]`, P1 miss allowed with warn, P4/P5/P6 `[measured]`, P1/P2/P3 `[reconstructed from #35]`
- [x] 2.4 Narrate T3 control in `openspec/changes/foundryh-baseline-fill/baseline-fill.md`: all cells `[narrated]`, counters `n/a` or estimated, never measured; add intent ledger (ERP → liviano order, zero executed) + sources (#35/#36, git diff)

## Phase 3: Verify

- [x] 3.1 Verify every P-cell has exactly one tag, no token totals, no SAP rows in `openspec/changes/foundryh-baseline-fill/baseline-fill.md`
- [x] 3.2 Verify local-only: `git status` shows only `openspec/changes/foundryh-baseline-fill/baseline-fill.md` as new; `openspec/changes/archive/2026-09-17-foundryh-token-research/baseline.md` (read-only) and `foundry.schema.json` (read-only) untouched; no push
