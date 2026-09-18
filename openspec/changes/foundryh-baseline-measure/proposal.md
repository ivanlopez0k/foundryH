# Proposal: FoundryH Real-Counter Baseline v0.2

## Intent

Replace v0.1 reconstructed/narrated proxies with real `[measured]` P1–P6 counters from two fresh genuine edits; publishable `baseline/v0.2` as OQ-4 input, no savings claim.

## Scope

### In Scope
- T2-now: docs-clarity micro-task on PLANNING.md / INFORMACION.md debt, liviano lens; full P1–P6 count, apply-window rule.
- T1-deferred: next genuine ERP-touching change (contract/spec) under ERP lens; no staged T1.
- `.codegraph/` init at T1 with gitignore decision; index cost in P1/P2 per #29-C4.
- Clean tree first, one branch per row, scoped numstat excluding `.atl/`, `.codegraph/`.

### Out of Scope
- Staged T1; solicited T3 (T3 narrated-only indefinitely).
- Token totals, OQ-4 model, SAP rows, closed-archive edits, push.
- v0.2 publication before both rows land (D4 hold).

## Capabilities

### New Capabilities
- None — measurement only.

### Modified Capabilities
- None — `sync-baseline` / `foundry-init` unchanged; v0.2 fills existing table.

## Approach

Hybrid D1–D5; reuse #29 steps 1–8 and P1–P6 template. T2 now; T1 on next genuine ERP change. Per row: clean tree (commit/stash renames, 35/3 drift, untracked evidence), one branch, window = acquire-to-settle history only. Pins: `gentle-ai@2.7.0`, team-4 single-writer/single-pr/400-gate, same collector and counter definitions, intents in order, zero root executions. T2 stays pending until T1 lands; then publish v0.2.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `PLANNING.md`, `INFORMACION.md` | Modified | T2 target |
| `foundry.json` / ERP specs | Modified | Deferred T1 target |
| `openspec/changes/foundryh-baseline-measure/` | New | v0.2 collection (pending) |
| `openspec/specs/sync-baseline/spec.md` | Modified | Later: v0.2 provenance rule |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| T2 too trivial → P2/P4 bias | Med | Keep genuine debt; exact size |
| Ledger noise outside window | Med | Strict acquire-to-settle cutoff |
| Dirty tree contaminates counts | Med | D3 clean-tree + scoped numstat |
| P1 miss without index | High | D2: index at T1; tag T2 honestly |
| P5 n/a (no harness runner) | High | n/a `[measured]`; intents only |
| Closed-archive drift | Low | Read-only sources; no archive edits |

## Rollback Plan

Delete `openspec/changes/foundryh-baseline-measure/`; archives, schema, specs untouched. Pending T2 data goes with the dir.

## Dependencies

- #29 + `archive/2026-09-17-foundryh-token-research/research.md` (protocol/template); v0.1 `baseline-fill.md`
- Core `gentle-ai@2.7.0`; clean tree per D3

## Success Criteria

- [ ] T2 P1–P6 `[measured]` (liviano); T1 pending, no staged fill
- [ ] Every cell one tag; counters only, no totals/SAP rows
- [ ] Windows, pins, zero-execution ledger auditable; validator-ready
