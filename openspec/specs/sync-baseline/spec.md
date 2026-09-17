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

Baseline `baseline/v0.1` MUST record counters only for T1 (ERP reference), T2 (liviano change), T3 (no-harness control): P1 graph-first hit + fallback scans, P2 files read, P3 attempts/retries, P4 PR size vs 400 (chained Y/N), P5 early-stop, P6 forecast Y/N. It MUST NOT derive token totals; SAP/servicios rows MUST NOT appear.

#### Scenario: Harness rows collectible by hand

- GIVEN T1 and T2 runs with tool history and attempt ledger
- WHEN the collector fills the table
- THEN every P1–P6 cell holds a counter or `n/a`, never a token total

#### Scenario: Control row exposes harness gap

- GIVEN a T3 ad-hoc run of the same change
- WHEN its counters are recorded
- THEN fallback scans, files read, and unlogged retries are narrated without ledger benefit

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
