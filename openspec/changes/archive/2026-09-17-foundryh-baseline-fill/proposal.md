---
schema: gentle-ai.sdd-proposal/v1
revision: 1
change: foundryh-baseline-fill
artifact_store_mode: hybrid
pack_targets: [erp-dotnet-angular@0.1.0, lightweight-generic@0.1.0]
---

# Proposal: Fill baseline/v0.1 with honest counters

## Intent

Prove saving honestly: recount T1/T2 from archived SDD history with per-cell provenance, narrate T3 as counterfactual without invented numbers. Validates user model: shared ordering (pinned `@0.1.0` packs, versioned 2-question init, sync harden-only check) makes individual T1/T2 counters comparable; without sync they are incomparable.

## Scope

### In Scope
- T1 recount: same schema-note run under ERP lens, labeled same-harness proxy
- T2 verify: dry-fill cells against git/Engram, fix P4 to 74 lines (64+10)
- T3 narrate: counterfactual gaps only, never counted
- New files only in this change; reuse #29 protocol steps 1-8, P1-P6 template

### Out of Scope
- Token totals (OQ-4 parked), SAP rows, archive edits
- Runner synthesis, push, Approach 2/3 fresh runs, v0.2

## Capabilities

### New Capabilities
- None — fill only, no new behavior

### Modified Capabilities
- `sync-baseline`: add provenance-tag rule (measured/reconstructed/narrated) to Versioned Proxy Baseline cells

## Approach

Approach 1 recount-in-place (explore #39): every P1-P6 cell tagged `[measured]` (P4/P5/P6 via wc/git/tasks.md), `[reconstructed from #35]` (P1 6 scans, P2 8 files, P3 1+1), `[narrated]` (all T3). T1 ERP-lens: P1 miss = policy VIOLATION (required, fail with init hint). T2 liviano: same miss allowed (optional, warn); P6 Y nuance recorded (forecast from SDD discipline, not pack default).

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `openspec/changes/foundryh-baseline-fill/baseline-fill.md` | New | Provenance-tagged T1/T2/T3 table, local-only |
| `openspec/changes/archive/2026-09-17-foundryh-token-research/baseline.md` | Unchanged | Read-only source, never edited |
| `openspec/specs/sync-baseline/spec.md` | Modified (delta) | Provenance-tag requirement for P1-P6 cells |
| `foundry.schema.json` | Unchanged | Read-only P4 recount source (5/5 lines) |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| T1 misread as independent ERP run | High | Notes state same-harness proxy |
| Reconstructed cells read as observed | Med | Tag every cell; cite #35/#36 |
| T3 numbers invented | Med | Narrative only, counters n/a or estimated |
| Token totals derived | Low | Counters-only guard; OQ-4 parked |

## Rollback Plan

Delete `openspec/changes/foundryh-baseline-fill/`; archive, schema, and specs untouched; no remote mutation; user pushes only from own terminal.

## Dependencies

- #29 protocol, #35/#36 provenance, #31/#32/#33 archived contract; gentle-ai@2.7.0, Engram + openspec hybrid trail

## Success Criteria

- [ ] T1/T2 cells filled with provenance tags; T3 narrated, none counted
- [ ] P4 corrected to 74 lines; no token totals, no SAP rows, no archive edit
- [ ] Spec delta for provenance tags ready for sdd-spec
