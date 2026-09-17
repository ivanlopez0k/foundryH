# foundry-init Specification

## Purpose

Defines what init v0 writes for `erp-dotnet-angular@0.1.0` and `lightweight-generic@0.1.0`. Additive-only: v0 readers MUST ignore unknown keys.

## Requirements

### Requirement: Init Contract Completeness

Init MUST write exactly the declared set: pinned `@0.1.0` packs, `stackDetails` (codegraph policy, verification order, `failFast`, `reviewFocus` order), `teamDetails` (size 4, single-writer, small-prs-to-main), `budgetDetails` (`tokenForecastRequired`), `init` answers. It MUST NOT add token numerics. The 400-line gate SHALL NOT be re-declared.

#### Scenario: ERP init writes exigent contract

- GIVEN a fresh repo targeting ERP
- WHEN init completes
- THEN contract pins `erp-dotnet-angular@0.1.0`: codegraph `required`, `dotnet test → ng test → ng lint`, failFast true, focus `risk,resilience`, forecast true

#### Scenario: Liviano init writes cheap-path contract

- GIVEN a fresh repo targeting liviano
- WHEN init completes
- THEN contract pins `lightweight-generic@0.1.0`: codegraph `optional`, `npm test → npm run lint`, failFast false, focus `readability,reliability`, forecast false

### Requirement: Exactly Two Versioned Questions

Init MUST ask exactly 2 questions (stack selection, team size) and MUST persist answers with `init.versioned: true`. It MUST NOT add sub-stack, roles, or rotating-mode questions.

#### Scenario: Two questions only

- GIVEN init prompting
- WHEN the user finishes answering
- THEN exactly 2 answers exist and no extra question was asked

#### Scenario: Answers versioned in repo

- GIVEN completed init
- WHEN the contract is inspected
- THEN `init.stackQuestion` and `init.teamSize` are fixed in the repo with `versioned: true`

### Requirement: Idempotent Init with Diff

Re-running init with unchanged answers MUST produce a byte-identical contract. With changed answers it MUST show a versioned diff before writing.

#### Scenario: Unchanged re-run is identical

- GIVEN an initialized repo with unchanged answers
- WHEN init re-runs
- THEN the contract bytes are unchanged and no diff is reported

#### Scenario: Changed answers show diff

- GIVEN an initialized repo with a changed answer
- WHEN init re-runs
- THEN a versioned diff is shown and writing requires confirmation
