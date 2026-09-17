---
baseline: v0.1
change: foundryh-token-research
local_only: true
---

# Baseline v0.1: same-harness proxy counters (T1/T2/T3 x P1-P6)

Scope guards (read before filling): every P1-P6 cell holds a counter or
`n/a` — never a token total. No SAP/servicios rows (OQ-10 out of scope).
Pack verification strings are downstream intents: record them in run order,
never execute them at the harness root. This file stays local: no push, no
remote mutation. OQ-4 numeric token model stays parked for v1 by design.

## Tasks

- T1 (ERP reference): same change applied under `erp-dotnet-angular@0.1.0`
  (codegraph `required`, failFast true).
- T2 (liviano change): same change applied under
  `lightweight-generic@0.1.0` (codegraph `optional`, failFast false).
- T3 (no-harness control): same change applied ad-hoc, without the harness.

## Proxies

- P1: graph-first hit + fallback scans (codegraph hit Y/N, then scan count).
- P2: files read (distinct files opened to implement the change).
- P3: attempts/retries (work-unit attempts, then tool retries).
- P4: PR size vs 400 + chained Y/N (changed lines, single vs chained).
- P5: early-stop (failFast stop Y/N, or `n/a` when nothing executed).
- P6: forecast Y/N (was a token forecast required and present).

## Hand-collection protocol

1. Open the tool history and the attempt ledger for the T-task run.
2. Fill each P1-P6 cell with a counter or `n/a`; never derive token totals.
3. Copy pack verification strings into the intent ledger below, in run order.
4. Execute nothing at the harness root; keep this file local (no push).
5. Narrate T3 gaps (fallback scans, files read, unlogged retries) in notes.

## Counter table

| Baseline | Task | Path / harness | P1 hit+fallbacks | P2 files | P3 attempts | P4 size vs 400 + chained | P5 early-stop | P6 forecast | Notes |
|---|---|---|---|---|---|---|---|---|---|
| v0.1 | T1 | ERP reference (`erp-dotnet-angular@0.1.0`) | n/a (uncollected in this slice) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | Collect per protocol before v1 |
| v0.1 | T2 | liviano-style docs change, this change (`lightweight-generic@0.1.0` analogue) | miss (no index consulted) + 6 fallback scans | 8 files | 1 attempt + 1 tool retry | 74 lines vs 400, chained N (64 new + 10 changed) | n/a (no commands executed) | Y (forecast 80-120, Low, single PR in tasks.md) | Dry-fill from SDD history of this change; counters only |
| v0.1 | T3 | no-harness control | n/a (uncollected in this slice) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | n/a (uncollected) | Narrate fallback/file/retry gaps when collected |

## Intent ledger (recorded in order, zero executed at root)

- ERP (`erp-dotnet-angular@0.1.0`): `dotnet test` -> `ng test` -> `ng lint`.
- Liviano (`lightweight-generic@0.1.0`): `npm test` -> `npm run lint`.
- Executed at harness root: none. Pushed to remote: nothing.

## T2 dry-fill sources (this change, SDD history)

- P1: no codegraph index consulted; 6 fallback scans (2 dir listings,
  1 glob, 3 text scans).
- P2: 8 distinct files read (tasks, design, proposal, 2 specs, schema,
  2 contracts).
- P3: 1 work-unit attempt; 1 tool retry (edit whitespace mismatch, recovered).
- P4: 74 changed lines vs 400, chained N — 64 new (this file) + 10 changed
  (5 schema description lines, insertion + deletion counted).
- P5: `n/a` — declaration-only repo, no verification command executed.
- P6: Y — workload forecast present in tasks.md before apply.
