---
schema: gentle-ai.sdd-proposal/v1
revision: 1
change: foundryh-token-research
artifact_store_mode: hybrid
pack_targets: [erp-dotnet-angular@0.1.0, lightweight-generic@0.1.0]
---

# Proposal: Foundry init v0 + sync baseline (Punto 3 + Punto 4)

## Intent

Close the v0 harness loop: init writes a reproducible contract and sync proves same-harness behavior via counted proxies, without invented token savings.

## Scope

### In Scope
- Init v0 contract: codegraph policy, verification intents, reviewFocus order, forecast flag, team size/mode, 2 versioned questions, idempotence with diff
- Sync v0: same-harness verification + pinned-pack check + harden-only override check
- Baseline v0.1 table T1 ERP / T2 liviano / T3 no-harness with proxies P1–P6 + collection protocol

### Out of Scope
- Numeric token model/limits (OQ-4 parked for v1)
- Instrumented per-phase accounting (Approach 2, v1)
- SAP/servicios instances, sub-stack/roles/rotating-mode questions
- Workspace runner synthesis, remote push

## Capabilities

### New Capabilities
- `foundry-init`: what init writes, idempotence with diff, 2 questions
- `sync-baseline`: same-harness sync verification + versioned proxy baseline collection

### Modified Capabilities
- None — `openspec/specs/` empty; 400-line gate stays in immutable core, not re-declared.

## Approach

Adopt Approach-1 evidence: init mirrors the foundry.json field set; sync diffs versioned packs; baseline manually counts P1 CodeGraph hits, P2 files read, P3 attempts, P4 PR size vs 400, P5 failFast stops, P6 forecast on T1/T2/T3.

## Affected Areas

| Area | Impact | Description |
|------|--------|-------------|
| `foundry.json`, `foundry.liviano.example.json` | Modified | Init contract source of truth (ERP exigent + liviano) |
| `foundry.schema.json` | Modified | Document init/sync without token numerics |
| `openspec/changes/foundryh-token-research/specs/` | New | Delta specs for foundry-init, sync-baseline |
| `openspec/changes/foundryh-token-research/baseline.md` | New | Versioned T1/T2/T3 table, local-only |

## Risks

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Invented numeric savings | Med | Counters only; OQ-4 parked; table forbids token totals |
| Runner synthesis from intents | Med | strict_tdd false; intents never execute at root |
| SAP/drift corrupts baseline | Low | Pin @0.1.0; harden-only + exceptionId; table local |

## Rollback Plan

Revert init/sync docs and schema notes to `master@c166417`; delete unfilled baseline table; no remote mutation; user pushes only from own terminal.

## Dependencies

- gentle-ai@2.7.0 wrapper (no fork); CodeGraph/attempt/review commands; Engram + openspec hybrid trail

## Success Criteria

- [ ] Init writes exactly declared fields, idempotent with diff, 2 questions
- [ ] Sync verifies same packs on ERP + liviano; T1/T2/T3 template collectible by hand
- [ ] No schema numerics, no runner, no SAP, no push
