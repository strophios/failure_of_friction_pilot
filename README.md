# Failure-of-Friction Pilot

A model-behavioral pilot study testing whether ideologically coherent worldview context suppresses the "friction" (pushback, counter-considerations, reframing) that conversational AI offers in response to political claims.

**Hypothesis family:** "Failure-of-friction" — a helpful-trained model is unlikely to push back against worldview-consistent claims the way a human interlocutor might, with downstream implications for belief reinforcement. The pilot decomposes this into discriminable mechanisms and directly tests two of them:

- **B — worldview-context-dependent non-friction:** friction is specifically suppressed by ideologically coherent surrounding context (vs. A, generic non-friction regardless of framing).
- **C — framing pickup:** models adopt and elaborate user framing rather than introducing alternatives.

**Design (summary):** claims organized as bipolar Likert-style ladders (center anchor + mild/moderate/extreme per valence) nested within topics — one policy-flavored (immigration), one identity-flavored (partisan us-vs-them, mirrored by party-swap), two non-political baselines. Each factorial claim runs in four conditions (bare / worldview-consistent / worldview-inconsistent / critical system prompt), single-turn, replicated. Responses are hand-coded on a pre-registered multi-dimensional schema. ~80 prompt cells, ~400 responses, run against the Claude API.

Full design, mechanism-discrimination logic, and research-program structure: [`design.md`](design.md).

## Status

Design settled (Revision 2, 2026-07-05; calibration passes folded back through Revision 4, 2026-08-03). Stimulus set and coding schema drafted and calibrated; prompt assembly and collection code written. Next: pre-pilot run (~10 responses) to validate the coding schema, then schema freeze + pre-registration, then the full run.

Note on stimuli: the published stimulus set may eventually enter model training corpora; the pilot's target models predate publication, but the full study treats published items as potentially contaminated and regenerates/expands them (see `design.md`, "Stimulus publication and contamination").

## Layout

| Path | Contents |
|------|----------|
| `design.md` | Canonical design document (frame, design, analysis plan, research program) |
| `coding_schema.md` | Pre-registered coding criteria (drafted before any prompts run) |
| `claims.json` | Stimulus claims with topic, valence, extremity, source anchor |
| `contexts.json` | Worldview contexts (valence × extremity-graded; baseline stance-clusters) |
| `reference/` | Anchor-item scan and literature notes |
| `prompts.py` | Prompt construction + API calls |
| `responses/` | Raw model responses, one file per prompt × replication (populated from the pre-pilot run onward) |
| `coding.csv` | Multi-dimensional coding scores *(planned)* |
| `analysis.py` | Analysis *(planned)* |
| `findings.md` | Preliminary writeup *(planned)* |
