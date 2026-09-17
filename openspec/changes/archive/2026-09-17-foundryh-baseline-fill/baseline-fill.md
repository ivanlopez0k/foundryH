---
baseline: v0.1
change: foundryh-baseline-fill
local_only: true
---

# Baseline v0.1 fill: tagged T1/T2/T3 counters

Scope guards (read before using): every P1–P6 cell holds a counter or
`n/a` with exactly one provenance tag. Counters only — no token totals.
No SAP/servicios rows (out of scope). Pack verification strings are
downstream intents: record them in run order, never execute them at the
harness root. This file stays local: no push, no remote mutation, no
archive edit, no schema edit.

## Counter table

| Baseline | Task | Path / harness | P1 hit+fallbacks | P2 files | P3 attempts | P4 size vs 400 + chained | P5 early-stop | P6 forecast | Notes |
|---|---|---|---|---|---|---|---|---|---|
| v0.1 | T1 | ERP reference proxy (`erp-dotnet-angular@0.1.0`) | miss + 6 fallback scans, policy VIOLATION (codegraph required, fail with init hint) [reconstructed from #35] | 8 files [reconstructed from #35] | 1 attempt + 1 tool retry [reconstructed from #35] | 74 vs 400, chained N [measured] (64 new + 10 changed) | n/a (no commands executed) [measured] | Y (forecast 80-120, Low, single PR in tasks.md) [measured] | same-harness proxy: same schema-note run reinterpreted under ERP lens; P1 miss is a policy VIOLATION under required codegraph |
| v0.1 | T2 | liviano-style docs change, this change (`lightweight-generic@0.1.0` analogue) | miss + 6 fallback scans, allowed (codegraph optional, warn) [reconstructed from #35] | 8 files [reconstructed from #35] | 1 attempt + 1 tool retry [reconstructed from #35] | 74 vs 400, chained N [measured] (64 new + 10 changed) | n/a (no commands executed) [measured] | Y (forecast 80-120, Low, single PR in tasks.md) [measured] | dry-fill from SDD history of this change; P6 Y nuance: forecast came from SDD tasks.md discipline, not the liviano pack default (forecast false); counters only |
| v0.1 | T3 | no-harness control | n/a, fallback scans unbounded without ledger [narrated] | n/a, files re-read without record [narrated] | n/a, retries unlogged [narrated] | n/a, size estimated, chaining unknown [narrated] | n/a, nothing recorded [narrated] | n/a, forecast presence unknown [narrated] | counterfactual control: same change ad-hoc without harness; unbounded re-reads, unlogged retry, possible intent-not-runner violation; never counted |

## Intent ledger (recorded in order, zero executed at root)

- ERP (`erp-dotnet-angular@0.1.0`): `dotnet test` -> `ng test` -> `ng lint`.
- Liviano (`lightweight-generic@0.1.0`): `npm test` -> `npm run lint`.
- Executed at harness root: none. Pushed to remote: nothing.

## Sources

- P1: no codegraph index consulted; 6 fallback scans (2 dir listings,
  1 glob, 3 text scans) per Engram #35; T1 reuses the same run as a
  same-harness proxy under the ERP lens, so the identical miss becomes a
  policy VIOLATION there and an allowed warn under liviano optional.
- P2: 8 distinct files read (tasks, design, proposal, 2 specs, schema,
  2 contracts) per Engram #35.
- P3: 1 work-unit attempt; 1 tool retry (edit whitespace mismatch,
  recovered) per Engram #35.
- P4: 74 changed lines vs 400, chained N — 64 new (archive baseline.md
  line count via file read) + 10 changed (5 schema description lines,
  insertion + deletion counted, commit cdb4c6e numstat 5/5). Recount
  commands: file line read on the archive baseline plus git show numstat
  on foundry.schema.json; both sources read-only, neither edited.
- P5: n/a — declaration-only repo, no verification command executed;
  zero executions observed per Engram #36.
- P6: Y — workload forecast present in tasks.md before apply
  (80-120, Low, single PR); the tag split records this cell as measured
  from tasks.md, with the nuance that the forecast came from SDD
  discipline rather than the liviano pack default.
- T3: no ledger exists for the ad-hoc run; all T3 cells are prose-only
  counterfactual with counters n/a or estimated, never counted.
