# Delta for sync-baseline

## ADDED Requirements

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
