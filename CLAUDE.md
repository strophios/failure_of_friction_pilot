# Failure-of-Friction Pilot

Last verified: 2026-11-03

A pre-registered model-behavioral pilot: does ideologically coherent worldview context suppress the friction (pushback, counter-considerations, reframing) a conversational model offers to political claims? One researcher; Claude Sonnet 5.5 via the API; responses hand/LLM-coded on a frozen schema. `design.md` is canonical for the design, `coding_rules.md` for the coding rules, `coding_schema.md` for the rules' rationale and amendment log.

## State at last verification

- **Schema frozen v1.0 (2026-11-03)** = v0.6 rules, after three pre-pilots and a targeted re-check (`coding/prepilot3/synthesis.md`). Design at Revision 7 + freeze record and pre-registration summary in `design.md`.
- **Stimuli v0.5** (`stimuli/`): 28 claims (24 factorial, bipolar on all four topics; 4 center anchors), 15 contexts (4 worldview families + neutral, each with explicit slots), companion files `frames.json` (interpretive presuppositions, lenses), `loaded_terms.json`, `probe_tags.json`. Audited: all 24 consistent pairs pass the preemption test.
- **Collected**: pre-pilot 1 (10, Sonnet 5, stimuli v0.2), pre-pilot 2 (8 on Sonnet 5 + 8 on Sonnet 5.5, v0.3), pre-pilot 3 (26 on Sonnet 5.5, v0.5). **The full run has not been collected.**
- **Next, in order**: (1) full-run collection; (2) judge harness: rebase branch `judge-check` onto the reorganized layout and bring `judge_check/` to v1.0 (rules-only prompt, v0.6 columns, `prompts.parse_c_labels`, two judges reported separately), and settle the second judge — Sonnet 5.5's `F_struct_claim` was near-degenerate at the re-check, so try a non-Anthropic model (or Haiku 5.5) on the 27 rows in `coding/prepilot3/prepilot3_recheck_rows.txt`; (3) judge coding of all responses; (4) human validation sample (matched consistent/neutral pairs + every primary-DV judge disagreement or borderline flag); (5) `analysis.py` (planned), `findings.md` (planned). `analysis_backlog.md` lists post-hoc codes and exploratory analyses deliberately kept out of the registered sheet.

## Tech stack and commands

Python 3 via `uv` (`uv run ...`); `anthropic` SDK; `ruff` for lint (run `uv run ruff check prompts.py` before any commit). No test suite for `prompts.py` beyond `uv run python -m doctest prompts.py` (the `C_labels` parser). The API key is read from `FAILURE_OF_FRICTION_KEY`; the researcher runs live collections (the key in agent shells has been stale).

- `uv run python prompts.py --dry-run [--probe-inconsistent]` — assemble every cell, no API calls (144 cells / 720 responses; 168 / 744 with the probe).
- `uv run python prompts.py --probe-inconsistent` — **the full run** (resumable: existing files are skipped). Writes `responses/v0.5/claude-sonnet-5-5/`.
- `--opener-check`, `--mild-center`, `--slot-sample`, `--pre-pilot-2` — the small pre-pilot collections (already done).
- `uv run python prompts.py --make-coding-sheet --include-run v0.5/claude-sonnet-5-5 --sheet-name <dir>/<name>.csv` — prompt-visible, condition-hidden sheet + key (`<name>_key.csv`); paths are relative to `coding/`; refuses to overwrite without `--force`.
- `uv run python prompts.py --join-coding --sheet-name <dir>/<name>.csv` — joins sheet + key, derives the C counts from `C_labels`, writes `<name>_coded.csv`; prints a WARNING for every malformed label entry (never silent).

## Layout

- `design.md`, `coding_rules.md` (judge brief: rules only, no hypotheses), `coding_schema.md` (rationale, calibration records, amendment log), `analysis_backlog.md`, `README.md`.
- `stimuli/` — claims, contexts (with slots), frames, loaded terms, probe tags. All pre-registered; changing any is an amendment.
- `responses/v<stimulus>/<model>/<claim>__<condition>__rNN.json` — raw responses with prompt, usage, thinking presence, stop details. Never edited by hand; v0.2/v0.3 are calibration material only.
- `coding/prepilot{1,2,3}/` — each pre-pilot's sheet, key, human codes, LLM codes, critiques, alignment, synthesis; `coding/prepilot_coding_notes.md` spans all three.
- `reviews/` — four adversarial reviews of Revision 6 / v0.4, their reconciliation, the v0.5 stimulus audit, the reorganization proposal.
- `reference/` — ANES/GSS/Pew anchor scan.

## Conventions and invariants

- **Blinding**: a coder works from the sheet only and never opens the `_key.csv`. LLM judges receive `coding_rules.md`, `frames.json`, `loaded_terms.json`, stripped stimulus texts (ids + text, no `_meta`), and the responses — never `design.md`, the schema rationale, or any earlier codes. Judges of different model families, independent row orders, never pooled.
- **Human validation is independent first**: the human codes the primary DVs (D, D_engaged, C_labels with sign, F_struct_claim) on the validation subset before seeing judge output; everything else is verified afterwards.
- **`C_labels` format**: `label [pro|con|neu] @target {+|-|0} (tags)`, ` | `-separated; the `{sign}` (deletion test) is required; counts are derived, never typed. `prompts.parse_c_labels` is the single parser; `judge_check` must import it.
- **Primary DVs and test scales**: 3-way D; claim-relative friction ratio from the sign with the 0.4/0.6 band; binary F_struct_claim (in-frame = adopt/expand). Whole-response measures are descriptive.
- **Stimulus version bumps whenever any claim or context text changes**; responses are keyed by version and model so runs never collide.
- **Every design or schema change is logged with its rationale and the alternative rejected** (Revision History in `design.md`; Amendments in `coding_schema.md`). Post-freeze changes are amendments flagged in the writeup.
- Commit messages carry the what and the why; commits by Claude end with the attribution trailer. Keep research artifacts (codes, critiques, syntheses) in the repo, not in agent scratch space — scratch space has been lost twice.
- Markdown prose: escape literal dollar signs as `\$`.

## Gotchas

- Sonnet 5.5 thinks adaptively by default; thinking tokens count against `max_tokens` (now 8192). A refusal is data (`stop_reason`, `stop_details` recorded); never enable server-side fallbacks.
- Rows in old sheets use stimulus wordings that differ from `stimuli/` (versions 0.2/0.3); judges code them against the nearest claim and family.
- `judge_check/` exists only on branch `judge-check` (two commits past the pre-reorganization `main`); on `main` it is deleted. Rebase before touching it.
- The opener check found no opener effect on Sonnet 5.5; the pre-pilot-2 difference was a model-version effect (Sonnet 5 vs 5.5). Stance-withholding also differs by model version, so never compare across versions as if they were conditions.
