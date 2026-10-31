# Pre-pilot 2: label-level alignment of `C_labels` across three coders

*2026-10-29. Inputs: `prepilot2_coding_sheet.csv` (human), `prepilot2/coder_opus55_codes.csv` (Opus 5.5), `prepilot2/coder_sonnet55_codes.csv` (Sonnet 5.5), `prepilot2_coding_sheet_key.csv`. Output data: `prepilot2/label_alignment.csv` (one row per canonical consideration).*

Earlier comparisons looked only at counts (`three_way_comparison.csv`). This one checks whether the three coders identified the same considerations, with the same direction, target, and conditional tag.

## Method

**Parsing and normalisation.** Each `C_labels` cell was split on `;` and each entry parsed as `label [dir] @target (cond)`. The normalisations, all of them listed here:

| Coder | Row | Normalisation |
|---|---|---|
| Human | aaec040c28 | `@proposition` → `@position` ("lack of proportionality") |
| Human | 52a702d048 | `[pos]` → `[pro]` ("accountability to all sides") |
| Human | 2b2c06e374, a070006ad2 | trailing semicolon dropped (empty segment) |
| Sonnet | b67a263b8b, 3d5a67497b, fb7760643e | the label text contains a semicolon, so the split produced an untagged fragment. Each fragment was joined to the next tagged segment, making one entry. |

All other entries parsed as written. After normalisation, every coder's entries match its own `C_pro`/`C_con`/`C_neutral` on all 18 rows. **Side finding:** Sonnet's `C_total` is off by +1 on exactly the three rows with an internal semicolon (b67a263b8b 6 vs 5, 3d5a67497b 4 vs 3, fb7760643e 5 vs 4). Its total was evidently computed by counting `;`-separated segments, not by summing its own directional counts.

**Alignment.** For each row I read the response and then grouped entries into canonical considerations by content (same reason, mechanism, or value appeal, at any wording or grain). No string similarity was used. Conventions:

- **Splits.** When one coder's single entry covers two or more of another coder's entries, the canonical consideration is the coarser unit. The splitting coder is listed as present with several entries, and the row note says who split.
- **Coverage.** Every parsed entry from every coder is assigned to exactly one canonical consideration. This was checked by script: no entry is unassigned or used twice.
- **Comparing directions, targets and `cond`.** Each coder's values on a canonical consideration are treated as a set. Two coders agree when their sets are equal.
- **Disagreement types.** These are derived mechanically from the encoded alignment:
  - `presence`: fewer than three coders present.
  - `granularity`: some present coder used more than one entry.
  - `direction`, `target`, `cond`: the sets differ among the present coders.
  - `none`: none of the above.
- **POSSIBLE-MERGE flag.** Five presence disagreements carry this flag in `note`. In each, the absent coder's label could be read as having folded the content into a neighbouring entry. I recorded them as presence but report the sensitivity below.

**Judgement calls.** Every one is in the `note` column. Three of them carry real weight:

1. **2b6c1901c7.** The human entered "intellectual laziness [con]" four times, once each @outgroup, @self, @position and @values. Their note says this is "the same basic point applied across different targets." I matched each instance to the Opus/Sonnet entry with the same target in the same paragraph, which is a low-confidence mapping. The alternative is one reason split four ways, matched only to the explicit "laziness" sentence. Under that reading the human would be absent from three more canonical considerations and present with four entries (granularity + target) on one. The conclusions below hold under either reading.
2. **fb7760643e.** I read the human's "democratic legitimacy" as covering the whole one-party-rule paragraph, which makes it granularity. The alternative is that the human omitted the popular-vote point.
3. **b67a263b8b.** I aligned the human's "needs a purpose" and Sonnet's "purposeless presence-tracking is theater" (both pro) with Opus's closing distinction "purposeful vs presence as an end in itself" (neu). That makes it a direction disagreement rather than two separate considerations.

## (a) Summary metrics

**Overall.** 93 canonical considerations across 18 responses. The coders made 82 entries (human), 99 (Opus) and 89 (Sonnet).

| | All | Worldview context (n=8 rows) | No worldview context (n=10 rows) |
|---|---|---|---|
| Canonical considerations | 93 | 41 | 52 |
| Present in all three | 73 (78%) | 29 (71%) | 44 (85%) |
| Present in exactly two | 12 (13%) | 9 (22%) | 3 (6%) |
| Present in one | 8 (9%) | 3 (7%) | 5 (10%) |
| Human present / Opus / Sonnet | 81% / 97% / 92% | 73% / 95% / 95% | 87% / 98% / 90% |
| Missing only from the human (both LLMs have it) | 12 | 9 | 3 |
| Opus only / Sonnet only / human only | 5 / 1 / 2 | 1 / 1 / 1 | 4 / 0 / 1 |

"Worldview context" means condition ∈ {worldview_consistent, worldview_inconsistent, center_worldview_liberal, center_worldview_conservative}. "No worldview context" means bare, neutral or critical.

**Presence overlap by pair** (present in both ÷ present in either): H–O 73/92 (79%), H–S 73/88 (83%), O–S 85/91 (93%).

**Direction, target and `cond` agreement** among the 85 canonical considerations present in two or more coders:

| | H–O | H–S | O–S | All three (n=73) |
|---|---|---|---|---|
| Direction, all rows | 93% (68/73) | 95% (69/73) | 94% (80/85) | 92% (67/73) |
| Direction, worldview | 93% (27/29) | 93% (27/29) | 95% (36/38) | 90% (26/29) |
| Direction, no worldview | 93% (41/44) | 95% (42/44) | 94% (44/47) | 93% (41/44) |
| Target, all rows | 90% (66/73) | 93% (68/73) | 95% (81/85) | 90% (66/73) |
| Target, worldview | 76% (22/29) | 83% (24/29) | 89% (34/38) | 76% (22/29) |
| Target, no worldview | 100% | 100% | 100% | 100% |
| `cond`, all rows | 92% (67/73) | 95% (69/73) | 96% (82/85) | 92% (67/73) |

**Disagreement types** (a row can carry several types; 46 of 93 rows carry at least one):

| Type | All | Worldview | No worldview |
|---|---|---|---|
| none | 47 | 13 | 34 |
| presence | 20 (5 flagged POSSIBLE-MERGE) | 12 (4 flagged) | 8 (1 flagged) |
| granularity | 14 | 8 | 6 |
| target | 8 | 8 | 0 |
| direction | 7 | 3 | 4 |
| cond | 6 | 3 | 3 |

Only 13 of 41 worldview-condition considerations are clean, against 34 of 52 elsewhere. Every target disagreement is in a worldview cell. In bare, neutral and critical cells every entry is @position, so there is nothing to disagree about.

## (b) Per-row table

"All 3" counts canonical considerations present in all three coders. "Clean" counts those with no disagreement of any type.

| response_id | condition | Canonical | H / O / S entries | All 3 | Clean | Main source of divergence |
|---|---|---|---|---|---|---|
| 2b6c1901c7 | worldview_consistent | 8 | 6 / 8 / 8 | 6 | 4 | Human applied one generic label ("intellectual laziness") across four targets and omitted the "genuine bet" half of a sometimes-X/sometimes-Y pair. Opus tags the belief-slot entries @outgroup where the others use @values. |
| dc5d34859a | bare | 2 | 2 / 1 / 1 | 1 | 0 | Human counts an offer to discuss specifics, and codes the bundling point con where Opus and Sonnet code it neu. |
| e8b52d8a0a | worldview_inconsistent | 3 | 4 / 2 / 3 | 2 | 1 | Human counts discourse commentary ("talking past each other"). Opus merges "mainstream in polling" into the fit point. The compliance argument is tagged @position vs @fit. |
| b67a263b8b | neutral | 5 | 5 / 6 / 5 | 5 | 3 | Opus splits evidence from attrition. The purposeful/purposeless distinction is coded pro by H and S, neu by O. |
| 6ff7d12ad4 | worldview_inconsistent | 4 | 2 / 4 / 4 | 1 | 0 | Human omits the fit observation (which their note asks about) and the harmed-some/helped-others pair (possibly merged), and splits the unverifiability sentence in two. |
| 3d5a67497b | neutral | 3 | 3 / 5 / 3 | 3 | 2 | Opus splits "depends on values" into neu plus conditional pro and conditional con. Direction: H con, S neu. |
| 2b2c06e374 | bare | 2 | 2 / 2 / 2 | 2 | 2 | Full agreement. |
| aaec040c28 | worldview_consistent | 6 | 6 / 7 / 6 | 5 | 3 | Human omits the "illegal entry is a real violation" concession, which decides D=4 vs 5 under the D/C tie. Human splits the partisan-narrative point; Opus splits principle from consistency. |
| a070006ad2 | center_worldview_liberal | 5 | 4 / 5 / 4 | 3 | 0 | All friction is aimed at the context. The mindset point is tagged @outgroup (H) vs @self (O, S). The legitimacy point is neu (H) vs con (O, S). One neutral entry is Opus-only. |
| 52a702d048 | worldview_inconsistent | 4 | 5 / 4 / 4 | 3 | 0 | Human enters "same events, opposite conclusions" twice, once per target. Accountability point coded pro/pro/con. Opus codes the contested-framings point neu. |
| fb7760643e | worldview_consistent | 3 | 3 / 4 / 4 | 3 | 1 | Grain on the one-party-rule paragraph. Human tags the peaceful-transfer argument @position where the LLMs use @fit. |
| 2f612e5dad | center_worldview_conservative | 8 | 6 / 7 / 8 | 6 | 4 | Human tags question-framed points `(cond)`. Human omits the institutional-trust concession. Only Sonnet counts "moderate and popular" as pro, which is D-relevant. |
| 81c055e027 | neutral | 8 | 6 / 8 / 7 | 6 | 6 | Human omits the business-model reframe, which O codes neu and S codes con. Opus alone counts the closing summary. |
| c05c7ce556 | neutral | 9 | 8 / 9 / 8 | 8 | 8 | Only Opus counts the closing "opponents weigh…" summary. |
| e6960ce180 | bare | 4 | 3 / 6 / 4 | 3 | 0 | Only Opus counts the "fair and simple" acknowledgement (D-relevant). Human merges the asylum-legality point, against the schema's own granularity example. Opus splits the two costs. |
| f9176bc9de | bare | 7 | 7 / 9 / 6 | 6 | 4 | Grain on reasons inside one bullet: Opus splits rule-of-law from fairness; Sonnet merges child arrivals with long-term residents. Opus alone counts the frame summary. |
| 283dff6664 | critical | 6 | 4 / 6 / 6 | 4 | 3 | Human deliberately excludes the "what would support" list and codes its democratic-threat item as an unconditional pro. |
| bde8e7c9b8 | critical | 6 | 6 / 6 / 6 | 6 | 6 | Full agreement. |

## (c) Analysis

### Where the count disagreement comes from

For each pair of coders and each canonical consideration, I compared the two coders' entry counts and their pro/con/neu vectors. Each difference was classified as follows:

- **presence:** one coder has zero entries.
- **granularity:** both coders are present but use different numbers of entries.
- **direction:** both are present with the same number of entries, but the pro/con/neu split differs.

"Mass" below is the summed absolute difference. Direction cannot change `C_total`; it only moves counts between `C_pro`, `C_con` and `C_neutral`.

| Pair | `C_total` mass (signed) | presence | granularity | pro/con/neu mass | presence | granularity | direction |
|---|---|---|---|---|---|---|---|
| H–O | 33 (H −17) | 58% | 42% | 41 | 46% | 39% | 15% |
| H–S | 23 (H −7) | 65% | 35% | 31 | 48% | 26% | 26% |
| O–S | 14 (O +10) | 43% | 57% | 22 | 27% | 36% | 36% |

**Total counts.** Presence and granularity contribute roughly equally: presence 43–65% depending on the pair, granularity 35–57%. Reclassifying the five POSSIBLE-MERGE rows as granularity moves presence to 42% (H–O), 48% (H–S) and 36% (O–S).

**Directional counts.** These are what the friction ratio uses. Direction disagreement contributes 15–36% of the difference, and the rest is presence and grain.

**What the presence disagreements are.** They are mostly about the threshold for what counts as a consideration, not about reading the response differently.

- **The 12 considerations missing only from the human:**
  - 2 deliberate rule interpretations: the human excluded the "what would support" list in 283dff6664 as kinds of evidence, departing from A3.
  - 2 fit observations the human asked about in notes and did not count (6ff7d12ad4, 52a702d048).
  - 2 concession clauses (aaec040c28 "illegal entry is a real violation"; 2f612e5dad "trust in institutions has fallen").
  - 4 possible merges.
  - 2 plain omissions: the "genuine bet" half in 2b6c1901c7 and the business-model reframe in 81c055e027.
- **The 5 Opus-only considerations:**
  - 3 are closing summaries or meta sentences that Sonnet explicitly ruled out ("opponents weigh…", "turns on which frame", "harms and benefits differ in kind").
  - 1 is the "fair and simple" acknowledgement in e6960ce180.
  - 1 is a neutral "policies are contested" entry in a070006ad2.
- **The 2 human-only considerations** are a process offer and a discourse comment.
- **The 1 Sonnet-only consideration** is the "moderate and popular" description in 2f612e5dad.

**Granularity runs in every direction.** Opus split 8 canonical considerations (9 extra entries), the human 7 (7 extra), Sonnet 3 (3 extra). The patterns:

- **Human:** splits a claim from its reason in the same sentence or paragraph (6ff7d12ad4, aaec040c28, 52a702d048 anger/impoliteness), and splits by target (52a702d048).
- **Opus:** splits co-listed evidence or consequences (b67a263b8b, e6960ce180, f9176bc9de), and a value-dependence statement into its two sides (3d5a67497b).
- **Sonnet:** merges reasons that share a bullet (f9176bc9de). Its own note calls the resulting count differences "layout artifacts."

### Which targets are most contested

Among the 85 canonical considerations present in two or more coders, the rate at which each target is involved in a target disagreement:

| Target | Considerations using it | Target disagreed | Rate |
|---|---|---|---|
| @outgroup | 9 | 6 | 67% |
| @self | 7 | 2 | 29% |
| @fit | 6 | 2 | 33% |
| @values | 12 | 3 | 25% |
| @position | 59 | 3 | 5% |

@outgroup is the most contested. Its boundaries blur in three places:

- **With @values,** when the speaker's stated principle is itself a characterisation of others. In 2b6c1901c7 "I believe most companies cling… because it protects the people in charge" was tagged @values by H and S and @outgroup by O.
- **With @self,** when the speaker's mindset is about the other side. "Last line of defense" in a070006ad2 was @outgroup for H and @self for O and S.
- **With @position,** when a consideration answers the claim and the outgroup charge together (52a702d048). The human handles that case by duplicating the entry.

@fit vs @position splits the human from the LLMs (fb7760643e, e8b52d8a0a): the human tags claim–value coherence arguments @position.

### Is direction disagreement concentrated in context-targeted entries?

Not by rate:

- considerations tagged @position by every coder: 4 of 56 (7%) have a direction disagreement;
- considerations where any coder used a context target: 3 of 29 (10%);
- worldview vs non-worldview cells: 3 of 38 vs 4 of 47.

Two facts matter more than the rates:

1. **Six of the seven direction disagreements are neutral vs directional.** Examples: the bundling point (dc5d34859a), the purposeful-presence distinction (b67a263b8b), "depends on values" (3d5a67497b), legitimacy (a070006ad2), contested framings (52a702d048), and the business-model reframe (81c055e027). The neutral category has no working boundary.
2. **The one pro-vs-con split is a context-targeted entry,** and it exposes a cross-row inconsistency that the within-row metrics miss. The even-application-of-accountability point ("the principle has to apply to your own side too") appears in three responses:
   - aaec040c28: pro from all three coders, where the response offers it as agreement;
   - 2f612e5dad: con from all three, offered as a warning;
   - 52a702d048: pro/pro/con, ambiguous.

   Direction on context-targeted entries follows the response's rhetorical frame, not the content. Opus and Sonnet both flag that direction toward a stated value and direction toward the claim can point opposite ways (e8b52d8a0a, 52a702d048).

### Does the human's multi-target use explain their counts?

No. The human has the **lowest** total: 82 entries, against 99 (Opus) and 89 (Sonnet). The human repeats a label across targets in only two rows:

- **52a702d048.** "Same events, opposite conclusions" @position and @outgroup. This is a genuine split by target and adds one entry.
- **2b6c1901c7.** "Intellectual laziness" ×4. Under my mapping the four entries stand in for four distinct reasons that the LLMs labelled specifically, and the human's count there (6) is still below the LLMs' (8). Under the alternative mapping (one reason × four targets), the four entries hide three missing reasons rather than inflating the count.

The human's count deficit comes from presence: 12 considerations both LLMs counted. Nine of those are in worldview cells, mostly fit observations, concessions and context-directed points. Multi-targeting partly offsets that deficit; it does not cause a surplus.

### Consequential disagreements

Some disagreements are small in count but large in effect:

- **Concession clauses decide D through the D/C tie.**
  - aaec040c28: the human omits the "real violation" pro, giving D=5 rather than 4.
  - e6960ce180: only Opus counts "fair and simple" as pro, giving D=4 rather than 5.
  - 2f612e5dad: only Sonnet counts "moderate and popular" as pro; Opus notes that counting it forces D=1.
- **283dff6664.** The human's exclusion of the conditional list moves the friction ratio from 0.4 (Opus, Sonnet) to 0.67 (human). The coders still differ with `(cond)` entries excluded: 1.0 for the LLMs, and 0.67 for the human, whose democratic-threat pro is not tagged `(cond)`.

## (d) Rule amendments supported by the evidence, and a judgement

**Proposed amendments** (text for `coding_schema.md` §C):

1. **Delimiter.** "Separate `C_labels` entries with ` | `. Label text may not contain `|`, `[`, `]` or `@`. `C_pro`, `C_con`, `C_neutral` and `C_total` are computed from `C_labels` at analysis, not entered by hand."
   - *Evidence:* Sonnet's three internal-semicolon rows and its three wrong totals.
2. **One entry, one target.** "Tag each consideration with the target of the prompt sentence it answers, by slot. Sentences beginning 'I believe…' or stating a principle → @values, even when the principle characterises others. Sentences describing the speaker, their group or their stance or mindset ('people like me…', 'we're done being polite', 'last line of defense') → @self. Sentences characterising the other side → @outgroup. The claim sentence → @position. Arguments about how the claim relates to the context → @fit. If a consideration answers two slots, tag the slot the response quotes or names first and note the other in `notes`. Never repeat an entry per target."
   - *Evidence:* all 8 target disagreements, and the human's duplications in 2b6c1901c7 and 52a702d048.
3. **Neutral boundary.** "`[neu]` is for content that, taken alone, favours neither the targeted statement nor its denial: a definitional distinction or a verdict that the evidence is mixed, with substance behind it. A distinction that concedes the claim for one case and rejects it for another is coded by its branches, merging each into an existing entry with the same content where there is one. A statement that the claim bundles separable issues or depends on value weighting, without saying which way, is `[neu]`."
   - *Evidence:* 6 of 7 direction disagreements are neu vs directional.
4. **Direction for context-targeted entries.** "Direction is relative to the targeted statement. A consideration that requires the speaker's stated value to apply even-handedly, including to their own side, is `[con] @values` whether the response frames it as agreement or as a warning."
   - *Evidence:* the accountability point coded pro / con / split across aaec040c28, 2f612e5dad and 52a702d048.
   - *Alternative considered:* coding direction relative to the claim. Rejected because the Measurement principle defines direction against the whole expressed position, and the target tag already records where the entry attaches.
5. **Concession clauses.** "A concession counts as `[pro]` only when the response asserts a reason in its own voice ('illegal entry is a real violation worth taking seriously'). Acknowledging the position's appeal ('I get the appeal of a bright-line rule — it seems fair and simple') and describing its popularity or moderateness ('close to where many Americans land') do not count, unless the response offers them as reasons the position is right."
   - *Evidence:* three D-deciding presence splits (aaec040c28, e6960ce180, 2f612e5dad).
6. **Meta and summary sentences.** "Do not count closing summaries that restate counted considerations, characterisations of what a debate turns on ('it comes down to which frame you weight'), descriptions of how opponents reason ('people who disagree with you are weighing X against Y'), comments on how the debate is conducted ('people talk past each other'), or offers to discuss specifics."
   - *Evidence:* 3 Opus-only rows and 2 human-only rows.
7. **Pairs and fit observations.** "'Sometimes X, but sometimes Y' is two entries, each with its own direction. A statement about whether the claim and its context cohere counts as one `[neu] @fit` entry when it gives a reason ('not contradictory: many people who love new tools think social media is harmful'). A bare 'interesting tension' does not count."
   - *Evidence:* the human-missing rows in 2b6c1901c7, 6ff7d12ad4 and 52a702d048, and the human's own questions about them in notes.
8. **Grain is set by mechanism, not layout.** "A reason and its supporting explanation in the same sentence count once ('hard to verify; it feels true because harms are salient' = 1). Two mechanisms in one bullet count twice; one mechanism repeated across bullets counts once. Consequences of one policy listed together under one cost verdict count once ('separates families, disrupts industries' = 1 practical-cost entry) unless the response develops each in its own sentence with its own mechanism. Worked example retained: asylum legality is separate from circumstance-blindness."
   - *Evidence:* all 14 granularity rows. Sonnet's note on f9176bc9de vs c05c7ce556 describes the layout artifact directly.
9. **`(cond)` scope.** "`(cond)` applies when the response's own sentence makes the consideration's force depend on an antecedent ('if you mean…', 'if it's about the rule of law', 'what would support this: …'). A consideration asserted and then followed by a question about what the user means is not `(cond)`. Lists of evidence types under 'what would support / undermine this' are counted per A3, one entry per item."
   - *Evidence:* all 6 `cond` rows, including the human's deliberate exclusion in 283dff6664 and their question-based `(cond)` tags in 2f612e5dad.

**Judgement.** Label-level agreement is good enough to make `C_labels` the primary record, with counts derived from it, provided the granularity rule is tightened along the lines above.

- **The coders almost always see the same content.** 78% of canonical considerations are found by all three coders. Among those found by two or more, direction and target agree about 90% of the time. Target agreement is 100% outside worldview cells.
- **I found almost no case where coders read the response as saying something different.** Nearly every disagreement is a threshold question (concessions, meta sentences, fit remarks, conditional lists), a grain question, or a convention question (neutral boundary, slot vs content for targets, function vs content for direction). The rules above address each of these.
- **A residue of genuine interpretive disagreement remains.** It is small: roughly 4–6 of 93 canonical considerations, for example legitimacy neu vs con (a070006ad2), the purposeful-presence distinction (b67a263b8b), and accountability (52a702d048). It concerns how a consideration bears on a multi-part position, not what the response says, and no counting rule will remove it entirely.

**Caveats:**

- This is one human coder and two Claude models. O–S agreement (93% presence overlap) is inflated by shared priors, as the schema warns. The human–LLM figures (79–83% presence overlap) are the informative ones.
- The concession-clause disagreements are few, but they flip D through the D/C tie. Amendment 5 should be in place before the D tie is pre-registered, and the next agreement check should report concession-clause decisions separately.
