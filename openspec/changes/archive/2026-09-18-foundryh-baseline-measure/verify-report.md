```yaml
schema: gentle-ai.verify-result/v1
evidence_revision: sha256:de7c109c9351ca38676705a521eacf3c15af3b598fe24b25874a066e9ebaedfa
verdict: pass
blockers: 0
critical_findings: 0
requirements: 4/4
scenarios: 7/7
test_command: 'Select-String -Path ''openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md'' -Pattern ''\[measured\]''; Select-String -Path ''openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md'' -Pattern ''\[narrated\]''; Select-String -Path ''openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md'' -Pattern ''total|SAP''; git status --short --branch; git branch; git log --oneline -3; git diff --numstat -- . ":!.atl" ":!.codegraph"; git diff --name-only -- ''openspec/changes/archive'' ''openspec/specs''; git diff -- foundry.json; git check-ignore -v .codegraph/codegraph.db'
test_exit_code: 0
test_output_hash: sha256:4104f18a196b0596721063a7da14080b7c3224970baae37a62dd3cf95d97207f
build_command: none - measurement-only change, no build step
build_exit_code: 0
build_output_hash: sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

# Verify report: foundryh-baseline-measure (T1 + T2 cumulative)

- Change: `foundryh-baseline-measure`
- Mode: Standard (Strict TDD OFF — measurement-only change, no runner; hand-check coverage is the verification of record per `openspec/config.yaml` `strict_tdd: false`)
- Date (UTC): 2026-09-18
- Branch: `measure/t1-erp-contract` (uncommitted T1 work unit on base `4190433` which already holds the T2 row); local-only, no push
- Attempt authority: orchestrator-held proceed, token `sha256:77e65b8db66329bc72ab93f0353e1cda5ce1ce62a7c320f94e61a351fca17200`, request `t1-verify-20260918-01`; this agent did not acquire or settle
- Skill resolution: none (no matching skill for declaration-only baseline measurement verification)
- Spec counted: 4 requirements (`### Requirement:`), 7 scenarios (`#### Scenario:`) in `openspec/changes/foundryh-baseline-measure/specs/sync-baseline/spec.md`
- Tasks: 18/18 checked, 0 unchecked

## Completeness (tasks)

| Task | Expected | Observed | Result |
|---|---|---|---|
| 1.1 D3 clean-tree before T2 branching | Drifts committed/stashed, clean status at branch point | Base `7c6ea39` branch point per log; T2 work committed as `4190433` | PASS |
| 1.2 Baseline-fill archive state recorded read-only | No archive edits | Scoped archive/spec diff empty; archives only read | PASS |
| 2.1 T2 branch from clean tree, single-writer single-PR | `measure/t2-docs-clarity` | Recorded in pending Notes + committed as `4190433`; current branch is the T1 successor | PASS |
| 2.2 Genuine docs-clarity micro-edit (PLANNING.md, INFORMACION.md) | Small genuine debt edit under liviano lens | Preserved in base `4190433` (T2 commit); T1 diff adds no docs edits | PASS |
| 2.3 Pending table: T2 measured, window/pins/ledger | T2 P1–P6 `[measured]`, T1 `pending`, T3 `[narrated]` at T2 time | Pending line 21 still holds the T2 measured row intact | PASS |
| 3.1 T2 tag audit, no totals, no SAP rows | Exactly one tag per claimed P-cell | T2 row 6x `[measured]`, verified in current probes | PASS |
| 3.2 T2 window audit (acquire-to-settle only) | Pre-acquire reads excluded; honest miss allowed | Freeze rule lines 31-37 intact; P1 miss + warn preserved | PASS |
| 3.3 T2 branch audit (scoped numstat, clean tree) | Single-row scope excluding `.atl/`/`.codegraph/` | T2 scope preserved via commit; current scoped numstat holds only T1 slice | PASS |
| 3.4 v0.2 hold enforced at T2 time (D4) | No `baseline/v0.2` publish with T1 pending | No publish artifact existed at T2; hold gate intact | PASS |
| 4.1 T1 trigger documented, no execution at T2 time | Next genuine ERP change + `.codegraph/` init plan | Trigger closed by the current candidate-A attempt | PASS |
| 4.2 Canonical spec unchanged by T2 | `openspec/specs/sync-baseline/spec.md` read-only | Still untouched (scoped diff empty) | PASS |
| 5.1 D3 clean-tree at 4190433 | Planning deltas are pre-acquire context, no stash needed | Status shows only T1 work-unit files modified; `.atl/` untracked-only | PASS |
| 5.2 Branch measure/t1-erp-contract from clean master | Single-writer single-PR | `git branch`: `master` + `* measure/t1-erp-contract`; merge-base equals `4190433` | PASS |
| 5.3 Genuine ERP contract edit | Remove legacy `stackDetails.notes`, canonical intact, schema-valid | Diff `foundry.json` 1+/2- removes only the legacy line; `migrationCare.notes` intact; JSON parses | PASS |
| 5.4 `.codegraph/` init in-window with gitignore | Index cost in T1 P1/P2 per #29-C4 | `.codegraph/codegraph.db` exists; `git check-ignore` confirms gitignored; cost recorded lines 73-85 | PASS |
| 6.1 T1 pending-to-measured flip | P1–P6 counters, window, pins, ledger | Pending line 22 holds the T1 measured row; T3 narrated intact | PASS |
| 6.2 Tag, window, branch audits | One tag per cell, acquire-to-settle, scoped numstat | All pass, evidence below | PASS |
| 6.3 D4 hold kept, canonical untouched | No publish, canonical read-only | No `baseline/v0.2` artifact; scoped spec diff empty | PASS |

## Focused check evidence (observed commands + results)

1. Tag probe `[measured]`: 3 matching lines — line 10 (guard prose) 1 occurrence + line 21 (T2 row) 6 occurrences + line 22 (T1 row) 6 occurrences. Occurrence audit: 13 total = 6 T2 + 6 T1 (exactly one per P1–P6 cell each) + 1 guard mention. PASS.
2. Tag probe `[narrated]`: 2 matching lines — line 10 (guard prose) 1 occurrence + line 23 (T3 row) 6 occurrences. Per-cell split of line 23: each exactly 1x `[narrated]` / 0x `[measured]`. Occurrence audit: 7 total = 6 T3 + 1 guard. PASS.
3. Banned-token probe `total|SAP`: sole hit is line-11 guard prose (`Counters only - no token totals. No SAP/servicios rows`), same guard pattern as v0.1. No totals, no SAP rows in table. PASS.
4. Savings-claim probe `sav|OQ-4`: zero hits in the pending file — no savings claim; release condition carries no claim language. PASS.
5. Pins/ledger probe: `gentle-ai@2.7.0` + `erp-dotnet-angular@0.1.0` + `lightweight-generic@0.1.0` present; team-4 single-writer / single-PR / 400-gate; ledger `dotnet test -> ng test -> ng lint` in order, never executed at root; branches `measure/t2-docs-clarity` from `7c6ea39` and `measure/t1-erp-contract` from `4190433` recorded in Notes. PASS.
6. `git status --short --branch`: `## measure/t1-erp-contract`, `M .gitignore`, `M foundry.json`, `M` pending + apply-progress + proposal + delta spec + tasks, `?? .atl/`. No staged fill, no publish artifact, `.codegraph/` correctly absent (ignored). PASS (local-only).
7. `git branch`: `master` + `* measure/t1-erp-contract`. Single T1 branch on top of the committed T2 base. PASS.
8. `git log --oneline -3`: head `4190433` (T2 commit = T1 base), then `7c6ea39`, `cdb4c6e`. No new commit by this work unit, no publish commit. PASS.
9. Scoped numstat (`git diff --numstat -- . ":!.atl" ":!.codegraph"`): `.gitignore` 3+/0, `foundry.json` 1+/2-, apply-progress 107+/2-, pending 50+/5-, proposal 23+/25-, delta spec 8+/8-, tasks 18+/2-. T1 P4 184 recount matches attempt-authored rule (tracked mods + pending + apply-progress + 7 flips x2; planning body excluded as context with full numstat shown for transparency). T2 P4 225 preserved in row. `.atl/` + `.codegraph/` excluded. PASS.
10. Archive/spec diff (`git diff --name-only -- openspec/changes/archive openspec/specs`): empty. Closed archives, schema, and canonical specs untouched. PASS.
11. Contract probe: `git diff -- foundry.json` shows only the legacy `stackDetails.notes` removal (1+/2-); `migrationCare.notes` canonical intact; `ConvertFrom-Json` and JSON parse pass; required keys intact, removal schema-valid per `foundry.schema.json:104-107` (legacy optional). PASS.
12. Ignore probe: `git check-ignore -v .codegraph/codegraph.db` returns `.gitignore:19:.codegraph/`; `git status --short --ignored` shows `!! .codegraph/` (ignored) and `?? .atl/` (pre-existing untracked local-only). PASS.
13. Publish-hold probe: no `baseline/v0.2` artifact exists; only `baseline-v0.2-pending.md` holds both rows; hold gate lines 128-135 blocks publication until both rows pass verify. No push performed. PASS.
14. Runtime harness: N/A — measurement-only change, no runner exists (`strict_tdd: false`, harness-declaration repo; pack intents recorded in order, never executed at root). No test runner synthesis required in Standard mode.

## Spec compliance matrix (delta spec, 4 REQ / 7 scenarios)

| Requirement / Scenario | Implementation evidence | Covering hand-check | Verdict |
|---|---|---|---|
| REQ T2 Real-Measured Row — genuine docs-clarity edit, acquire-to-settle window, pins, one tag per P-cell, counters only | Pending line 21 (T2 row), lines 29-58 (T2 window), lines 96-115 (ledger + pins) | Tag/window/branch audits 1, 5-10 above | COMPLIANT |
| Scenario T2 window excludes pre-acquire reads | Lines 31-37: acquire `measure-t2-pending`, settle pending, P1–P3 freeze rule, pre-acquire reads excluded | Window audit: ledger vs counted history hand-checked; P1 3 scans + miss, P2 12 files, P3 1+1 retry enumerated | COMPLIANT |
| Scenario T2 tags and branch evidence audit clean | Line 21: 6 P-cells each 1x `[measured]`; Notes carry branch `measure/t2-docs-clarity` from `7c6ea39` + window | Per-cell split 6/6 one-tag; commit `4190433` preserves single-row scope; scoped numstat clean | COMPLIANT |
| REQ T1 ERP-Contract Candidate-A Row — genuine contract edit, codegraph init in-window, window/pins/ledger discipline, one tag per cell, counters only, D4 hold | Pending line 22 (T1 row), lines 60-94 (T1 window), foundry diff, gitignore + check-ignore | Tag/window/branch audits 1, 5, 11-12; P1/P2 include index cost | COMPLIANT |
| Scenario Staged T1 fill rejected | No staged fill ever landed; T1 stayed `pending` until the genuine candidate-A edit | History check: T2 report showed bare `pending` with zero tags; current row carries genuine counters only | COMPLIANT |
| Scenario Candidate-A edit triggers T1 collection | Genuine removal of `foundry.json:20` on `measure/t1-erp-contract` from clean `4190433` with `.codegraph/` init in-window | Contract probe 11 + ignore probe 12; canonical notes intact and schema-valid; every cell one tag, counters only, D4 hold respected | COMPLIANT |
| REQ T3 Narrated-Only Control — all cells `[narrated]`, never measured, no solicited run | Pending line 23: 6 P-cells each 1x `[narrated]`, counters `n/a`, counterfactual Notes | Per-cell split 6/6 narrated, 0 measured | COMPLIANT |
| Scenario T3 control never counted | Line 23 + Notes `never counted, never measured`; no ledger exists for T3 | T3 probe: 0 `[measured]` in row; no T3 ledger section | COMPLIANT |
| REQ v0.2 Publication Hold — no publish until both T2 and T1 rows are measured with evidence each | Hold gate lines 128-135 (D4); both rows stay pending in the change dir | Publish-block check 13: no `baseline/v0.2` artifact; only the pending file | COMPLIANT |
| Scenario Single-row v0.2 blocked | Historical state (T2 measured, T1 pending) was blocked; no publish occurred | Gate-condition check: hold text present at T2 time, no publish artifact then or now | COMPLIANT |
| Scenario Both rows release publication | Both measured rows each with tag, window, and branch evidence; publishable as OQ-4 input with no savings claim | Gate-condition check: hold gate names the both-rows condition; savings probe 4 confirms no claim language | COMPLIANT |

Canonical `openspec/specs/sync-baseline/spec.md` is consistent and untouched: the pending table adds measured/narrated provenance without introducing token totals, SAP rows, runner execution, or pushes.

## Design coherence

| Design decision | Implementation | Verdict |
|---|---|---|
| Acquire-to-settle window; pre-acquire reads excluded | Freeze rules + pre-acquire exclusions + itemized in-window counts (T2 lines 31-58, T1 lines 60-94) | COHERENT |
| Honest miss as `miss`/`n/a [measured]` with reason | T2 P1 `miss + 3 fallback scans, allowed (codegraph optional, warn)`; T1 P1 `1 miss + 2 scans, init in-window`; both P5 `n/a (no commands executed)` | COHERENT |
| T1 via genuine ERP change, no staged fill (deferred at T2, landed as candidate A) | Line 22 measured row on genuine contract branch; data flow `T1 branch -> ledger + history (+ index cost) -> pending table (both rows measured)` followed | COHERENT |
| `.codegraph/` init at T1, cost in T1 P1/P2 | Init in-window with gitignore decision; cost charged per #29-C4, proven by check-ignore | COHERENT |
| D4 hold: no `baseline/v0.2` until both rows pass hand-checks | Hold gate lines 128-135; pending-only artifact; local-only no push | COHERENT |
| Row schema `\| baseline \| task \| path/harness \| P1..P6 \| Notes \|`, P-cell = counter + exactly one tag; scoped diff excludes `.atl/`/`.codegraph/` | Lines 19-23 table shape; scoped numstat command as specified | COHERENT |
| Rollback: delete change dir / checkout master / delete branch / restore contract+gitignore / drop local `.codegraph/`; archives, schema, specs untouched; local-only, no push | Git evidence 6-10, 12; no remote-tracking branch for T1 work, no push performed | COHERENT |

## Issues

No CRITICAL. No WARNING.

- SUGGESTION-1: `design.md` still phrases the T1 decision as `T1 stays pending` in the options table while `proposal.md`, the delta spec, and `tasks.md` already carry the candidate-A refinement. The data-flow section already anticipates the T1 landing, so this is stale wording, not incoherence. Refresh the options row at `baseline/v0.2` publish time so readers do not misread the design as forbidding the landed row.
- SUGGESTION-2: The live `measure/t2-docs-clarity` branch pointer is gone (current `git branch` shows only `master` + `measure/t1-erp-contract`); T2 evidence now rests on commit `4190433` plus the pending row. This is the expected branch lifecycle, but keep the T2 commit hash beside the final table at publish time so the T2 branch evidence reads without reconstructing history.
- SUGGESTION-3: P4 recounts (T2 225, T1 184) use the documented attempt-authored rule with full-branch numstat shown alongside for transparency. At v0.2 publish time, keep the single canonical recount beside the final table to avoid reader confusion (same note as the T2 verification).

## Verdict

PASS — 18/18 tasks complete; 4/4 requirements and 7/7 delta scenarios compliant by hand-check evidence; design coherent with no deviations (one honestly counted tool retry per row, index cost correctly charged to T1 P1/P2); additive-only with closed archives, schema, and canonical specs untouched; D4 hold respected with no publish and no push.

## Envelope evidence audit

- test_output_hash sha256:4104f18a196b0596721063a7da14080b7c3224970baae37a62dd3cf95d97207f is the SHA256 (Get-FileHash / python hashlib, lowercase) of the UTF8 capture at C:\Users\Usuario\AppData\Local\Temp\opencode\verify-t1-test-output.txt holding the concatenated stdout of the envelope test_command in order (exact tag probes + total/SAP probe + status/branch/log/numstat/archive-spec diff + foundry diff + check-ignore); test_exit_code 0; captured bytes 3993. Git LF advisory warnings go to stderr and are excluded from the capture.
- build_output_hash sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 is the SHA256 of the empty string (zero bytes of build output): build step is none - measurement-only change, no build step (declaration-only repo, zero runnable projects per openspec/config.yaml testing capabilities), so there is no build output to hash.
- evidence_revision sha256:de7c109c9351ca38676705a521eacf3c15af3b598fe24b25874a066e9ebaedfa is the SHA256 (lowercase) of openspec/changes/foundryh-baseline-measure/baseline-v0.2-pending.md.
