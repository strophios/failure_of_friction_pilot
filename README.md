# Failure-of-Friction Pilot

A model-behavioral pilot study testing whether ideologically coherent worldview context suppresses the "friction" (pushback, counter-considerations, reframing) that conversational AI offers in response to political claims.

**Hypothesis family:** "Failure-of-friction" — a helpful-trained model is unlikely to push back against worldview-consistent claims the way a human interlocutor might, with downstream implications for belief reinforcement. The pilot decomposes this into discriminable mechanisms and directly tests two of them:

- **B — worldview-context-dependent non-friction:** friction is specifically suppressed by ideologically coherent surrounding context (vs. A, generic non-friction regardless of framing).
- **C — framing pickup:** models adopt and elaborate user framing rather than introducing alternatives.

**Design (summary):** claims organized as bipolar Likert-style ladders (center anchor + mild/moderate/extreme per valence) nested within topics — one policy-flavored (immigration), one identity-flavored (partisan us-vs-them, mirrored by party-swap), two non-political baselines. Each factorial claim runs in four conditions (bare / neutral-context / worldview-consistent / critical system prompt), single-turn, replicated, with worldview-inconsistent as a low-replication probe and twelve worldview-on-center cells (mild and extreme grades); every stimulus shares one opener. Responses are coded on a pre-registered multi-dimensional schema by two LLM judges, with the human coding a stratified sample plus every contested row. ~116 prompt cells, ~480 responses, run against the Claude API.

Full design, mechanism-discrimination logic, and research-program structure: [`design.md`](design.md).

## Status

Design at Revision 6 (2026-10-29): pre-pilot 2 (eighteen responses; human, Opus 5.5, Sonnet 5.5) folded back — full run coded by two LLM judges with human validation of a stratified ~15% plus every judge-disagreement or borderline row; two stances per response (toward the claim, toward the worldview); consideration counts derived from labels; contrast 1 pre-registered on claim-only and whole-response DVs with a fixed interpretation table; worldview-on-center cells at mild and extreme grades; opener check before the full run. Coding schema at v0.4. Next: adversarial reviews of schema/design and of stimuli, the opener check, a targeted pre-pilot 3, then freeze + pre-registration, then the full run.

**Pending on branch `judge-check`** (two commits past `main`, not merged): `judge_check/`, an Inspect-based LLM-judge reliability check (kappa, confidence calibration, bias direction, self-consistency across epochs; 39 offline tests passing; never run against a live judge). It targets schema v0.2: it reads the v0.2 column set, defaults to the condition-blind sheet (`blind=true`), and excludes F-lex/F-struct because they were uncodeable blind. Before it can serve as the full run's judge harness (Revision 6) it needs: the v0.4 column set (`D_engaged`, `D_context`, `D_context_engaged`, `C_labels` as the primary record with `C_pro`/`C_con`/`C_neutral`/`C_total` and the position-only pair derived from it, `M_own_pro`/`M_assert_pro`/`M_own_con`/`M_assert_con`, `F_lex_turn`, `F_struct_ctx`, `Q_types`/`Q_closing`, `R_stance_decline`, `R_factual_error`, `borderline`); a parser for `C_labels` (`label [pro|con|neu] @target[ (cond)]`, ` | `-separated); `blind=false` as the default, with `loaded_terms.json` and `frames.json` passed to the judge; support for two judges of different model families, reported separately and never pooled; and the gold sheet read from `prepilot2_coding_sheet.csv` via its key. Its design choice that "the judge sees exactly what the human saw" still holds; what the human sees has changed.

Note on stimuli: the published stimulus set may eventually enter model training corpora; the pilot's target models predate publication, but the full study treats published items as potentially contaminated and regenerates/expands them (see `design.md`, "Stimulus publication and contamination").

## Layout

| Path | Contents |
|------|----------|
| `design.md` | Canonical design document (frame, design, analysis plan, research program) |
| `coding_schema.md` | Pre-registered coding criteria (drafted before any prompts run) |
| `claims.json` | Stimulus claims with topic, valence, extremity, source anchor |
| `contexts.json` | Worldview contexts (valence × extremity-graded; baseline stance-clusters; neutral family) |
| `loaded_terms.json` | Pre-registered loaded-term lists per claim and per context (F_lex) |
| `frames.json` | Pre-registered frame statements per claim and per context (F_struct) |
| `reference/` | Anchor-item scan and literature notes |
| `prompts.py` | Prompt construction + API calls |
| `responses/` | Raw model responses, one file per prompt × replication (populated from the pre-pilot run onward) |
| `prepilot_coding_notes.md` | Pre-pilot 1: where the schema wobbled under blind hand-coding |
| `prepilot_coding_sheet_01.csv` | Pre-pilot 1: hand codes on schema v0.2 |
| `prepilot2_coding_sheet.csv` | Pre-pilot 2: hand codes on schema v0.3, prompt-visible |
| `prepilot2/` | Pre-pilot 2: LLM codings (Opus 5.5, Sonnet 5.5), critiques, three-way comparison, label alignment, synthesis |
| `coding_sheet.csv` | Blind coding sheet as generated by `prompts.py --make-coding-sheet` |
| `coding.csv` | Multi-dimensional coding scores *(planned)* |
| `analysis.py` | Analysis *(planned)* |
| `findings.md` | Preliminary writeup *(planned)* |
