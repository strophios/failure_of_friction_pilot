# Repo reorganization proposal (read-only survey; nothing moved)

Surveyed 2026-10-29 on `main` (92 tracked files, clean tree). Key CSVs read for headers only.

## 1. Current tree, annotated

```
Canonical docs:   design.md  coding_rules.md  coding_schema.md  README.md
Notes/backlog:    analysis_backlog.md  reference/anchor_scan.md
Stimuli (root):   claims.json  contexts.json  frames.json  loaded_terms.json  probe_tags.json
Code/env:         prompts.py  pyproject.toml  uv.lock  .python-version  .gitignore
Data:             responses/v0.2/claude-sonnet-5  v0.3/claude-sonnet-5, claude-sonnet-5-5  v0.5/claude-sonnet-5-5
Reviews:          reviews/{reconciliation, schema_design_review_pare, ..._elaborate,
                           stimuli_audit_v05, stimuli_review_quality, stimuli_review_readings}.md
Coding, PP1:      coding_sheet.csv, coding_key.csv        (STALE-ish: generated sheet + key, old column set)
                  prepilot_coding_sheet_01.csv, prepilot_coding_notes.md
                  coding_sheet_in_process.numbers         (TRACKED despite *.numbers in .gitignore)
Coding, PP2:      prepilot2_coding_sheet.csv, prepilot2_coding_sheet_key.csv
                  prepilot2/{coder_opus55_codes.csv, coder_opus55_critique.md, coder_sonnet55_codes.csv,
                             coder_sonnet55_critique.md, label_alignment.csv, label_alignment_report.md,
                             synthesis.md, three_way_comparison.csv}
Coding, PP3:      prepilot3_coding_sheet.csv, prepilot3_coding_sheet_key.csv
Untracked/ignored on disk: prepilot2_coding_sheet.numbers, judge_check/ (only __pycache__ + tests/ dir;
                  the real package lives on branch judge-check), __pycache__/, .venv, .ruff_cache,
                  .pytest_cache, .DS_Store
```

Root has 31 tracked entries; 12 are coding records. `coding.csv`, `analysis.py`, `findings.md` are listed in README but do not exist (planned).

## 2. Proposed tree

```
README.md  design.md  coding_rules.md  coding_schema.md  analysis_backlog.md   # canonical + notes, top level
prompts.py  pyproject.toml  uv.lock  .python-version  .gitignore
stimuli/    claims.json contexts.json frames.json loaded_terms.json probe_tags.json
coding/
  prepilot1/  coding_sheet.csv coding_key.csv prepilot_coding_sheet_01.csv prepilot_coding_notes.md
              coding_sheet_in_process.numbers   (see section 5)
  prepilot2/  prepilot2_coding_sheet.csv prepilot2_coding_sheet_key.csv  + the 8 existing prepilot2/ files
  prepilot3/  prepilot3_coding_sheet.csv prepilot3_coding_sheet_key.csv
responses/    (unchanged)
reviews/      (unchanged; + this file)
reference/    (unchanged)
```

Top level: 5 docs, 4 code/env files + .gitignore, 5 dirs (`stimuli/ coding/ responses/ reviews/ reference/`).
Files keep their names (no renames), so history and prose references stay greppable.

## 3. `git mv` commands, in order

```bash
cd /Users/strophios/failure_of_friction_pilot
mkdir -p stimuli coding/prepilot1 coding/prepilot3

# stimuli (5 files)
git mv claims.json contexts.json frames.json loaded_terms.json probe_tags.json stimuli/

# pre-pilot 1 (5 files)
git mv coding_sheet.csv coding_key.csv prepilot_coding_sheet_01.csv prepilot_coding_notes.md \
       coding_sheet_in_process.numbers coding/prepilot1/

# pre-pilot 2: move the directory (8 files), then add the sheet + key (2 files)
git mv prepilot2 coding/prepilot2
git mv prepilot2_coding_sheet.csv prepilot2_coding_sheet_key.csv coding/prepilot2/
mv prepilot2_coding_sheet.numbers coding/prepilot2/        # ignored/untracked: plain mv

# pre-pilot 3 (2 files)
git mv prepilot3_coding_sheet.csv prepilot3_coding_sheet_key.csv coding/prepilot3/
```

22 tracked file moves in 6 `git mv` commands (+1 plain `mv` for the untracked `.numbers`). Verify afterwards with `git status` (all should show as renames) and `git log --follow` on one file.

## 4. Edits

### prompts.py (the only code that reads moved paths)

| Where | Old | New |
|---|---|---|
| after line 78 | (none) | add `STIMULI_ROOT = ROOT / "stimuli"` and `CODING_ROOT = ROOT / "coding"` |
| line 173 (stimulus loader) | `ROOT / "claims.json"` | `STIMULI_ROOT / "claims.json"` |
| line 179 (same loader) | `ROOT / "contexts.json"` | `STIMULI_ROOT / "contexts.json"` |
| line 481 (`make_coding_sheet`) | `ROOT / "probe_tags.json"` | `STIMULI_ROOT / "probe_tags.json"` |
| line 84 `DEFAULT_SHEET_NAME` | `"coding_sheet.csv"` | `"prepilot1/coding_sheet.csv"` |
| `sheet_paths`, line 427 | `sheet = ROOT / sheet_name` | `sheet = CODING_ROOT / sheet_name` |
| `sheet_paths`, line 429 | `return sheet, ROOT / "coding_key.csv", ROOT / "coding.csv"` | `return sheet, sheet.with_name("coding_key.csv"), sheet.with_name("coding.csv")` |

Nothing else changes: the `else` branch of `sheet_paths` already uses `sheet.with_name(...)`, so keys and `_coded.csv` follow the sheet into its directory. `RESPONSES_ROOT` and `responses_dir` are untouched. `loaded_terms.json` and `frames.json` are not read by `prompts.py` (they are for the judge harness).

Usage strings to update by hand (text only): module docstring lines 54-59 and `--sheet-name` help (~line 708). New invocations become `--sheet-name prepilot2/prepilot2_coding_sheet.csv` and `--sheet-name prepilot3/prepilot3_coding_sheet.csv` (relative to `coding/`).

Check: `uv run python prompts.py --dry-run`, then `--make-coding-sheet --sheet-name prepilot3/prepilot3_coding_sheet.csv` to a scratch name and diff, not over the real sheet.

### README.md

Replace the Layout table (lines 24-46) with:

| Path | Contents |
|---|---|
| `design.md` | Canonical design document |
| `coding_rules.md` | Judge brief: definitions, decision rules, anchors; no hypotheses |
| `coding_schema.md` | Schema rationale, calibration records, protocol, amendment log |
| `analysis_backlog.md` | Post-hoc coding, exploratory analyses, ideas kept out of the registered sheet |
| `stimuli/` | `claims.json`, `contexts.json`, `frames.json`, `loaded_terms.json`, `probe_tags.json` |
| `coding/prepilot{1,2,3}/` | Per pre-pilot: coding sheet, key, hand-code notes; PP2 also LLM codes, critiques, alignment, synthesis |
| `responses/` | Raw model responses, `v<stimulus>/<model>/` |
| `reviews/` | Adversarial reviews of Revision 6 / v0.4, reconciliation, v0.5 audit, this reorganization proposal |
| `reference/` | Anchor-item scan, literature notes |
| `prompts.py` | Prompt construction, API calls, coding-sheet build/join |
| *(planned)* | `analysis.py`, `findings.md`, `coding.csv` |

Also edit the pending-work paragraph (line 18): after `judge-check` is merged or rebased, its readers must use `stimuli/loaded_terms.json`, `stimuli/frames.json`, and `coding/prepilot2/prepilot2_coding_sheet.csv` (+ `_key.csv`). Add one clause saying so.

### design.md "File organization" (lines 316-339)

Replace the tree body with the section 2 tree (same one-line comments as the README rows). Then `grep -n "claims.json\|contexts.json\|frames.json\|loaded_terms\|probe_tags\|prepilot" design.md coding_schema.md coding_rules.md analysis_backlog.md reviews/*.md` and fix only bare path references that name a location (`prepilot2/...`, `prepilot2_coding_sheet.csv`); bare mentions of `claims.json` as a concept can stay. Do not edit the reviews' text (they are dated records); add nothing to them.

## 5. Delete / gitignore (ask first where coding work is involved)

- `coding_sheet_in_process.numbers` (tracked, 269 KB, Oct 7): ASK. It is a Numbers working copy and may hold hand codes not yet in a CSV. Proposal: keep it in `coding/prepilot1/` for now; once confirmed redundant with `prepilot_coding_sheet_01.csv`, `git rm` it. It is tracked despite the `*.numbers` ignore, so the ignore never applied.
- `prepilot2_coding_sheet.numbers` (ignored, Oct 28): ASK. Probably the editing source for `prepilot2_coding_sheet.csv`. Moved alongside, not deleted.
- `coding_sheet.csv` + `coding_key.csv` vs `prepilot_coding_sheet_01.csv`: ASK. Likely the generated PP1 sheet and its key, with the hand codes in `_01`. They are the `prompts.py` default sheet, so they are not deleted; just moved. Possible later consolidation, only after the owner confirms.
- `judge_check/` on disk (ignored: `__pycache__` + `tests/`): leftover from checking out the other branch. Safe to `rm -rf` after `ls -R judge_check` shows no non-cache files; confirm first. The real package is on branch `judge-check`.
- `__pycache__/`, `.venv/`, `.ruff_cache/`, `.pytest_cache/`, `.DS_Store`: already ignored. No action.
- Gitignore changes: none required. Optional: `.ruff_cache/` and `.pytest_cache/` explicitly, though they already show as ignored. Do not add `coding/**/*.numbers`; the existing `*.numbers` rule is fine once the tracked one is resolved.

## 6. Leave in place

- `design.md`, `coding_rules.md`, `coding_schema.md`, `README.md`: cross-referenced by name from nearly every file (20 hits in `design.md` alone), and the `prompts.py` docstring cites them.
- `analysis_backlog.md`: cited by README, design, and three reviews; one file does not justify a `notes/` directory.
- `reviews/`, `reference/`, `responses/`: already coherent; `responses/` is hard-wired in `RESPONSES_ROOT` and the sheet keys' `file` column (`v0.5/<model>/<file>`), which also means moving the stimuli and coding files does not touch any key content.
- File names: no renames (`prepilot2_coding_sheet.csv` inside `coding/prepilot2/` is redundant but renaming would force the `--sheet-name` / `_key.csv` stem logic and every doc reference to change).
- Branch `judge-check`: do not rebase as part of this; reorganize `main` first, then rebase that branch and apply the path changes in the README note above. Doing both at once is the costly move.
