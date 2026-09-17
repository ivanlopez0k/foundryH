---
schema: gentle-ai.sdd-archive-report/v1
revision: 1
change: foundryh-token-research
artifact_store_mode: hybrid
archived_to: openspec/changes/archive/2026-09-17-foundryh-token-research/
date_utc: 2026-09-17
verdict_at_close: CLEAN CLOSE (verify WARNING W1 remediated post-verification)
---

# Archive Report — foundryh-token-research (init v0 + sync baseline)

## 1. Close verdict

**CLEAN CLOSE.** The change completed the full SDD cycle: explore → research →
pre-proposal → proposal → spec → design → tasks → apply (7/7) → verify
(PASS WITH WARNINGS, one minor warning) → post-verify remediation of that
warning → spec sync → archive. No CRITICAL issue ever existed; the single
WARNING (W1) was fixed after `verify-report` was persisted and before this
archive, so the state at close is clean. Per the Final-State Authority
hierarchy, this report records state AT CLOSE and cites the remediation
evidence below; it does not echo the intermediate `verify-report` snapshot's
"WARNING open" claim as a current fact.

## 2. Final-state facts (authoritative at close)

- Apply 7/7 complete + verify WARNING W1 remediated AFTER `verify-report`
  (#36) and AFTER `apply-progress` (#35 rev 1): two P4 lines in
  `baseline.md` corrected 72 (62+10) → 74 (64+10) (counter-table T2 row +
  dry-fill sources P4). `apply-progress` (#35, rev 2, merged) records the
  remediation batch success; the archived `baseline.md` lines 45 and 61–62
  now read 74 / 64+10.
- Footprint final: 74 lines vs 400 single PR (64-line `baseline.md` new +
  10 changed = 5 schema lines: 5 ins / 5 del, description-only), chained N,
  additive-only, no token numerics, no runner synthesis, no SAP, pins
  `@0.1.0` intact, ERP vs liviano parity 8/8.
- `verify-report` (#36) was PASS WITH WARNINGS solely for W1 drift; W1 is
  now fixed — this archive records a clean close, noting the W1 fix as
  post-verify remediation (see section 6).
- Push/auth: remote untouched per user constraint (no push, head still
  `c166417`). `openspec/` + `.atl/` untracked handling left to the user —
  commit only on explicit request. This archive performed zero commits and
  zero pushes.

## 3. Task Completion Gate — PASS

Persisted tasks artifact
(`openspec/changes/archive/2026-09-17-foundryh-token-research/tasks.md`,
mirroring Engram #34) shows 7/7 `[x]`, zero unchecked implementation tasks:

- 1.1 schema notes description-only — done
- 1.2 schema parses, `@0.1.0` pins, `init.versioned:true` — done
- 2.1 `baseline.md` v0.1 template + protocol, local-only — done
- 2.2 parity `foundry.json` vs liviano (read-only), 8/8 — done
- 3.1 dry-fill one row, counters-only, no token totals, no SAP row — done
- 3.2 intents in order, zero execution at root, no push — done
- 4.1 design scope guard holds — done

Post-move grep for `- [ ]` in the archived `tasks.md`: no matches. No
stale-checkbox reconciliation was needed; `sdd-apply` ownership held.

## 4. Verification summary (final rank)

- `verify-report` (#36, file + Engram, 2026-09-17): PASS WITH WARNINGS —
  7/7 tasks, 6/6 requirements, 12/12 scenarios COMPLIANT with passing
  hand-check coverage (strict_tdd false, no runner per config);
  design fully coherent; additive-only; no CRITICAL issues.
- WARNING W1 (minor count drift, non-spec-breaking): `baseline.md` T2 P4
  cell claimed 72 (62 new + 10 changed); measured footprint 74 (64-line
  file + 10 changed schema lines). Fix landed post-verification in the two
  P4 lines; `apply-progress` #35 rev 2 confirms the batch and re-confirms
  additive-only via `git diff`. No re-verify run was required: the fix
  touches only prose counter cells, not implementation, schema, or spec
  coverage (W1 was explicitly non-spec-breaking).
- SUGGESTION S1 (74 vs 80–120 forecast): calibration note only; single PR,
  chained N, Low risk all hold. S2 (untracked `openspec/` + `.atl/`):
  user-owned commit/push; this phase committed/pushed nothing.

## 5. Specs synced (Step 2, mechanical)

`openspec/specs/` was empty (no canonical specs existed), so both delta
specs were full specs copied mechanically with the shell
(cp → temp → `diff -r` → mv); model Read/Write was never used for artifact
bytes. Composition command N/A (no existing canonical to compose into).

| Domain | Action | Details |
|--------|--------|---------|
| foundry-init | Created | `openspec/specs/foundry-init/spec.md` — 3 requirements / 6 scenarios, byte-identical to delta |
| sync-baseline | Created | `openspec/specs/sync-baseline/spec.md` — 3 requirements / 6 scenarios, byte-identical to delta |

Totals: 6 requirements / 12 scenarios now canonical. Unrelated-requirement
preservation N/A (no pre-existing canonical content to preserve).

Verbatim `diff -r` readbacks (empty = passing, only evidence accepted):

```text
===== SYNC DOMAIN: foundry-init =====
--- diff -r (delta vs temp) [foundry-init] ---
--- end diff [foundry-init] status=0 ---
SYNCED: openspec/specs/foundry-init/spec.md
===== SYNC DOMAIN: sync-baseline =====
--- diff -r (delta vs temp) [sync-baseline] ---
--- end diff [sync-baseline] status=0 ---
===== ALL DOMAINS SYNCED =====
===== POST-SYNC READBACK =====
--- diff -r delta vs canonical [foundry-init] ---
--- end diff foundry-init status=0 ---
--- diff -r delta vs canonical [sync-baseline] ---
--- end diff sync-baseline status=0 ---
READBACK CLEAN: both canonical specs byte-identical to deltas
```

## 6. Archive move (Step 3, mechanical)

Entire change folder moved with the shell (`git mv` attempted → refused
because `openspec/` is untracked, "source directory is empty" in index →
verified source unchanged → plain `mv` fallback), snapshotted before the
move and verified with mandatory `diff -r` (archive-report additive-only,
written after the move, excluded).

- Source: `openspec/changes/foundryh-token-research/` — gone (verified absent).
- Destination: `openspec/changes/archive/2026-09-17-foundryh-token-research/`
  (ISO date prefix, today UTC 2026-09-17).

Verbatim `diff -r` readback (empty = passing):

```text
fatal: source directory is empty, source=openspec/changes/foundryh-token-research, destination=openspec/changes/archive/2026-09-17-foundryh-token-research
--- diff -r (snapshot vs destination) ---
--- end diff status=0 ---
ARCHIVE MOVE CLEAN
```

(The `fatal` line is `git mv`'s expected refusal on untracked source; the
script's fallback guard confirmed the source was unchanged before `mv`,
and the empty `diff -r` proves byte-identity.)

### Archive contents

- proposal.md ✅ (rev 1)
- specs/foundry-init/spec.md ✅
- specs/sync-baseline/spec.md ✅
- design.md ✅ (rev 1)
- tasks.md ✅ (7/7 complete, zero unchecked)
- baseline.md ✅ (64 lines, W1-fixed: 74 / 64+10)
- research.md ✅ (rev 1, outcome done)
- preproposal.md ✅ (rev 1, proposal_ready true)
- verify-report.md ✅ (PASS WITH WARNINGS at its time; W1 since remediated)
- archive-report.md ✅ (this file, additive post-move)

Active changes directory no longer contains this change (only `archive/`
remains). `openspec/archive` collision guard: destination did not exist
before the move.

## 7. Source of truth updated

The following specs now reflect the new behavior:

- `openspec/specs/foundry-init/spec.md` (new: init contract, 2 versioned
  questions, idempotent diff)
- `openspec/specs/sync-baseline/spec.md` (new: pinned-pack sync,
  harden-only overrides, versioned proxy baseline, local-only guard)

Implementation of record: `foundry.schema.json` (5 description-only lines,
5+/5-, no new fields) + archived `baseline.md` (T2 dry-fill, counters-only).
`foundry.json`, `foundry.liviano.example.json`, `design.md` untouched
read-only, per constraints.

## 8. Traceability (Engram observation IDs actually read)

| Artifact | Engram ID | Notes |
|----------|-----------|-------|
| explore | #28 | `sdd/foundryh-token-research/explore` |
| research | #29 | `sdd/foundryh-token-research/research`, rev 1, outcome done |
| preproposal | #30 | `sdd/foundryh-token-research/preproposal`, rev 1 |
| proposal | #31 | `sdd/foundryh-token-research/proposal`, rev 1 |
| spec | #32 | `sdd/foundryh-token-research/spec`, rev 2, 6 req / 12 scen |
| design | #33 | `sdd/foundryh-token-research/design`, rev 1 |
| tasks | #34 | `sdd/foundryh-token-research/tasks`, rev 1, 7/7 |
| apply-progress | #35 | `sdd/foundryh-token-research/apply-progress`, rev 2 incl. W1 remediation |
| verify-report | #36 | `sdd/foundryh-token-research/verify-report`, PASS WITH WARNINGS (W1 at its time) |
| archive-report | this save | `sdd/foundryh-token-research/archive-report`, rev 1 |

File trail (hybrid): this report at
`openspec/changes/archive/2026-09-17-foundryh-token-research/archive-report.md`
+ change artifacts in the same folder + canonical specs in `openspec/specs/`.

## 9. Constraints honored at close

Additive-only (schema 5+/5- description-only, zero added/removed keys);
no token numerics (OQ-4 parked, 0 numeric-token-field hits); no runner
synthesis (intents recorded, `Executed at harness root: none`);
no SAP rows; pins `@0.1.0` intact; local-only (`local_only: true`,
`Pushed: nothing`); no push / no remote mutation (head `c166417`,
`M foundry.schema.json` + `?? .atl/` + `?? openspec/` only).

## 10. SDD cycle complete

The change has been fully planned, implemented, verified, and archived.
Ready for the next change. Commit of `openspec/` + `.atl/` and any push
remain user-owned from their own terminal, on explicit request only.
