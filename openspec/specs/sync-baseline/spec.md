# sync-baseline Specification

## Purpose

Proves same-harness sync and collects a manual proxy baseline (T1/T2/T3, P1–P6) with counters only. No token totals, no runner synthesis, no SAP, no push.

## Requirements

### Requirement: Same-Harness Sync Verification

Sync MUST verify pinned packs `@0.1.0` on ERP and liviano and MUST enforce harden-only overrides: loosening a default REQUIRES `exceptionId`. Codegraph `required` MUST fail with init hint without an index; `optional` MUST warn and continue.

#### Scenario: ERP and liviano sync on pinned packs

- GIVEN ERP and liviano contracts at `@0.1.0`
- WHEN sync runs on each
- THEN both report pinned-pack match and surface any versioned drift as diff

#### Scenario: Loosening override rejected without exception

- GIVEN an override loosening a default with no `exceptionId`
- WHEN sync runs
- THEN sync fails and names the offending key

### Requirement: Versioned Proxy Baseline

Baseline `baseline/v0.1` MUST record counters only for T1 (ERP reference proxy), T2 (liviano change), T3 (no-harness control): P1 graph-first hit + fallback scans, P2 files read, P3 attempts/retries, P4 PR size vs 400 (chained Y/N), P5 early-stop, P6 forecast Y/N. Every P1–P6 cell MUST carry exactly one provenance tag — `[measured]`, `[reconstructed from #35]`, or `[narrated]`. It MUST NOT derive token totals; SAP/servicios rows MUST NOT appear.
(Previously: cells held a counter or n/a with no provenance tag.)

#### Scenario: Harness rows collectible by hand

- GIVEN T1 and T2 runs with tool history and attempt ledger
- WHEN the collector fills the table
- THEN every P1–P6 cell holds a counter or `n/a` with one provenance tag
- AND no cell holds a token total

#### Scenario: Control row exposes harness gap

- GIVEN a T3 ad-hoc run of the same change
- WHEN its counters are recorded
- THEN fallback scans, files read, and unlogged retries are tagged `[narrated]` without ledger benefit

#### Scenario: Untagged cell rejected

- GIVEN a filled table with a P1–P6 cell missing its tag
- WHEN the fill is reviewed
- THEN the fill is rejected until every cell carries exactly one tag

### Requirement: Intent-Not-Runner and Local-Only Guard

Pack verification strings MUST be treated as downstream intents and MUST NOT execute at the harness root. The baseline table MUST stay local; sync and baseline MUST NOT push or mutate remotes.

#### Scenario: Intents never execute at root

- GIVEN pack intents `dotnet test` and `npm test`
- WHEN sync or baseline runs at the harness root
- THEN no command executes and intents are only recorded in order

#### Scenario: Baseline stays local

- GIVEN a filled `baseline/v0.1` table
- WHEN the run finishes
- THEN the table is stored locally and no remote push occurs
### Requirement: Provenance-Tagged Baseline Fill

The `foundryh-baseline-fill` table MUST label T1 as same-harness proxy under the ERP lens, MUST record T2 with verified P4 `74 lines (64+10)`, and MUST narrate T3 as counterfactual without counted numbers. P4/P5/P6 cells MUST use `[measured]`, P1/P2/P3 cells MUST use `[reconstructed from #35]`, and all T3 cells MUST use `[narrated]`. The fill MUST stay local and MUST NOT edit the archive, add schema keys, or push remotes.

#### Scenario: T1 ERP-lens proxy tagged

- GIVEN the same schema-note run reinterpreted under ERP policy
- WHEN T1 P1–P6 cells are filled
- THEN P1 miss is recorded as policy VIOLATION with init hint
- AND every cell carries its provenance tag plus same-harness proxy note

#### Scenario: T2 verified fill with 74-line P4

- GIVEN git diff and Engram #35/#36 evidence
- WHEN T2 cells are verified
- THEN P4 reads `74 vs 400, chained N` tagged `[measured]`
- AND P1 miss is recorded as allowed (optional, warn)

#### Scenario: T3 narrated control never counted

- GIVEN no ledger exists for the ad-hoc run
- WHEN T3 is recorded
- THEN all cells are `[narrated]` prose with counters `n/a` or estimated
- AND no T3 value is presented as measured
### Requirement: T2 Real-Measured Row

The T2 liviano row MUST be measured from one genuine docs-clarity edit on `PLANNING.md` / `INFORMACION.md` debt under `lightweight-generic@0.1.0`. The apply-window MUST be acquire-to-settle history only. Pins MUST be `gentle-ai@2.7.0`, team-4 single-writer / single-PR / 400-gate, same P1–P6 definitions, intents in order, zero root executions. Every P1–P6 cell MUST carry exactly one tag, `[measured]` except an honest miss recorded as miss/`n/a` with reason. Counters only; no totals, no SAP rows.

#### Scenario: T2 window excludes pre-acquire reads

- GIVEN the T2 attempt ledger with acquire/settle timestamps
- WHEN the collector counts P1–P6
- THEN only tool history inside the window counts, pre-acquire reads are excluded
- AND the window is re-checkable from ledger timestamps by hand

#### Scenario: T2 tags and branch evidence audit clean

- GIVEN one T2 branch with scoped numstat excluding `.atl/`, `.codegraph/`
- WHEN a hand-check audits the row
- THEN every cell has one tag (`[measured]` or honest miss with reason)
- AND `git branch` plus numstat confirm single-row scope and clean tree

### Requirement: T1 ERP-Contract Candidate-A Row

T1 MUST be measured from one genuine ERP contract edit: remove legacy `stackDetails.notes` (`foundry.json:20`) with `migrationCare.notes` canonical intact and contract schema-valid. `.codegraph/` init with `.gitignore` decision MUST occur in-window at T1 with index cost in P1/P2 per #29-C4. Window MUST be acquire-to-settle only with pre-acquire reads excluded. Pins MUST be `gentle-ai@2.7.0` + `erp-dotnet-angular@0.1.0`, team-4 single-writer/single-PR/400-gate, ledger `dotnet test → ng test → ng lint` in order, never executed at root. Every P1–P6 cell MUST carry exactly one tag (`[measured]` or honest miss with reason); counters only, no totals, no SAP rows; D4 hold until hand-checks pass.

#### Scenario: Staged T1 fill rejected

- GIVEN no genuine ERP contract edit has landed
- WHEN a T1 fill is proposed from staged or synthetic edits
- THEN the fill is rejected and T1 stays `pending`

#### Scenario: Candidate-A edit triggers T1 collection

- GIVEN genuine removal of `foundry.json:20` on its own branch from a clean tree with `.codegraph/` init in-window
- WHEN T1 P1–P6 are collected with window, pins, and ledger discipline
- THEN P1/P2 include index cost, canonical notes stay intact and schema-valid
- AND every cell carries one tag with counters only, D4 hold respected

### Requirement: T3 Narrated-Only Control

T3 MUST remain narrated-only indefinitely. All T3 cells MUST use `[narrated]` prose with counters `n/a` or estimated. No solicited T3 run SHALL be staged, and no T3 value SHALL be presented as measured.

#### Scenario: T3 control never counted

- GIVEN no ledger exists for the ad-hoc run
- WHEN T3 is reviewed by hand
- THEN every cell shows `[narrated]` and no counter claims measurement

### Requirement: v0.2 Publication Hold

`baseline/v0.2` MUST NOT be published until both T2 and T1 rows are measured. T2 data MUST stay pending inside the change directory. Publication MUST require a passing hand-check per row: tag audit, window audit, and branch/diff evidence.

#### Scenario: Single-row v0.2 blocked

- GIVEN only the T2 row measured with T1 still `pending`
- WHEN publication of `baseline/v0.2` is attempted
- THEN publication is blocked until T1 lands

#### Scenario: Both rows release publication

- GIVEN measured T2 and T1 rows each with tag, window, and branch evidence
- WHEN the release check runs
- THEN `baseline/v0.2` is publishable as OQ-4 input with no savings claim
