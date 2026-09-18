---
schema: gentle-ai.sdd-archive-report/v1
revision: 1
change: foundryh-baseline-measure
artifact_store_mode: openspec
archived_to: openspec/changes/archive/2026-09-18-foundryh-baseline-measure/
date_utc: 2026-09-18
verdict_at_close: CLEAN CLOSE (verify PASS, D4 released by explicit user approval, zero CRITICAL)
---

# Archive Report — foundryh-baseline-measure (baseline/v0.2 real-counter close)

## 1. Close verdict

**CLEAN CLOSE.** The change completed the full SDD cycle: proposal →
spec (delta) → design → tasks → apply (18/18 cumulative: T2 11/11 +
T1-A 7/7) → verify (PASS) → publish `baseline/v0.2` (D4 released by
explicit user approval) → spec sync (native compose) → archive. No
CRITICAL issue ever existed; the three SUGGESTIONs in `verify-report`
are non-blocking notes left as-is for archive fidelity (no code
changes after verify, no new blockers). Per the Final-State Authority
hierarchy, this report records state AT CLOSE and cites the
orchestrator handoff facts below; it does not echo intermediate
`apply-progress` / `verify-report` snapshots as current facts.

## 2. Final-state facts (authoritative at close, orchestrator handoff outranks snapshots)

- Apply T1-A complete 18/18 tasks (T2 11/11 + T1 7/7) on branch
  `measure/t1-erp-contract` from base `4190433`, local-only, uncommitted
  by design. Genuine edit: `foundry.json` 1+/2- (legacy
  `stackDetails.notes` removed, `migrationCare.notes` canonical intact,
  schema-valid) + `.gitignore` 3+/0 (`.codegraph/` gitignored,
  local-only) + `baseline-v0.2-pending.md` 50+/5- (T1 P4 184 vs 400
  measured, T2 P4 225 intact, T3 narrated). P4 actual 184/400 Low,
  single PR, no split, no exception. Spot-check parent ok, risk medium,
  writer self-verification sufficient.
- Verify PASS: 18/18 tasks, 4 requirements / 7 scenarios compliant by
  hand-check, design coherent, additive-only, archives/schema/canonical
  untouched at verification time, D4 hold respected (no `baseline/v0.2`
  published yet at that moment). `verify-report.md` hash
  `sha256:1309462a8f135eb8cad58bf924b8585e0c4a515cb9d55dae034e13a26a78fbb7`
  (confirmed at archive time). Three non-blocking suggestions in report.
- Ledgers settled complete: `t1-apply-20260918-01` passed (evidence
  `de7c109c9351ca38676705a521eacf3c15af3b598fe24b25874a066e9ebaedfa`,
  = SHA256 of `baseline-v0.2-pending.md`, confirmed),
  `t1-verify-20260918-01` passed. No reset pending.
- User approved "Publicar y archivar": publish `baseline/v0.2` with both
  rows (D4 release unlocked, both rows with tag/window/branch evidence),
  then archive. Publish executed as new file `baseline-v0.2.md` derived
  from pending with both rows, no totals/SAP, no savings claim (section 5).
- Commits only on explicit request: ZERO commits and ZERO pushes in this
  phase. Head remains `4190433`; commit/merge/push stay user-owned from
  their own terminal (T2 `4190433` pattern).

## 3. Task Completion Gate — PASS

Persisted tasks artifact
(`openspec/changes/archive/2026-09-18-foundryh-baseline-measure/tasks.md`)
shows 18/18 `[x]`, zero unchecked implementation tasks (probed:
`- [ ]` count 0, `- [x]` count 18):

- Phase 1 (D3 clean tree): 1.1, 1.2 — done
- Phase 2 (T2 collection): 2.1, 2.2, 2.3 — done (landed as `4190433`)
- Phase 3 (audits + hold): 3.1, 3.2, 3.3, 3.4 — done
- Phase 4 (T1 deferral plan): 4.1, 4.2 — done
- Phase 5 (T1-A setup + genuine edit): 5.1, 5.2, 5.3, 5.4 — done
- Phase 6 (T1-A collection + audits + hold): 6.1, 6.2, 6.3 — done

No stale-checkbox reconciliation was needed; `sdd-apply` ownership held.

## 4. Verification summary (final rank)

- `verify-report.md` (2026-09-18, branch `measure/t1-erp-contract`,
  local-only): verdict `pass` — 18/18 tasks, 4/4 requirements and 7/7
  delta scenarios COMPLIANT by hand-check evidence (Standard mode,
  Strict TDD OFF — measurement-only, no runner; hand-check coverage is
  the verification of record); design fully coherent with no
  deviations (one honestly counted tool retry per row, index cost
  correctly charged to T1 P1/P2); additive-only with closed archives,
  schema, and canonical specs untouched; D4 hold respected with no
  publish and no push at verification time.
- Envelope audit: `test_output_hash`
  `sha256:4104f18a196b0596721063a7da14080b7c3224970baae37a62dd3cf95d97207f`
  (SHA256 of the UTF8 capture holding the concatenated stdout of the
  envelope test_command, 3993 bytes); `build_output_hash`
  `sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`
  (empty string — no build step); `evidence_revision`
  `sha256:de7c109c9351ca38676705a521eacf3c15af3b598fe24b25874a066e9ebaedfa`
  (SHA256 of `baseline-v0.2-pending.md`, re-confirmed at archive time).
- Issues: No CRITICAL. No WARNING. Three SUGGESTIONs only (design T1
  wording still says "T1 stays pending"; T2 branch pointer gone, evidence
  on commit `4190433`; P4 recount note to keep beside final table) —
  all reader-clarity-only, compliance unaffected, intentionally
  unedited for archive fidelity. The publish step (section 5) addresses
  suggestion 2/3 placement by keeping commit hashes and P4 recounts
  beside the released table. No re-verify required: no measured content
  changed after verify (publish diff is wrapper-only, section 5).
- CRITICAL gate: nothing to override; archive proceeds cleanly.

## 5. Publish baseline/v0.2 (D4 release, pre-move)

Per explicit user approval, the D4 hold is RELEASED at archive time.
New file `baseline-v0.2.md` created inside the change directory BEFORE
the archive move (so it is part of the archived audit trail):

- Mechanical creation: `cp.exe` pending → `baseline-v0.2.md`
  (CP_EXIT:0), readback `diff.exe` empty (DIFF_EXIT:0) — byte-identical
  copy before wrapper edits; no model Read/Write copy path used.
- Wrapper-only edits after copy (front-matter `v0.2-pending` → `v0.2`,
  title, guards HOLD → RELEASED, row labels `v0.2-pending` → `v0.2`,
  tag-scope note refreshed for both-rows-measured, hold-gate section →
  release record). Full pending↔published diff contains ONLY these
  wrapper lines; every P-cell counter is byte-identical.
- Content checks on `baseline-v0.2.md`: `[measured]` 13 = 6 T2 + 6 T1
  (exactly one per P1–P6 cell each) + 1 guard mention; `[narrated]` 7 =
  6 T3 + 1 guard; `total|SAP` hits only in guard/release prose, none in
  table rows; no savings claim (release record explicitly denies totals,
  SAP rows, and savings claim; `OQ-4 input` purpose phrase per the
  Both-rows-release scenario). T1 P4 184 vs 400, T2 P4 225 vs 400,
  T3 narrated intact.
- `baseline-v0.2-pending.md` kept unchanged as the pre-release audit
  trail. Published file hash
  `sha256:79965bf493351e7389ce4de497d44b81dfb3ad86109da8cd7258b1c81b7bee8f`.
- The pending file is NOT the publication; this new file is.

## 6. Specs synced (native composition, CRLF incident documented)

Single delta domain (`sync-baseline`); `foundry-init` has no delta and
was not touched. Composition ran through the native
`sdd-archive-compose` command (mandatory path — no model Read/Edit merge).
Unrelated requirements preserved byte-for-byte (diff shows pure
addition at line 88; RENAMED-before-MODIFIED ordering N/A).

Command invocation (zero exit is the only passing evidence):

```text
gentle-ai sdd-archive-compose --canonical "openspec/specs/sync-baseline/spec.md" --delta "openspec/changes/foundryh-baseline-measure/specs/sync-baseline/spec.md" --output "openspec/specs/sync-baseline/spec.md.compose-tmp"
COMPOSE_EXIT:0
```

Followed by atomic `Move-Item -Force` of the `.compose-tmp` over the
canonical (only ever replaced by a composition the command proved
complete, never by a partial write; `.compose-tmp` confirmed absent
afterwards).

| Domain | Action | Details |
|--------|--------|---------|
| sync-baseline | Updated (compose) | 4 ADDED requirements (T2 Real-Measured Row + 2 scenarios; T1 ERP-Contract Candidate-A Row + 2 scenarios; T3 Narrated-Only Control + 1 scenario; v0.2 Publication Hold + 2 scenarios). Canonical now 8 requirements / 17 scenarios. `git diff --stat`: 60 insertions, 0 deletions. |
| foundry-init | Untouched | No delta for this domain; file unmodified. |

Incident (tooling gotcha, resolved without touching composition
semantics): the first compose attempt failed with `DELTA: delta spec
declares no ADDED...` (EXIT 1). Bisected in `$TEMP` copies: the shipped
delta file used CRLF line endings while the canonical uses LF, and the
composer does not recognize `## ADDED Requirements\r`. Fix was
mechanical and byte-safe: shell-level CRLF→LF normalization of the
delta file in place, proven content-identical via
`diff.exe --strip-trailing-cr` (empty, exit 0) against a pre-normalize
backup; composition itself still ran 100% through the native command.
Requirement/scenario counts (4/7) unaffected. No manual merge was
performed. The skill's blocking rule for refused composition targets
unappliable deltas (unknown requirement, missing reason, duplicate
name, malformed rename) — this was an encoding refusal, diagnosed,
normalized, and recomposed natively.

## 7. Archive move (mechanical)

Entire change folder moved with the shell (`git mv` EXIT 0 — renames
staged as R/RM; the new untracked `baseline-v0.2.md` moved along with
the directory rename, same pattern as the prior archive), snapshotted
before the move (`cp.exe -R`, 8 files) and verified with the mandatory
`diff -r` (this archive-report is additive-only, written after the
move, excluded from the comparison).

- Source: `openspec/changes/foundryh-baseline-measure/` — gone
  (verified absent).
- Destination: `openspec/changes/archive/2026-09-18-foundryh-baseline-measure/`
  (ISO date prefix, today UTC 2026-09-18).
- Destination collision guard: destination did not exist before the move.

Verbatim `diff -r` readback (empty = passing, only evidence accepted):

```text
--- diff -r (snapshot vs destination) ---
(no output)
ARCHIVE_DIFF_EXIT:0
ARCHIVE MOVE CLEAN
```

(`diff.exe` = GNU diffutils 3.12 via Git for Windows; snapshot
`$TEMP/sdd-archive-measure/source` recursive copy of all 8 pre-move
files; zero output, exit 0.)

### Archive contents

- proposal.md ✅ (tracked, renamed via git mv)
- specs/sync-baseline/spec.md ✅ (delta, tracked, renamed via git mv)
- design.md ✅ (tracked, renamed via git mv, content unchanged by T1 unit)
- tasks.md ✅ (18/18 complete, zero unchecked)
- baseline-v0.2-pending.md ✅ (pre-release audit trail, evidence_revision
  `de7c109c…`)
- baseline-v0.2.md ✅ (D4-released publication, both rows + T3 narrated,
  hash `79965bf4…`)
- apply-progress.md ✅ (18/18 cumulative record, T2 + T1 merged)
- verify-report.md ✅ (envelope PASS, hash `1309462a…`)
- archive-report.md ✅ (this file, additive post-move)

Active changes directory no longer contains this change (only `archive/`
remains).

## 8. Source of truth updated

The following spec now reflects the new behavior:

- `openspec/specs/sync-baseline/spec.md` (8 req / 17 scen: prior v0.1
  provenance rules preserved + new T2/T1 measured-row rules, T3
  narrated-only control, and the v0.2 publication-hold rule whose
  both-rows condition is now satisfied and released by this archive)
- `openspec/specs/foundry-init/spec.md` — untouched (no delta; out of scope)

Implementation of record: `baseline-v0.2.md` (released counter table +
windows + intent ledger + pins + sources; counters-only, no token
totals, no SAP rows, no savings claim, local-only). Closed archives,
`foundry.schema.json`, and `PLANNING.md`/`INFORMACION.md` untouched
read-only, per constraints.

## 9. Traceability (files actually read)

| Artifact | Path | Notes |
|----------|------|-------|
| proposal | `.../2026-09-18-foundryh-baseline-measure/proposal.md` | T1-A candidate-A intent, 63 lines |
| spec (delta) | `.../specs/sync-baseline/spec.md` | 64 lines, 4 req / 7 scen (CRLF→LF normalized, content-identical) |
| design | `.../design.md` | 69 lines, measurement-only rationale |
| tasks | `.../tasks.md` | 62 lines, 18/18 [x] |
| implementation (pending) | `.../baseline-v0.2-pending.md` | 135 lines, evidence_revision de7c109c… |
| implementation (released) | `.../baseline-v0.2.md` | 135 lines, hash 79965bf4…, wrapper-only delta vs pending |
| apply-progress | `.../apply-progress.md` | 212 lines, T2 + T1 merged, 18/18 |
| verify-report | `.../verify-report.md` | 114 lines, envelope PASS, hash 1309462a… |
| canonical (before) | `openspec/specs/sync-baseline/spec.md` | 4 req / 10 scen pre-merge |
| canonical (after) | `openspec/specs/sync-baseline/spec.md` | 8 req / 17 scen post-merge, +60/-0 |
| canonical (untouched) | `openspec/specs/foundry-init/spec.md` | no delta, unmodified |
| archive-report | this file | `.../2026-09-18-foundryh-baseline-measure/archive-report.md` |

## 10. Constraints honored at close

Local-only (branch `measure/t1-erp-contract`, uncommitted T1 work unit
on base `4190433`, `.codegraph/` gitignored local-only, `.atl/`
untracked-only); no archive edit (closed archives read-only, verified
via empty archive/spec name-only diff at verify time); no schema edit;
no token totals; no SAP rows; no savings claim; no runner synthesis
(pack intents recorded in order, never executed); no push / no remote
mutation; no commit in this phase — commit/merge/push remain user-owned
from their own terminal, on explicit request only.

## 11. SDD cycle complete

The change has been fully planned, implemented, verified, published
(`baseline/v0.2` released), and archived. Ready for the next change.
