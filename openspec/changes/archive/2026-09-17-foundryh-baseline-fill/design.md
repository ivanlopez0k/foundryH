# Design: Fill baseline/v0.1 with honest counters

## Technical Approach

Approach 1 (recount-in-place + narrated control, per explore #39). Reuse #29 protocol steps 1-8 and the P1-P6 template. T1 reinterprets the same schema-note run under the ERP lens as a labeled same-harness proxy; T2 verifies the dry-fill against git/Engram; T3 is prose-only counterfactual. Every P1-P6 cell carries exactly one tag: `[measured]`, `[reconstructed from #35]`, or `[narrated]`. Counters only; no token totals, no SAP rows, no archive edit, no runner synthesis, local-only.

## Architecture Decisions

| Option | Tradeoff | Decision |
|--------|----------|----------|
| T1 as same-run ERP-lens proxy vs fresh ERP re-enactment | Fresh run is cleaner but biased (agent knows codebase), churns files for no gain in a declaration-only repo | Same-run proxy, Notes state `same-harness proxy`; P1 miss = policy VIOLATION (codegraph `required`, fail with init hint) |
| T2 P1 miss allowed vs violation | ERP requires, liviano (`optional`) only warns | T2 miss allowed with warn; record P6 Y nuance: forecast came from SDD tasks.md discipline, not the liviano pack default (`forecast false`) |
| T3 estimated numbers vs narrated-only | Numbers complete the table but would be invented (no ledger) | Narrated-only; counters `n/a` or `estimated`, all cells `[narrated]`, never presented as measured |
| Tag source split | Uniform `[measured]` overclaims (tool history gone); uniform `[reconstructed]` underclaims verifiable lines | Split: P4/P5/P6 `[measured]` (wc/git/tasks.md), P1/P2/P3 `[reconstructed from #35]`, all T3 `[narrated]` |

## Data Flow

```
archive baseline.md (read-only) + git diff + Engram #35/#36
  ──→ recount (T1 proxy / T2 verify) + narrate (T3)
    ──→ baseline-fill.md (new, tagged table, local-only)
```

P4 recount: `wc -l` (64-line archive file) + `git diff --stat` (5 ins/5 del schema) = 74 lines (64+10). P5: zero executions observed. P6: `tasks.md` forecast 80-120 present.

## File Changes

| File | Action | Description |
|------|--------|-------------|
| `openspec/changes/foundryh-baseline-fill/design.md` | Create | This design |
| `openspec/changes/foundryh-baseline-fill/baseline-fill.md` | Create (apply) | Tagged T1/T2/T3 table + intent ledger + sources |
| `openspec/changes/foundryh-baseline-fill/specs/sync-baseline/spec.md` | Modified (done) | Provenance-tag rule delta |
| `openspec/changes/archive/2026-09-17-foundryh-token-research/baseline.md` | Unchanged | Read-only source, never edited |
| `foundry.schema.json` | Unchanged | Read-only P4 recount source |

## Interfaces / Contracts

Table schema per row: `| v0.1 | T{1,2,3} | path/harness | P1 | P2 | P3 | P4 | P5 | P6 | Notes |` where each P-cell = `counter-or-n/a + exactly-one-tag`. T1 Notes include `same-harness proxy`; T3 Notes are prose gaps (unbounded re-reads, unlogged retry, possible intent-not-runner violation).

## Testing Strategy

| Layer | What to Test | Approach |
|-------|-------------|----------|
| Unit | P4 = 74 (64+10); P6 forecast present | `wc -l`, `git diff --stat`, grep `tasks.md` for forecast |
| Integration | Every cell has exactly one tag; no token totals; no SAP rows | Manual review checklist on `baseline-fill.md` |
| E2E | Archive untouched; nothing pushed | `git status` shows new files only in this change; no remote op |

## Threat Matrix

N/A — no routing, shell, subprocess, VCS/PR automation, executable-file classification, or process-integration boundary.

## Migration / Rollout

No migration required. Rollback: delete `openspec/changes/foundryh-baseline-fill/`; archive, schema, specs untouched. Local-only; user pushes from own terminal.

## Open Questions

- None blocking. OQ-4 (token totals) stays parked by design.
