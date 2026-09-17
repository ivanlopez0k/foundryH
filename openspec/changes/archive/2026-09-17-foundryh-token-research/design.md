# Design: Foundry init v0 + sync baseline (Punto 3 + Punto 4)

## Technical Approach

Mirror `foundry.json` as the init contract, specify sync as a read-only comparator over pinned packs, and baseline as a local hand-filled counter table. Maps to proposal Approach-1 and specs `foundry-init` + `sync-baseline`. No runtime, no runner, no numerics.

## Architecture Decisions

| Option | Tradeoff | Decision |
|---|---|---|
| Init as doc-shaped writer/differ vs CLI binary | Binary needs runtime this repo lacks; docs fit declaration-only + wrapper (#17) | Writer/differ specified as contract shape only; execution delegates to gentle-ai@2.7.0 |
| Sync as comparator vs executable verifier | Executing intents at root violates no-synthesis rule (strict_tdd false) | Read-only compare: pinned-pack match + drift diff + harden-only verdict; never execute |
| Manual P1–P6 counters vs instrumented accounting | Instrumentation unparks OQ-4 prematurely, needs telemetry that does not exist | Manual `baseline/v0.1` table; OQ-4 stays parked, no token totals |
| Schema note-only vs new fields | New numeric fields break additive-only + invite invented savings | Only `description`/`$comment` notes; readers ignore unknown keys |

## Data Flow

    answers(2) ──→ writer ──→ foundry.json (pinned @0.1.0)
         │                        │
         └──── re-run ──→ differ ──┴── identical | versioned diff (confirm)
    ERP + liviano contracts ──→ sync checker ──→ match/drift + override verdict
    T1/T2/T3 runs ──→ ledgers/history ──→ baseline/v0.1 (counters only, local)

## File Changes

| File | Action | Description |
|---|---|---|
| `openspec/changes/foundryh-token-research/design.md` | Create | This decision record |
| `foundry.schema.json` | Modify | Notes for init/sync in `description`/`$comment` only; no new numerics |
| `foundry.json`, `foundry.liviano.example.json` | Reference | Canonical ERP/liviano outputs init must reproduce byte-for-byte |
| `openspec/changes/foundryh-token-research/baseline.md` | Create | Versioned T1/T2/T3 x P1–P6 template + collection protocol, local-only |

## Interfaces / Contracts

Writer input: `{stackQuestion: "erp-dotnet-angular"\|"lightweight-generic", teamSize: 4}` → contract with `packs.*@0.1.0`, `stackDetails{ codegraph, verification[], verificationPolicy.failFast, reviewFocus[] }`, `teamDetails{size, single-writer, small-prs-to-main}`, `budgetDetails{tokenForecastRequired}`, `init{stackQuestion, teamSize, versioned:true}`.

```json
{"differ": "identical | versioned-diff-requires-confirm", "sync": "match | drift-diff + override: pass | fail(key, needs exceptionId)"}
```

Baseline row: `| baseline/v0.1 | T-task | path | P1 hit+fallbacks | P2 files | P3 attempts | P4 size vs 400 + chained | P5 early-stop | P6 forecast | notes |` — counters or `n/a`, never token totals; no SAP rows.

Sync rules: `required` without index → fail with init hint; `optional` → warn and continue. Loosening override without `exceptionId` → fail naming key.

## Testing Strategy

| Layer | What to Test | Approach |
|---|---|---|
| Schema | `@0.1.0` pins, enums, `init.versioned:true` | JSON parse + pattern check by hand (Test-Json absent) |
| Parity | ERP exigent vs liviano cheap-path fields | Manual diff against reference contracts |
| E2E | None at root | Dry-fill one T1/T2/T3 row from history; verify no command executed, no push |

## Threat Matrix

N/A — no routing, shell, subprocess, VCS/PR automation, executable-file classification, or process-integration boundary. Intents are recorded in order, never executed; baseline stays local.

## Migration / Rollout

No migration required. Rollback: revert schema notes to `master@c166417`; delete unfilled baseline table; no remote mutation.

## Open Questions

None blocking. OQ-4 numeric model parked for v1 by design.
