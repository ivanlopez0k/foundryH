---
schema: gentle-ai.sdd-research/v1
revision: 1
outcome: done
change: foundryh-token-research
lane: Approach 1 — ledger/counter-derived baseline (v0-compatible)
artifact_store_mode: hybrid
---

# Research — FoundryH v0 token-saving evidence (Approach 1 only)

## 1. Questions (selected lane)

- Q1: Which observable proxy counters define a v0 baseline for token saving without adding numeric token fields to the schema?
- Q2: How are the counters collected on 2–3 reference tasks (ERP exigent path vs liviano path vs no-harness run) with vs without harness?
- Q3: What evidence feeds Punto 3 (init v0 contract, no numerics)?
- Q4: What evidence feeds Punto 4 (sync + baseline table)?
- Constraints (binding): no invented numeric savings; pack verification strings are downstream intents, never workspace-local runners; no token numerics added to schema (OQ-4 parked); SAP/servicios out of v0 scope; no push or remote mutation.

## 2. Admission and observed grants

- Requested source classes (orchestrator instruction): `documentation` (internal declarations, project docs, Engram topics) + `open-web` (external supporting literature for proxy mechanisms).
- Capability declaration: no explicit `gentle-ai.sdd-research-capability/v1` token string was supplied in the launch prompt. The launch prompt explicitly orders "Collect external + internal evidence" under `mode=hybrid`, and the runtime exposed working `documentation` access (filesystem Read, Engram search/get) and working `open-web` access (websearch succeeded with live results, 2026-09-17). No denial was encountered on any requested class.
- Grants observed and exercised:
  - `documentation`: Read of foundry.json, foundry.liviano.example.json, foundry.schema.json, PLANNING.md, INFORMACION.md, openspec/config.yaml; Engram mem_search + mem_get_observation for topics #28, #25, #26, #19, #17, #24.
  - `open-web`: websearch queries returned live results (CodeCompass/CodexGraph, PR-size literature, fail-fast literature) on 2026-09-17.
- Verdict: admission treated as granted-by-instruction with zero denials; the missing explicit capability token string is recorded as a risk (see section 8), not as a denial, because every requested class succeeded with auditable sources. No claim is made beyond what the mapped sources support.

## 3. Sources

| ID | Class | Title | Publisher | URL | Accessed (UTC) | Excerpt |
|----|-------|-------|-----------|-----|----------------|---------|
| SRC-01 | documentation (internal declaration) | foundry.json — ERP exigent instance | FoundryH repo | `foundry.json` | 2026-09-17 | Pins `schema foundry/v0`, `core gentle-ai@2.7.0`, stack `erp-dotnet-angular@0.1.0`, `stackDetails.codegraph required`, verification `["dotnet test","ng test","ng lint"]` with `failFast true`, `reviewFocus ["risk","resilience"]`, `migrationCare.requireMigrationReview true`, team size 4 single-writer small-prs-to-main, `budgetDetails.tokenForecastRequired true`, init 2 versioned questions. |
| SRC-02 | documentation (internal declaration) | foundry.liviano.example.json — cheap-path counterexample | FoundryH repo | `foundry.liviano.example.json` | 2026-09-17 | Stack `lightweight-generic@0.1.0`, `codegraph optional`, verification `["npm test","npm run lint"]` with `failFast false`, `reviewFocus ["readability","reliability"]`, `tokenForecastRequired false`, same team-4 single-writer small-prs-to-main. |
| SRC-03 | documentation (internal declaration) | foundry.schema.json — v0 contract, OQ resolutions | FoundryH repo | `foundry.schema.json` | 2026-09-17 | `$comment`: OQ-1 bare commands = CI non-watch, flags parked; OQ-2 required = fail with init hint, optional = warn; OQ-3 migration notes human-only; OQ-4 token model/limits parked until baseline measured, only `tokenForecastRequired` boolean; 400-line limit intentionally NOT re-declared (immutable core); OQ-10 SAP/servicios out of scope, do not invent instances; overrides harden-only with free-text exceptionId. |
| SRC-04 | documentation (internal doc) | PLANNING.md sections 2 and 5 | FoundryH repo | `PLANNING.md` | 2026-09-17 | Section 2: immutable core = SDD cycle, atomic review transaction, single writer, authoritative dispatcher, 400-line budget, attempt + review ledgers; composable packs ERP/SAP/servicios/liviano (start with ERP exigent + liviano extremes); harden-only overrides. Section 5: token pain causes = over-reading without compression, retrying without ledger, giant PRs; mitigations = bounded read, single CodeGraph mapper, single writer, gatekeeper, attempt ledger, forecast before long work, tiered verification. Pending: measure base tokens to compare v0 vs without harness. |
| SRC-05 | documentation (internal doc) | INFORMACION.md sections 3, 5, 11, 12 | FoundryH repo | `INFORMACION.md` | 2026-09-17 | Section 3: default agent is orchestrator-only coordinator; `explore` agent is read-only, no edit, no exec. Section 5: native `sdd-attempt acquire/settle` (bounded orchestration), `sdd-verify-validate`, review `start/capture-result/inspect-candidate/status` with `--focus risk\|resilience\|readability\|reliability`; `review mode status` observed off; `review status` clean. Section 11: CodeGraph via MCP (`codegraph serve --mcp`), AGENTS.md CodeGraph-first operating guide. Section 12: Engram MCP local v1.20.0 with mandatory usage protocol; gentle-ai 2.7.0 healthy. |
| SRC-06 | documentation (internal declaration) | openspec/config.yaml — hybrid trail, strict_tdd false | FoundryH repo | `openspec/config.yaml` | 2026-09-17 | `strict_tdd: false`, zero runnable projects, no workspace test command; verification strings declared as pack INTENTS for downstream repos with explicit "Do not synthesize a combined workspace runner" rule; team-4 single-writer small-prs-to-main; 400-line RDD core limit immutable, not re-declared. |
| SRC-07 | documentation (Engram) | sdd/foundryh-token-research/explore (#28) | Engram project foundryh | topic `sdd/foundryh-token-research/explore` (#28) | 2026-09-17 | 10-mechanism saving model (single CodeGraph mapper CodeGraph-first; bounded read-only explore; single writer + authoritative dispatcher; 400-line gate; attempt + review ledgers; tiered failFast; forecast gate; ordered review lenses; pinned packs + versioned init; persistent memory + hybrid trail); Approach 1/2/3 comparison recommending Approach 1 now, Approach 2 parked (unparks OQ-4), Approach 3 opportunistic; Punto 3 must-capture list; risks (no invented numerics, no runner synthesis, SAP out, harden-only, no push). |
| SRC-08 | documentation (Engram) | sdd-init-note-sdd/foundryh (#25) | Engram project foundryh | topic `sdd-init-note-sdd/foundryh` (#25) | 2026-09-17 | Harness declaration repo, NOT runnable; core gentle-ai@2.7.0 + additive schema; hybrid persistence; strict_tdd false; master @ c166417; push auth-blocked, DO NOT push; verification strings are pack intents, never local runners. |
| SRC-09 | documentation (Engram) | sdd/foundryh/testing-capabilities (#26) | Engram project foundryh | topic `sdd/foundryh/testing-capabilities` (#26) | 2026-09-17 | strict_tdd disabled; zero runnable projects; pack intents listed per pack (ERP dotnet/ng, liviano npm) with CodeGraph/review/failFast policies; no-runner fallback. |
| SRC-10 | documentation (Engram) | Roadmap 3 puntos (#19) | Engram project foundryh | observation #19 | 2026-09-17 | Punto 2 = verification + lenses per pack (done); punto 3 = what init writes, idempotence with diff, 2 questions; punto 4 = how each member syncs the same + how to measure saving vs without harness. |
| SRC-11 | documentation (Engram) | Wrapper decision (#17) | Engram project foundryh | observation #17 | 2026-09-17 | Foundry is init wrapper (init/sync/status) over Gentle-AI, not a binary replacement; execution delegates to gentle-ai 2.7.0. |
| SRC-12 | documentation (Engram) | Session summary (#24) | Engram project foundryh | observation #24 | 2026-09-17 | erp-dotnet-angular@0.1.0 is ONE exigent reference instance, not all ERPs; 400-line limit is immutable core, not re-declared; no gh CLI/auth, Test-Json absent; punto 2 committed 26c44b1 + c166417; push pending from user terminal. |
| SRC-13 | open-web | The Navigation Paradox in Large-Context Agentic Coding (CodeCompass, Feb 2026) | Paipuru / arXiv 2602.20048 | https://arxiv.org/html/2602.20048v1 | 2026-09-17 | MCP graph navigation exposing IMPORTS/INHERITS/INSTANTIATES 1-hop neighborhoods; 258 trials across 30 tasks x 3 conditions; thesis: bigger windows shift bottleneck from retrieval capacity to navigational salience — the model fails because it never discovers the relevant file, not because it lacks budget to read it. Supports CodeGraph-first over whole-codebase ingestion. |
| SRC-14 | open-web | CodexGraph: Bridging LLMs and Code Repositories via Code Graph Databases | Liu et al. / ACL NAACL 2025 | https://aclanthology.org/2025.naacl-long.7 | 2026-09-17 | Graph-DB interface with static-analysis schema lets agents construct precise structure-aware queries for repository-level tasks; evaluated on CrossCodeEval, SWE-bench, EvoCodeBench; similarity-only retrieval has low recall on complex tasks. Supports proxy "CodeGraph-first hits vs fallback scans". Notes graph querying itself costs tokens (nuance, see contradictions). |
| SRC-15 | open-web | groundtruth — tree-sitter code knowledge graph, token-budget context packs | GitHub vinodnarayanswamy/groundtruth (MIT, early prototype) | https://github.com/vinodnarayanswamy/groundtruth | 2026-09-17 | Retrieves only target symbol + ranked dependency neighborhood packed under a token budget with graceful degradation to signatures; nodes CALLS/INHERITS/DEFINED_IN; incremental content-hash indexing. Mechanism analogue for "files read per task" and budget-packed retrieval. Prototype status limits weight (see uncertainty). |
| SRC-16 | open-web | Peer code review size guidance: fewer than 200–400 lines per review | SmartBear/Cisco study via Bitpipe PDF; reconfirmed by RockstarDeveloperUniversity 2026-05-18 summary | http://viewer.media.bitpipe.com/1253203751_753/1284482743_310/11_Best_Practices_for_Peer_Code_Review.pdf and https://rockstardeveloperuniversity.com/code-review-statistics | 2026-09-17 | Cisco study: review fewer than 200–400 LOC at a time; 60–90 min sessions yield 70–90% defect discovery; defect density drops considerably past ~300 lines, near zero after 400; 2,500 reviews / 3.2M LOC industrial dataset. External context for the 400-line gate proxy; NOT a FoundryH saving measurement. |
| SRC-17 | open-web | PR-size outcome data: small PRs merge faster, large PRs catch fewer bugs | Cubic blog 2026-02-20 (millions of PRs); Graphite review practices; BSSw "Pull Request Size Matters" | https://www.cubic.dev/blog/does-pr-size-actually-matter and https://graphite.com/blog/code-review-best-practices and https://bssw.io/items/pull-request-size-matters | 2026-09-17 | PRs under ~200 lines merge faster and more thoroughly; PRs over 400 lines catch fewer bugs (focus fatigue after ~60 min); 50-line changes ~15% less likely reverted than 250-line ones; guidance "keep PRs less than 400 lines / under 200 when possible; stack related PRs". External context for "PR size vs 400-line gate" and chained-PR forecast; NOT a FoundryH saving measurement. |
| SRC-18 | open-web | Fail-fast / fail-first CI: stop at first failure, tier cheap checks first | Software Sustainability Institute (Gibson/Lee); GitLab Fail fast testing docs; Beeming 2025-08-25 tiered .NET pipeline; Currents fail-fast guide | https://www.software.ac.uk/blog/continuous-integration-fail-fast-and-fail-first and https://scm.sra.uni-hannover.de/help/ci/testing/fail_fast_testing.md and https://gordonbeeming.com/blog/2025-08-25/fail-fast-save-big-a-smarter-ci-testing-strategy and https://github.com/currents-dev/currents-readme/blob/main/guides/ci-optimization/fail-fast-strategy.md | 2026-09-17 | Fail-fast = stop as soon as a step/spec fails (jest `--bail`, pytest `--maxfail=n`, GitHub Actions/Jenkins stop on failed step); fail-first = order cheapest/most-likely-failing checks first (smoke test); GitLab Verify/FailFast runs changed-file-relevant specs first, skips full suite on failure; Beeming case: unit-first tier gives feedback in under 3 min and skips ~15 integration tests per failed run (billed per minute). External context for "early-stopped verification (failFast)" proxy; Beeming figures are that author's pipeline, NOT FoundryH. |

## 4. Validated claims (each maps to source IDs; no FoundryH numeric savings claimed)

- C1: V0 is declaration-only with no workspace runner; verification strings are downstream pack intents and MUST NOT be executed as local commands. Sources: SRC-06, SRC-08, SRC-09, SRC-03 (OQ-1).
- C2: The v0 token model is qualitative; numeric token model and limits are explicitly parked until a baseline is measured, with only the `tokenForecastRequired` boolean present (ERP true, liviano false). Sources: SRC-03 (OQ-4), SRC-01, SRC-02, SRC-07.
- C3: Proxy P1 — CodeGraph-first hits vs fallback scans — is observable per task from the declared policy (`required` ERP fails with init hint, `optional` liviano warns) plus the operating guide order. Sources: SRC-01, SRC-02, SRC-03 (OQ-2), SRC-05 (§11 + AGENTS.md guide), SRC-07.
- C4: Graph-structured navigation is an externally supported mechanism for replacing broad retrieval loops with precise structural queries (1-hop neighborhoods, structure-aware queries, budget-packed neighborhoods). This supports P1 and "files read per task" as valid proxies; it does not quantify FoundryH savings. Sources: SRC-13, SRC-14, SRC-15.
- C5: Proxy P2 — files read per task — is observable under the bounded read-only explore agent (explore = no edit, no exec). Sources: SRC-05 (§3), SRC-04 (§5), SRC-07.
- C6: Proxy P3 — attempt counts and retries via the `sdd-attempt` ledger (acquire/settle; status/begin/finish/reset/repair diagnostics) — is observable instead of blind redo. Sources: SRC-05 (§5), SRC-04 (§2), SRC-07.
- C7: Proxy P4 — PR sizes vs the 400-line gate — is observable; the gate itself lives in immutable Gentle-AI core (RDD) and is intentionally not re-declared in the schema. External literature supports 200–400 lines as the effective-review range and documents worse outcomes for oversized reviews. Sources: SRC-03, SRC-06, SRC-12, SRC-16, SRC-17. External figures describe the industry, not FoundryH.
- C8: Proxy P5 — verification runs stopped early by failFast (ERP true, liviano false) — is observable per pack; fail-fast/fail-first (stop at first failure, cheapest checks first) is externally supported as a compute-saving mechanism. Sources: SRC-01, SRC-02, SRC-18.
- C9: Proxy P6 — forecast present/absent (ERP required, liviano skipped to avoid ceremony tax) — is observable as a gate before long work. Sources: SRC-01, SRC-02, SRC-03 (OQ-4), SRC-04 (§5), SRC-07.
- C10: Proxy P7 — review lens order (`reviewFocus[0]` maps to `review start --focus`; ERP risk/resilience-first, liviano readability/reliability-first) — is observable as one-lens-first vs N parallel full reviews. Sources: SRC-01, SRC-02, SRC-03 (OQ-5), SRC-05 (§5).
- C11: Punto 3 (init v0 contract) evidence set = exactly what foundry.json already declares (codegraph policy, verification intent list, reviewFocus order, forecast flag, team size/mode) plus versioned 2-question init; it MUST NOT add token numerics, sub-stack/role/rotating-mode questions (parked for v1), or local-runner semantics. Sources: SRC-01, SRC-03, SRC-10, SRC-07, SRC-12.
- C12: Punto 4 (sync + baseline) evidence set = pinned packs + harden-only overrides + versioned init (drift visible as versioned diff) feeding a manual versioned with-vs-without table of proxies P1–P6 on reference tasks; SAP/servicios excluded from the baseline population. Sources: SRC-03 (OQ-6, OQ-10), SRC-04 (§3), SRC-07, SRC-10, SRC-12.
- C13: No remote push or mutation is permitted in v0 evidence work; baseline table stays local until the user pushes from their terminal. Sources: SRC-08, SRC-12, SRC-07.

## 5. With-vs-without table template (manual, versioned — counters only, NO savings numerics)

> Rule: fill counters by hand per reference task. Leave `n/a` where a proxy does not apply. Never derive token totals; this table is the input that later unparks OQ-4.

| Baseline version | Task | Path | P1 CodeGraph-first hit? (yes/no + fallback scans count) | P2 Files read (count + list) | P3 Attempts / retries (sdd-attempt acquire/settle counts) | P4 PR size (added+deleted vs 400 gate; chained? Y/N) | P5 Verification (commands run; stopped early by failFast? Y/N) | P6 Forecast present? (Y/N) | Notes |
|---|---|---|---|---|---|---|---|---|---|
| `baseline/v0.1` | T1 — ERP reference change (e.g. migration + .NET + Angular touch) | ERP exigent (`foundry.json`) |  |  |  |  | `dotnet test` → `ng test` → `ng lint`, failFast true | Y (required) |  |
| `baseline/v0.1` | T2 — lightweight change (e.g. docs + small TS fix) | liviano (`foundry.liviano.example.json`) |  |  |  |  | `npm test` → `npm run lint`, failFast false | N (skipped by design) |  |
| `baseline/v0.1` | T3 — same change as T1 or T2 | no-harness (ad-hoc run) |  |  |  |  | ad-hoc commands as actually run | n/a | Control run; expect more fallback scans, more files read, unlogged retries. |

Collection protocol (v0-manual):

1. Run T1, T2, T3 once each; record counters immediately from tool history, `sdd-attempt` ledger, and PR diff stats.
2. CodeGraph-first hit = first structural question answered by `codegraph_explore` (or read-only CLI equivalent) before any broad Grep/Glob sweep; otherwise count each broad sweep as one fallback scan (C3, C4).
3. Files read = distinct files opened per task; bounded read-only explore applies to T1/T2 only (C5).
4. Attempts/retries = `acquire`/`settle` entries plus explicit redo count; no-harness T3 retries are narrated manually since no ledger exists (C6).
5. PR size = `additions + deletions` of authored text vs 400; generated goldens excluded from risk count but kept in snapshot identity per review guard; record whether chaining was needed (C7).
6. Verification = commands in declared order; record early stop position when failFast triggers (T1) vs full run (T2); never execute pack intents at the harness workspace root (C1, C8).
7. Forecast = gate artifact present (T1) or skipped (T2) with one-line reason (C9).
8. Version the filled table (`baseline/v0.1`, `v0.2`, …); keep SAP/servicios rows out (C12); keep the table local until the user pushes (C13).

## 6. Contradictions

- None among internal sources; all Engram topics, declarations, and docs agree on v0 scope, parked OQ-4, intent-not-runner rule, and SAP-out.
- Apparent tension ERP `failFast true` vs liviano `failFast false` is intentional tiering (exigent vs cheap), not a contradiction (SRC-01 vs SRC-02).
- External nuance (not a contradiction of the baseline): CodexGraph notes graph querying itself consumes tokens (SRC-14), while groundtruth/CodeCompass emphasize net context reduction (SRC-13, SRC-15). Resolution for v0: count the graph call itself inside P1/P2 rather than assuming it is free.
- External PR-size thresholds vary (under-200 ideal vs 400 hard gate). Resolution: v0 uses the immutable 400-line gate as the binary proxy boundary and records exact sizes, so future analysis can test any threshold without re-collection (SRC-16 vs SRC-17, resolved by C7 protocol step 5).

## 7. Uncertainty

- U1: Zero FoundryH counters have been measured yet; this artifact provides the template and collection protocol, not a filled baseline. No saving claim of any size is validated.
- U2: External figures (70–90% defect discovery, 15% revert delta, 3-minute feedback, ~15 skipped tests) describe other teams' pipelines and literature, cited only as mechanism plausibility for proxies P4/P5 — they MUST NOT be quoted as FoundryH results.
- U3: `groundtruth` (SRC-15) is an early single-language prototype; used as mechanism analogue only.
- U4: Anonymous/aggregate telemetry (Approach 3) granularity and privacy limits were not evaluated beyond the exploration note; it remains opportunistic context only.

## 8. Freshness

- Internal declarations and docs read 2026-09-17; Engram topics created 2026-09-16 (#17, #19, #24) and 2026-09-16/17 (#25, #26, #28) — current for v0.
- External: CodeCompass preprint Feb 2026; CodexGraph ACL 2025 (paper 2024); groundtruth repo live 2026-09-17; PR-size guidance originating from Cisco/SmartBear industrial study (2,500 reviews / 3.2M LOC), reconfirmed by 2025–2026 surveys and practitioner posts; fail-fast literature spans GitLab docs, SSI guide, and a 2025-08 practitioner case — all accessed 2026-09-17. No source is stale for mechanism support; none substitutes for a measured FoundryH baseline.

## 9. Product choices (non-authoritative; orchestrator owns discovery)

- PC1 (recommended): adopt Approach 1 for Punto 4 now — manual proxy baseline per section 5. Status: proposed by exploration (#28), selected as this research lane; orchestrator to confirm.
- PC2 (recommended): keep Approach 2 (instrumented per-phase token accounting) parked for v1; it is exactly what unparks OQ-4. Status: pending.
- PC3 (recommended): use Approach 3 (external telemetry sampling) as opportunistic context only. Status: pending.
- PC4 (recommended): Punto 3 init v0 captures exactly the SRC-01 field set (C11) with no numerics and no new questions. Status: pending orchestrator confirmation in propose.
- These choices influenced no validated claim above; claims (C1–C13) stand on sources alone.

## 10. Evidence references for handoff

- OpenSpec: `openspec/changes/foundryh-token-research/research.md` (this file, revision 1).
- Engram: topic `sdd/foundryh-token-research/research` (identical bytes, revision 1).
- Exploration input: topic `sdd/foundryh-token-research/explore` (#28).
- Pre-proposal: topic `sdd/foundryh-token-research/preproposal` + `openspec/changes/foundryh-token-research/preproposal.md` (revision 1, proposal_ready true for Approach-1 scope).
