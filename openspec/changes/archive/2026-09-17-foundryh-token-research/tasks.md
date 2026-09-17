---
schema: gentle-ai.sdd-tasks/v1
revision: 1
change: foundryh-token-research
artifact_store_mode: hybrid
delivery_strategy: ask-on-risk
---

# Tasks: Foundry init v0 + sync baseline

## Review Workload Forecast

| Field | Value |
|-------|-------|
| Estimated changed lines | 80–120 |
| 400-line budget risk | Low |
| Chained PRs recommended | No |
| Suggested split | single PR |
| Delivery strategy | ask-on-risk |
| Chain strategy | pending |

Decision needed before apply: No
Chained PRs recommended: No
Chain strategy: pending
400-line budget risk: Low

### Suggested Work Units

| Unit | Goal | Likely PR | Focused test command | Runtime harness | Rollback boundary |
|------|------|-----------|----------------------|-----------------|-------------------|
| 1 | Schema notes + baseline template + dry-fill verified | PR 1 (single) | Hand-check: JSON parse + `@0.1.0` pin + parity diff (no runner, strict_tdd false) | N/A — declaration-only repo; dry-fill from history, never execute intents at root | Revert `foundry.schema.json` notes; delete `openspec/changes/foundryh-token-research/baseline.md` if unfilled |

## Phase 1: Schema notes (foundation)

- [x] 1.1 Add init/sync notes to `foundry.schema.json` via `description`/`$comment` only; no new fields, no numerics.
- [x] 1.2 Hand-check `foundry.schema.json` parses, keeps `@0.1.0` pins and `init.versioned:true`.

## Phase 2: Baseline template + parity (core)

- [x] 2.1 Create `openspec/changes/foundryh-token-research/baseline.md` with `baseline/v0.1` T1/T2/T3 x P1-P6 template + hand-collection protocol, counters-or-`n/a`, local-only.
- [x] 2.2 Parity-check `foundry.json` (read-only) vs `foundry.liviano.example.json` (read-only): ERP exigent vs liviano cheap-path fields match spec.

## Phase 3: Hand-check verification (no runner)

- [x] 3.1 Dry-fill one T1/T2/T3 row in `openspec/changes/foundryh-token-research/baseline.md` from history; counters only, no token totals, no SAP row.
- [x] 3.2 Verify intents recorded in order with zero execution at root and no push from `openspec/changes/foundryh-token-research/baseline.md`.

## Phase 4: Docs polish

- [x] 4.1 Confirm `openspec/changes/foundryh-token-research/design.md` (read-only) scope guard holds: additive-only, no numerics, no runner, no SAP, no push.
