# Delta for sync-baseline

## MODIFIED Requirements

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

## ADDED Requirements

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
