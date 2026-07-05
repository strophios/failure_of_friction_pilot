# Failure-of-Friction Pilot

A model-behavioral pilot study testing whether ideologically coherent worldview context suppresses the "friction" (pushback, counter-considerations, reframing) that conversational AI offers in response to political claims.

**Hypothesis family:** "Failure-of-friction" — a helpful-trained model is unlikely to push back against worldview-consistent claims the way a human interlocutor might, with downstream implications for belief reinforcement. The pilot decomposes this into discriminable mechanisms and directly tests two of them:

- **B — worldview-context-dependent non-friction:** friction is specifically suppressed by ideologically coherent surrounding context (vs. A, generic non-friction regardless of framing).
- **C — framing pickup:** models adopt and elaborate user framing rather than introducing alternatives.

**Design (summary):** claims organized as bipolar Likert-style ladders (center anchor + mild/moderate/extreme per valence) nested within topics — one policy-flavored (immigration), one identity-flavored (partisan us-vs-them, mirrored by party-swap), two non-political baselines. Each factorial claim runs in four conditions (bare / worldview-consistent / worldview-inconsistent / critical system prompt), single-turn, replicated. Responses are hand-coded on a pre-registered multi-dimensional schema. ~80 prompt cells, ~400 responses, run against the Claude API.

Full design, mechanism-discrimination logic, and research-program structure: [`design.md`](design.md).

## Status

Design settled (Revision 2, 2026-07-05). In progress: DV coding schema specification, stimulus construction (anchor-item scan against ANES/GSS and affective-polarization batteries), then pre-pilot run.

## Layout

| Path | Contents |
|------|----------|
| `design.md` | Canonical design document (frame, design, analysis plan, research program) |
| `coding_schema.md` | Pre-registered coding criteria (drafted before any prompts run) |
| `claims.json` | Stimulus claims with topic, valence, extremity, source anchor |
| `contexts.json` | Worldview contexts (valence × extremity-graded; baseline stance-clusters) |
| `reference/` | Anchor-item scan and literature notes |
| `prompts.py` | Prompt construction + API calls |
| `responses/` | Raw model responses (one file per prompt × replication) |
| `coding.csv` | Multi-dimensional coding scores |
| `analysis.py` | Analysis |
| `findings.md` | Preliminary writeup |
