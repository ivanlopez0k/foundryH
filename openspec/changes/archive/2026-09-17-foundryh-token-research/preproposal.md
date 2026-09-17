---
schema: gentle-ai.sdd-preproposal/v1
revision: 1
change: foundryh-token-research
artifact_store_mode: hybrid
---

# Pre-proposal — foundryh-token-research (Approach 1)

## Exploration

- Outcome: ready for research lane (Approach 1 protocol feeding Punto 3 + Punto 4).
- Reference: Engram topic `sdd/foundryh-token-research/explore` (#28).

## Research request

- Lane: Approach 1 — ledger/counter-derived baseline, v0-compatible.
- Questions: Q1 proxy counters without schema numerics; Q2 collection on 2–3 reference tasks (ERP vs liviano vs no-harness); Q3 Punto 3 init v0 contract evidence; Q4 Punto 4 sync + baseline evidence.
- Requested classes: `documentation` + `open-web`.
- Constraints: no invented numeric savings; pack verification strings are intents, never local runners; no token numerics in schema (OQ-4 parked); SAP/servicios out of v0; no push / no remote mutation.

## Admission and outcome

- Admission: granted-by-instruction — launch prompt explicitly orders external + internal collection under mode=hybrid; `documentation` (Read + Engram) and `open-web` (websearch) both succeeded live on 2026-09-17 with zero denials. No explicit `gentle-ai.sdd-research-capability/v1` token string was supplied; recorded as risk in research section 2, not a denial.
- Outcome: done (revision 1). All questions supported by mapped sources SRC-01–SRC-18; claims C1–C13; contradictions, uncertainty (U1–U4), and freshness recorded; product choices kept separate (PC1–PC4).

## Evidence references

- OpenSpec: `openspec/changes/foundryh-token-research/research.md` (gentle-ai.sdd-research/v1, revision 1, outcome done).
- Engram: topic `sdd/foundryh-token-research/research` (#29; identical bytes, revision 1).
- Readback: both stores verified with equal revision (1) and identical bytes before readiness.

## Product decisions

- D1 Approach 1 for Punto 4 (manual proxy baseline, versioned table): confirmed (orchestrator-selected lane).
- D2 Punto 3 init v0 captures exactly the foundry.json field set with no numerics and no new questions: confirmed scope for propose (orchestrator finalizes wording in propose).
- D3 Approach 2 (instrumented per-phase accounting) parked for v1 (unparks OQ-4): confirmed parked.
- D4 Approach 3 (telemetry sampling) opportunistic context only: confirmed.
- D5 SAP/servicios out of v0 baseline population; no runner synthesis; no push: confirmed constraints.

## Proposal readiness

- proposal_ready: true (Approach-1 scope). Evidence valid + done, decisions confirmed, references valid, hybrid stores ready (same revision and bytes on readback).
- Handoff to sdd-propose: state revision 1, confirmed decisions D1–D5, evidence references above.
