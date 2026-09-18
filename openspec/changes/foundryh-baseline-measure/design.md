# Design: FoundryH Real-Counter Baseline v0.2

## Technical Approach

Measurement only — no behavior change. Collect real `[measured]` P1–P6 counters from two genuine edits (T2 docs-clarity now, T1 ERP-touching later) reusing protocol #29 steps 1–8 and the P1–P6 template. T2 lands as `pending`; `baseline/v0.2` publishes only when both rows are measured (D4 hold). T3 stays narrated-only.

## Architecture Decisions

| Option | Tradeoff | Decision |
|--------|----------|----------|
| T2 window: acquire-to-settle history vs whole session | Whole session is easier but pollutes counts with pre-acquire reads | Acquire-to-settle only; pre-acquire reads excluded, window re-checkable from ledger timestamps |
| Honest miss vs forced `[measured]` | Forcing all-measured overclaims (P1 miss likely without index; P5 n/a with no runner) | Every cell carries exactly one tag; miss recorded as `miss`/`n/a [measured]` with reason (e.g. T2 P1 optional-warn, P5 no-harness-runner) |
| T1 now (staged) vs deferred to genuine ERP change | Staged is fast but synthetic — violates the "real counter" goal | T1 stays `pending`; trigger is the next genuine ERP-touching change (contract/spec) under `erp-dotnet-angular@0.1.0`, same window/pins/ledger discipline |
| `.codegraph/` init now vs at T1 | Init now simplifies T2 but charges index cost to the wrong row | Init at T1 with gitignore decision; index cost counts in T1 P1/P2 per #29-C4 |
| Publish T2 alone vs D4 hold gate | Single-row publish is tempting but breaks the OQ-4 input contract | D4 hold: no `baseline/v0.2` publication until both rows pass the hand-check (tag + window + branch evidence) |

Rules applied: `rules.design` (decisions with rationale; harden-only, no overrides touched).

## Data Flow

```
T2 branch (docs edit) ──→ attempt ledger + tool history ──→ pending table (T2 measured, T1 pending, T3 narrated)
T1 branch (ERP edit, later) ──→ ledger + history (+ codegraph index cost) ──→ pending table (both rows measured)
pending table + hand-checks pass ──→ publish baseline/v0.2 (OQ-4 input, no savings claim)
```

Pins per row: `gentle-ai@2.7.0`, team-4 single-writer/single-PR/400-gate, same P1–P6 definitions, intents recorded in order, zero executions at harness root, local-only.

## File Changes

| File | Action | Description |
|------|--------|-------------|
| `openspec/changes/foundryh-baseline-measure/design.md` | Create | This design (design phase) |
| `openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md` | Create (apply) | Pending table: T2 measured row, T1 `pending`, T3 narrated, intent ledger, sources |
| `openspec/specs/sync-baseline/spec.md` | Modify (at publish, not apply) | Later v0.2 provenance rule once both rows land |
| `PLANNING.md`, `INFORMACION.md` | Modify (T2 branch) | Genuine docs-clarity debt edit, one branch, clean tree first |
| `.codegraph/` | Create (at T1) | Index init with gitignore decision; cost in T1 P1/P2 |

Rollback: delete `openspec/changes/foundryh-baseline-measure/`; archives, schema, specs untouched.

## Interfaces / Contracts

Row schema (unchanged from #29 template): `| baseline | task | path/harness | P1 | P2 | P3 | P4 | P5 | P6 | notes |` where each P-cell = `counter-or-n/a + exactly-one-tag` (`[measured]` or honest miss with reason; T3 always `[narrated]`). Scoped diff excludes noise:

```
git diff --numstat -- . ":!.atl" ":!.codegraph"
```

## Testing Strategy

| Layer | What to Test | Approach |
|-------|-------------|----------|
| Tag audit | Every P-cell has exactly one tag; no totals/SAP rows | `grep` pending table for untagged cells and banned tokens |
| Window audit | Only acquire-to-settle history counted | Hand-check ledger timestamps vs counted tool history |
| Branch audit | One branch per row, clean tree, scoped scope | `git branch`, `git status`, scoped numstat above |

No runner exists (`strict_tdd: false`, harness-declaration repo); verification is hand-checks only.

## Threat Matrix

N/A — no routing, shell, subprocess, VCS/PR automation, executable-file classification, or process-integration boundary. Measurement-only change; pack strings stay intents, never executed.

## Migration / Rollout

No migration required. No flags, no phased rollout. Publish `baseline/v0.2` only after both rows pass; T2 waits pending until T1 lands.

## Open Questions

- None blocking. T2 exact debt slice is chosen at apply from a clean tree.
