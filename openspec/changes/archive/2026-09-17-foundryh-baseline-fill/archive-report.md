---
schema: gentle-ai.sdd-archive-report/v1
revision: 1
change: foundryh-baseline-fill
artifact_store_mode: openspec
archived_to: openspec/changes/archive/2026-09-17-foundryh-baseline-fill/
date_utc: 2026-09-17
verdict_at_close: CLEAN CLOSE (verify PASS, envelope remediated post-PASS, zero CRITICAL)
---

# Archive Report — foundryh-baseline-fill (baseline/v0.1 honest-counter fill)

## 1. Close verdict

**CLEAN CLOSE.** The change completed the full SDD cycle: proposal →
spec (delta) → design → tasks → apply (8/8) → verify (PASS) →
post-PASS envelope remediation → spec sync (native compose) → archive.
No CRITICAL issue ever existed; the two SUGGESTIONs in `verify-report`
are reader-confusion-only notes intentionally left as-is for archive
fidelity (per orchestrator handoff — no code changes after verify, no
new blockers). Per the Final-State Authority hierarchy, this report
records state AT CLOSE and cites the handoff facts below; it does not
echo intermediate `apply-progress` / `verify-report` snapshots as
current facts.

## 2. Final-state facts (authoritative at close, orchestrator handoff outranks snapshots)

- Verify envelope remediated AFTER first verify PASS: `verify-report.md`
  rewritten envelope-first (schema `gentle-ai.verify-result/v1`, verdict
  `pass`, requirements 2/2, scenarios 6/6, evidence_revision
  `sha256:c6111ed96335f8a8e0f92dc1f6a2b9af66459df859ba6db4eed5d6de14262dc4`,
  test_output_hash
  `sha256:c03f07b5889ffe441f2538ba613aebc1b01901f7f72fc6618855ec681c946c04`,
  build empty-hash
  `sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`).
  Validator observed: `{"valid": true, "verdict": "pass"}` EXIT 0.
  Verify-report hash now
  `sha256:fb37ae3d10b5cb44302e6c6987a7e518be39f85592ca186e133adbb4cd179abd`.
- Attempt ledger: apply passed 203/150, verify passed 280/100,
  envelope-fix passed 303/150 — each exceeded the per-attempt line budget
  (counts whole untracked change vs base) and each was cleared by explicit
  maintainer reset (`req-baseline-fill-reset-001/002/003`, actor
  maintainer). Lifetime 786 lines. `decision_required` false,
  `next_action` begin at close.
- No commits yet for this change (head still `cdb4c6e` per git log at
  archive time; change files are staged renames + untracked new, uncommitted
  by design). No push (owner user terminal only).
- No code changes after verify; no new blockers; SUGGESTIONs from verify
  (P6 80-120 vs 60-90 wording, tasks 3.2 wording) are
  reader-confusion-only, intentionally left as-is for archive fidelity.
- Skill resolution: none (no matching skill; declaration-only
  verification, no runner synthesis).

## 3. Task Completion Gate — PASS

Persisted tasks artifact
(`openspec/changes/archive/2026-09-17-foundryh-baseline-fill/tasks.md`)
shows 8/8 `[x]`, zero unchecked implementation tasks:

- 1.1 Recount T2 P4 as 74 lines (64+10), read-only — done
- 1.2 P6 forecast present, P5 zero executions — done
- 2.1 `baseline-fill.md` table, exactly one tag per P-cell — done
- 2.2 T1 same-harness ERP-lens proxy, VIOLATION + init hint — done
- 2.3 T2 verified row, P4 74 measured, warn, tag split — done
- 2.4 T3 narrated control + intent ledger + sources — done
- 3.1 One tag per cell, no token totals, no SAP rows — done
- 3.2 Local-only, archive/schema untouched, no push — done

Post-move grep for `- [ ]` in the archived `tasks.md`: no matches. No
stale-checkbox reconciliation was needed; `sdd-apply` ownership held.

## 4. Verification summary (final rank)

- `verify-report.md` (envelope-first, 2026-09-17): verdict `pass` —
  8/8 tasks, 2/2 requirements, 6/6 delta scenarios COMPLIANT by hand-check
  evidence (Standard mode, Strict TDD OFF — declaration-only fill, no
  runner; hand-check coverage is the verification of record); design fully
  coherent with no deviations; local-only with archive, schema, and
  canonical spec untouched at verification time.
- Envelope audit (post-PASS remediation, per handoff): test_output_hash is
  the SHA256 of the UTF8 capture holding the combined stdout of the
  envelope test_command; build_output_hash is the SHA256 of the empty
  string (no build step); evidence_revision is the SHA256 of
  `baseline-fill.md`. Validator: `{"valid": true, "verdict": "pass"}` EXIT 0.
- Issues: No CRITICAL. No WARNING. Two SUGGESTIONs only (P6 range text
  80-120 vs tasks.md 60-90; tasks 3.2 `only baseline-fill.md as new`
  wording) — both reader-confusion-only, compliance unaffected,
  intentionally unedited for archive fidelity. No re-verify required: no
  code changed after verify.
- CRITICAL gate: nothing to override; archive proceeds cleanly.

## 5. Specs synced (Step 2, native composition)

Single delta domain (`sync-baseline`); `foundry-init` has no delta and was
not touched. Composition ran through the native
`sdd-archive-compose` command (mandatory path — no model Read/Edit merge).
Unrelated requirements preserved byte-for-byte; RENAMED-before-MODIFIED
ordering N/A (no RENAMED sections).

Command invocation (zero exit is the only passing evidence):

```text
gentle-ai sdd-archive-compose --canonical "openspec/specs/sync-baseline/spec.md" --delta "openspec/changes/foundryh-baseline-fill/specs/sync-baseline/spec.md" --output "openspec/specs/sync-baseline/spec.md.compose-tmp"
COMPOSE_EXIT:0
```

Followed by atomic `Move-Item -Force` of the `.compose-tmp` over the
canonical (only ever replaced by a composition the command proved
complete, never by a partial write).

| Domain | Action | Details |
|--------|--------|---------|
| sync-baseline | Updated (compose) | 1 MODIFIED requirement (Versioned Proxy Baseline + provenance-tag rule, 2 scenarios updated + 1 new Untagged-cell scenario) + 1 ADDED requirement (Provenance-Tagged Baseline Fill + 3 scenarios). Canonical now 4 requirements / 10 scenarios. |
| foundry-init | Untouched | No delta for this domain; file unmodified (verified via git status: only `sync-baseline/spec.md` modified). |

Composition diff (canonical vs `.compose-tmp`, expected delta only —
unrelated `Same-Harness Sync Verification` and `Intent-Not-Runner and
Local-Only Guard` sections untouched):

```text
--- openspec/specs/sync-baseline/spec.md
+++ openspec/specs/sync-baseline/spec.md.compose-tmp
@@ Requirement: Versioned Proxy Baseline
-Baseline `baseline/v0.1` MUST record counters only for T1 (ERP reference), T2 (liviano change), T3 (no-harness control): ... It MUST NOT derive token totals; SAP/servicios rows MUST NOT appear.
+Baseline `baseline/v0.1` MUST record counters only for T1 (ERP reference proxy), T2 (liviano change), T3 (no-harness control): ... Every P1–P6 cell MUST carry exactly one provenance tag — `[measured]`, `[reconstructed from #35]`, or `[narrated]`. It MUST NOT derive token totals; SAP/servicios rows MUST NOT appear.
+(Previously: cells held a counter or n/a with no provenance tag.)
@@ Scenario: Harness rows collectible by hand
-- THEN every P1–P6 cell holds a counter or `n/a`, never a token total
+- THEN every P1–P6 cell holds a counter or `n/a` with one provenance tag
+- AND no cell holds a token total
@@ Scenario: Control row exposes harness gap
-- THEN fallback scans, files read, and unlogged retries are narrated without ledger benefit
+- THEN fallback scans, files read, and unlogged retries are tagged `[narrated]` without ledger benefit
+#### Scenario: Untagged cell rejected (new)
+### Requirement: Provenance-Tagged Baseline Fill (new, +3 scenarios: T1 proxy tagged, T2 74-line P4, T3 narrated control)
DIFF_EXIT:1 (differences = the applied delta itself; no unrelated drift)
```

Post-sync canonical requirement/scenario counts (observed via
Select-String): 4 × `### Requirement:`, 10 × `#### Scenario:`.
`git diff --stat`: `openspec/specs/sync-baseline/spec.md | 38 ++++---`
(35 insertions, 3 deletions — the delta, nothing else).

## 6. Archive move (Step 3, mechanical)

Entire change folder moved with the shell (`git mv` succeeded EXIT 0 —
two tracked files staged as renames; five untracked working files moved
along with the directory rename), snapshotted before the move and
verified with the mandatory `diff -r` (this archive-report is
additive-only, written after the move, excluded from the comparison).

- Source: `openspec/changes/foundryh-baseline-fill/` — gone (verified absent).
- Destination: `openspec/changes/archive/2026-09-17-foundryh-baseline-fill/`
  (ISO date prefix, today UTC 2026-09-17).
- Destination collision guard: destination did not exist before the move.

Verbatim `diff -r` readback (empty = passing, only evidence accepted):

```text
--- diff -r (snapshot vs destination) ---
--- end diff status=0 ---
ARCHIVE MOVE CLEAN
```

(`diff` = GNU diffutils 3.12 via Git for Windows; snapshot
`$TEMP/sdd-archive-f4da0d3566a2412a8b669770cd2d243a/source` recursive
copy of all 7 pre-move files; zero output, exit 0.)

### Archive contents

- proposal.md ✅ (tracked, renamed via git mv)
- specs/sync-baseline/spec.md ✅ (delta, tracked, renamed via git mv)
- design.md ✅ (new, moved with directory)
- tasks.md ✅ (8/8 complete, zero unchecked)
- baseline-fill.md ✅ (tagged T1/T2/T3 table, 52 lines)
- apply-progress.md ✅ (8/8 record)
- verify-report.md ✅ (envelope-first PASS, post-PASS remediated per handoff)
- archive-report.md ✅ (this file, additive post-move)

Active changes directory no longer contains this change (only `archive/`
plus no active entries remain for this change).

## 7. Source of truth updated

The following spec now reflects the new behavior:

- `openspec/specs/sync-baseline/spec.md` (Versioned Proxy Baseline now
  REQUIRES exactly-one provenance tag per P1–P6 cell + untagged-cell
  rejection; new Provenance-Tagged Baseline Fill requirement pins the
  74-line T2 P4, the T1 same-harness proxy reading, and the narrated-only
  T3 control)
- `openspec/specs/foundry-init/spec.md` — untouched (no delta; out of scope)

Implementation of record: `baseline-fill.md` (tagged counter table +
intent ledger + sources; counters-only, no token totals, no SAP rows,
local-only). Archive source `2026-09-17-foundryh-token-research/baseline.md`
and `foundry.schema.json` untouched read-only, per constraints.

## 8. Traceability (files actually read)

| Artifact | Path | Notes |
|----------|------|-------|
| proposal | `openspec/changes/archive/2026-09-17-foundryh-baseline-fill/proposal.md` | 69 lines, Approach 1 recount-in-place |
| spec (delta) | `.../specs/sync-baseline/spec.md` | 54 lines, 2 req / 6 scen |
| design | `.../design.md` | 58 lines, tag-split rationale |
| tasks | `.../tasks.md` | 40 lines, 8/8 [x] |
| implementation | `.../baseline-fill.md` | 52 lines, evidence_revision sha256:c6111e…42dc4 |
| apply-progress | `.../apply-progress.md` | 53 lines, 8/8 complete |
| verify-report | `.../verify-report.md` | 100 lines, envelope-first PASS, validator valid true |
| canonical (before) | `openspec/specs/sync-baseline/spec.md` | 3 req / 6 scen pre-merge |
| canonical (after) | `openspec/specs/sync-baseline/spec.md` | 4 req / 10 scen post-merge |
| canonical (untouched) | `openspec/specs/foundry-init/spec.md` | no delta, unmodified |
| archive-report | this file | `.../2026-09-17-foundryh-baseline-fill/archive-report.md` |

Engram sources cited by the fill (not SDD artifacts of this change):
#35/#36 provenance for P1/P2/P3 recount and P5/P6 observations.

## 9. Constraints honored at close

Local-only (`local_only: true`, `Executed at harness root: none`,
`Pushed to remote: nothing`); no archive edit (token-research archive
read-only, verified via `git diff --name-only` empty at verify time); no
schema edit; no token totals; no SAP rows; no runner synthesis (pack
intents recorded in order, never executed); no push / no remote mutation
(head `cdb4c6e`, change files staged/untracked uncommitted by design);
pre-existing untracked `.atl/` untouched and out of scope. This archive
performed zero commits and zero pushes — commit/push remain user-owned
from their own terminal, on explicit request only.

## 10. SDD cycle complete

The change has been fully planned, implemented, verified, and archived.
Ready for the next change.
