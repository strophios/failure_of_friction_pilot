# Analysis and coding backlog

Things deliberately left out of the pre-registered sheet or the pilot design, kept here so they are not lost. Everything in §1 can be coded post hoc from stored responses; §2 is analyses on data the pilot already collects; §3 is design ideas for the full version or sibling studies. Items move to the design or schema when a result calls for them, and are labeled exploratory when reported.

## 1. Post-hoc coding (from stored responses; not pre-registered)

- **Question types**: `Q_types` {basis, meaning, specifics, stakes}, anywhere in the response, multi-select; `Q_closing` (0/1). Dropped from v0.5 because every response closes with a question and no contrast reads the types. (reconciliation D3)
- **Response mode**: verdict / survey / decline / interview / decomposition ("you've put several distinct claims together"). Derivable from D_engaged, R_stance_decline, E_bothsides for the first three; decomposition and interview need a read. (reconciliation D8; pre-pilot 2 coder critiques)
- **Dropped flags**: E_bothsides, E_reflect, E_refuse, R_safety, R_boilerplate, R_factual_error (all zero or near-zero in 28 pre-pilot responses). The "seven of the last eight popular votes" error recurs across model versions.
- **Civility coaching**: counter-considerations about the user's tone or anger (`@self` entries about "done being polite"), seen only in context-heavy cells. (coder critiques, pre-pilot 2)
- **Claim as leverage against the scaffold**: the center claim used as a premise against the worldview (a070006ad2). Partly visible in D_context; the move itself has no code.
- **Evidence-citing vs assertion**: whether a consideration cites a study, statistic, or case. Only R_factual_error touched this.
- **Context-frame pickup over time**: `F_struct_context` is in the sheet as descriptive; any analysis comparing it with `F_struct_claim` is exploratory.
- **Neutral-context echo**: the model picking up the neutral affect slot ("why this one keeps you up at night") — recode after the neutral redraft to see if it persists.

## 2. Analyses on collected data (exploratory unless registered)

- Per-slot direction (values / self / outgroup / fit) from `C_labels` targets and the `{±}` sign; "context held constant" comparisons across claims within a family × grade.
- Complication share (neutral / total) by condition and extremity.
- Thinking presence and output-token share by condition (recorded per response since Revision 5).
- Sonnet 5 vs Sonnet 5.5 on the eight shared pre-pilot-2 cells (`responses/v0.3/`), including stance-withholding rates, which differed sharply (elaborate review G3).
- Judge-vs-human bias by condition (the condition-differential criterion), per judge, reported with the main results.
- Steelman-discounted and conditional-discounted friction ratios (tags `(steel)`, `(cond)`).

## 3. Design ideas (full version or sibling studies)

- **Slot factorial** beyond the single-slot substitutions the pilot runs: full 2^3 (belief, affect, identity each worldview or neutral) per family × grade; extremity mixing by slot was considered and set aside (mismatched intensities reintroduce incoherence).
- **Conjoint designs with models as respondents**: randomize prompt attributes (slot contents, claim features, opener) and estimate marginal effects on coded DVs; the slot factorial is a small version. Possible pairing with interpretability probes.
- **Bipolar baseline ladders** (in-office-better; social-media-positive) — see Revision 7 for the decision.
- Generated stimuli ("worldview translator"), real-text validation, separate real-text observational study, scripted-history multi-turn, deployment-surface localization: in design.md's research program.
