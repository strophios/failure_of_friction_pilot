# Failure-of-Friction Pilot

A model-behavioral pilot study testing whether ideologically coherent worldview context suppresses the "friction" (pushback, counter-considerations, reframing) that conversational AI offers in response to political claims.

**Hypothesis family:** "Failure-of-friction" — a helpful-trained model is unlikely to push back against worldview-consistent claims the way a human interlocutor might, with downstream implications for belief reinforcement. The pilot decomposes this into discriminable mechanisms and directly tests two of them:

- **B — worldview-context-dependent non-friction:** friction is specifically suppressed by ideologically coherent surrounding context (vs. A, generic non-friction regardless of framing).
- **C — framing pickup:** models adopt and elaborate user framing rather than introducing alternatives.

**Design (summary):** claims organized as bipolar Likert-style ladders (center anchor + mild/moderate/extreme per valence) nested within topics — one policy-flavored (immigration), one identity-flavored (partisan us-vs-them, mirrored by party-swap), two non-political baselines (remote work, social media), all four bipolar. Each of the 24 factorial claims runs in four conditions (bare / neutral-context / worldview-consistent / critical system prompt), single-turn, replicated, with worldview-inconsistent as a low-replication probe, sixteen worldview-on-center cells (mild and extreme grades), and, for the eight extreme claims, a slot-substitution arm (one context slot at a time replaced by its neutral counterpart); every stimulus shares one opener. Responses are coded on a pre-registered schema by two LLM judges working from a rules-only brief, with the human verifying matched pairs plus every contested row. 168 prompt cells, ~750 responses, run against the Claude API.

Full design, mechanism-discrimination logic, and research-program structure: [`design.md`](design.md).

## Status

Design at Revision 7 (2026-10-29): four adversarial reviews (schema/design from opposed briefs; stimuli for unintended readings and for ladder fit; `reviews/`) folded back. Confirmatory DVs are claim-relative (3-way D; a friction ratio counted by a claim-bearing sign on every labelled consideration; claim-only framing pickup), whole-response measures descriptive. Stimuli at v0.5: neutral family redrafted (it had been instructing the model), extreme contexts rewritten to pass the preemption test, baseline ladders made bipolar (24 factorial claims), party-identity ladder reordered, slot-substitution arm added. Coding schema at v0.5, split into `coding_rules.md` (the judge brief: rules only, no hypotheses) and `coding_schema.md` (rationale, calibration records, protocol, amendment log); the registered sheet is 22 columns, with everything else in `analysis_backlog.md` for post-hoc coding. Next: v0.5 stimulus audit and probe tagging, companion files, the opener check, a targeted pre-pilot 3 under the freeze thresholds, then freeze + pre-registration, then the full run.

**Pending on branch `judge-check`** (two commits past `main`, not merged): `judge_check/`, an Inspect-based LLM-judge reliability check (kappa, confidence calibration, bias direction, self-consistency across epochs; 39 offline tests passing; never run against a live judge). It targets schema v0.2: it reads the v0.2 column set, defaults to the condition-blind sheet (`blind=true`), and excludes F-lex/F-struct because they were uncodeable blind. Before it can serve as the full run's judge harness (Revision 7) it needs: the v0.5 column set (`D`, `D_engaged`, `D_context`, `D_context_engaged`, `C_labels`, `M_own_pro`/`M_assert_pro`/`M_own_con`/`M_assert_con`, `F_lex`, `F_struct_claim`/`F_struct_context`, `E_validate`, `R_refusal`, `R_stance_decline`, `S_attrib`, `borderline`), with the counts (`C_pro`/`C_con`/`C_neutral`/`C_total`, the sign-based `C_claim_pro`/`C_claim_con`, the `@position` fallback pair) derived from `C_labels` via `prompts.py`'s `parse_c_labels` (entry format `label [pro|con|neu] @target {+|-|0} (tags)`, ` | `-separated, sign required); prompting from `coding_rules.md` only (never `coding_schema.md`, which carries the hypotheses), with `loaded_terms.json` and `frames.json` passed to the judge; `blind=false` as the default; support for two judges of different model families, reported separately and never pooled, plus the context-masked D recode; the primary-DV agreement metrics on the test scales (3-way D, binary `F_struct_claim`, ratio sign) and the condition-differential bias criterion that the freeze thresholds use; and the gold sheet read from `prepilot2_coding_sheet.csv` via its key. Its design choice that "the judge sees exactly what the human saw" still holds; what the human sees has changed.

Note on stimuli: the published stimulus set may eventually enter model training corpora; the pilot's target models predate publication, but the full study treats published items as potentially contaminated and regenerates/expands them (see `design.md`, "Stimulus publication and contamination").

## Layout

| Path | Contents |
|------|----------|
| `design.md` | Canonical design document (frame, design, analysis plan, research program) |
| `coding_rules.md` | The judge brief: definitions, decision rules, anchors, worked examples — what the LLM judges and the human code from; no hypotheses |
| `coding_schema.md` | Schema rationale: measurement principle, mapping to mechanisms, calibration records (pre-pilots 1–2, label alignment), coding protocol and freeze thresholds, amendment log |
| `claims.json` | Stimulus claims with topic, valence, extremity, source anchor |
| `contexts.json` | Worldview contexts (valence × extremity-graded; baseline stance-clusters; neutral family) |
| `loaded_terms.json` | Pre-registered loaded-term lists per claim and per context (F_lex) |
| `frames.json` | Pre-registered frame statements, presuppositions, and alternative lenses per claim and per context (F_struct_claim / F_struct_context) |
| `probe_tags.json` | Inconsistent-probe pairs tagged clean-mismatch / plausibly-coherent; the gate reads the clean subset |
| `analysis_backlog.md` | Post-hoc coding, exploratory analyses, and design ideas deliberately kept out of the registered sheet |
| `reviews/` | Four adversarial reviews of Revision 6 / v0.4, their reconciliation, and the v0.5 stimulus audit |
| `reference/` | Anchor-item scan and literature notes |
| `prompts.py` | Prompt construction + API calls |
| `responses/` | Raw model responses, one file per prompt × replication (populated from the pre-pilot run onward) |
| `prepilot_coding_notes.md` | Pre-pilot 1: where the schema wobbled under blind hand-coding |
| `prepilot_coding_sheet_01.csv` | Pre-pilot 1: hand codes on schema v0.2 |
| `prepilot2_coding_sheet.csv` | Pre-pilot 2: hand codes on schema v0.3, prompt-visible |
| `prepilot2/` | Pre-pilot 2: LLM codings (Opus 5.5, Sonnet 5.5), critiques, three-way comparison, label alignment, synthesis |
| `coding_sheet.csv` | Coding sheet as generated by `prompts.py --make-coding-sheet` (prompt-visible, condition-label-hidden) |
| `coding.csv` | Multi-dimensional coding scores *(planned)* |
| `analysis.py` | Analysis *(planned)* |
| `findings.md` | Preliminary writeup *(planned)* |
