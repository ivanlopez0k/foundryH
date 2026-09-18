# Proposal: FoundryH Real-Counter Baseline v0.2 — T1 Work-Unit

## Intent

Complete the second real-counter row: flip T1 `pending` to `[measured]` P1–P6 via one genuine ERP contract edit (candidate A). Targets ERP exigent pack `erp-dotnet-angular@0.1.0`. Closes the OQ-4 input pair with landed T2 (`4190433`); no savings claim.

## Scope

### In Scope
- Remove legacy `stackDetails.notes` (`foundry.json:20`); keep `migrationCare.notes` canonical per `foundry.schema.json:104-107`.
- Init `.codegraph/` at T1 with `.gitignore` decision; index cost in T1 P1/P2 per #29-C4.
- Flip T1 row `pending→measured` (P1–P6, acquire-to-settle window, pins, ledger) in `baseline-v0.2-pending.md:22`.
- Tag, window, branch audits; clean tree + one branch + scoped numstat.

### Out of Scope
- Candidate B hint wording; candidate C PLANNING scope.
- `baseline/v0.2` publish step (separate, after both-row hand-check).
- Token totals, SAP rows, T3 solicited run, push.

## Capabilities

### New Capabilities
- None — measurement only.

### Modified Capabilities
- None — `sync-baseline` / `foundry-init` unchanged; v0.2 fills existing table.

## Approach

Acquire-to-settle only; pre-acquire reads excluded. Pins: `gentle-ai@2.7.0` + `erp-dotnet-angular@0.1.0`, team-4 single-writer/single-PR/400-gate, same P1–P6 definitions. Reference search forces miss-then-init (T1/T2 P1 contrast). Ledger (`dotnet test → ng test → ng lint`) in order, never executed at root. One tag per P-cell; counters only. D4 hold until hand-checks pass.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `foundry.json:20` | Modified | Remove legacy notes line |
| `foundry.schema.json:104-107` | Reference | Canonical-notes rule, read-only |
| `.codegraph/` + `.gitignore` | New/Modified | Init at T1; ignore decision |
| `openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md:22` | Modified | T1 pending→measured |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Search stalls without index | Med | Init in-window; cost in P1/P2 |
| Ledger noise outside window | Med | Strict acquire-to-settle cutoff |
| Dirty tree contaminates counts | Low | D3 clean tree; scoped numstat |
| T1 judged staged | Low | Live ERP contract edit; branch evidence |

## Rollback Plan

`git checkout master; git branch -D measure/t1-erp-contract`; restore `foundry.json` / `.gitignore`; delete `.codegraph/` if local-only; revert T1 row edits. Archives, schema, specs untouched. No push.

## Dependencies

- #29 protocol/template + #50 explore (candidate A); T2 row `4190433`.
- Core `gentle-ai@2.7.0`; clean tree per D3; local-only, no push.

## Success Criteria

- [ ] Legacy line removed, canonical notes intact, schema-valid contract
- [ ] T1 P1–P6 `[measured]` or honest miss, one tag per cell, counters only
- [ ] Window, pins, ledger, branch evidence auditable; D4 hold respected
