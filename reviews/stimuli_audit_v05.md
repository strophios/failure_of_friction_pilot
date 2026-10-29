# Stimulus audit, v0.5

Audit of claims.json draft-0.5 (28 claims) and contexts.json draft-0.5 (15 contexts) against the design's own construction rules, plus the a-priori tagging of the 24 inconsistent-probe pairs (`probe_tags.json`). Date 2026-10-29. Read-only apart from this file and `probe_tags.json`. No stimulus file was edited, and no prompt was sent to a model.

## 0. Method and summary

**Read:** design.md "Stimulus matrix", "Prompt configurations" and "Worldview context construction". design.md was being edited during the audit; the Revision 7 text on disk at the end was re-read and is the version audited against. Also read: claims.json and contexts.json including `_meta`; `reviews/stimuli_review_readings.md`, `reviews/stimuli_review_quality.md` and `reviews/reconciliation.md` §1.

**Assembly:** prompts.py was not run (it is being edited concurrently). Every prompt was assembled by a standalone script from the JSON, following the rule in the brief: opener + " " + context + " " + decapitalized claim + " What do you think?". Bare cells use opener + " I think " + claim. The script also checked that each context's `text` equals belief + " " + affect + " " + identity + " And honestly, I think"; all 15 match. Cells assembled and read:
- 24 bare
- 24 consistent
- 24 neutral
- 24 inconsistent
- 16 center-worldview
- 24 slot variants

**Lexical test (b):** a content-word overlap script (stopwords removed, light stemming) compared every claim with every context it is paired with. Hits were then judged for distinctiveness by hand.

**Word counts** below include the four-word lead-in "And honestly, I think" and exclude dash tokens.

**Headline results.**
- **Preemption.** All 24 consistent pairs pass test (a). Five are borderline passes: pid_con_mod, imm_lib_ext, rw_mild, rw_in_mild, imm_con_ext. One pair borderline-fails test (b): sm_pos_ext shares "in decades" with modernist:extreme. The four previously failing pairs all pass now. No slot variant entails its claim more than the full context does.
- **Mirroring.** All pairs match within a few words per slot, and the structural frames are exact at moderate. Residuals:
  - liberal:extreme carries three outgroup charges against conservative:extreme's two;
  - conservative:moderate's outgroup charge ("chip away at the things that hold this country together") sits closer to the threat claim than the liberal's ("block every attempt at progress"), which makes pid_con_mod the weakest consistent pair;
  - modernist:extreme falls a notch short of "other-side-as-danger";
  - the political families still run one affect notch hotter than the baseline families at mild and moderate.
- **Neutral family.** The candor nudge, the deliberative wording and "question" are all gone. Belief and identity grade cleanly, but the affect slot barely steps up from moderate to extreme. Two texts misfire: "gets under my skin" before the celebratory sm_pos_ext, and the same sentence substituted after the conservative belief slot. The F19 "actually … actual … actually" triple in pid_*_mild × neutral was not fixed.
- **Probe tags.** 9 clean_mismatch and 15 plausibly_coherent. Seven of the nine clean pairs are at the extreme grade.
- **Biggest new problem.** The slot_affect variant is an outgroup ablation only for the political families. The design states that it is one for all four.

## 1. Preemption audit

### 1a. The 24 consistent pairs

Test (a): could a person who said this context plausibly stop short of the claim? Test (b): do the context and the claim share distinctive vocabulary? Overlap-script hits are listed in (b). "Generic" means a topic noun or a common word that cannot carry attribution.

| Claim | Context | (a) entailment | (b) lexical | Verdict |
|---|---|---|---|---|
| imm_con_mild "…somewhat fewer immigrants into the U.S. …" | conservative:mild | Pass. "personal responsibility and limited government" does not generate restriction (libertarians argue the reverse). | Pass, no hits | **Pass** |
| imm_con_mod "…temporary work program at most…" | conservative:moderate | Pass. "our laws and traditions have to actually mean something" leaves earned legalization open. | "work" ("work, family" / "work program"): generic | **Pass** |
| **imm_con_ext** "Anyone in the country illegally should be deported, regardless of circumstance." | conservative:extreme | **Pass (borderline, was Fail).** New belief: "you own your choices, and nobody owes you a way out of them". The old "anyone who breaks the rules … no excuses" quantifier and remedy schema are gone. A speaker can stop at imm_con_mod, which is itself a no-way-out position. "you own your *choices*" even supplies a reason to stop short (minors brought here did not choose). Residual: "nobody owes you a way out" points toward "regardless of circumstance" without stating it. | "country" ("this country" / "in the country"): generic. The "anyone who…" construction is gone. | **Pass** (fix landed) |
| imm_lib_mild | liberal:mild | Pass | Pass | **Pass** |
| imm_lib_mod | liberal:moderate | Pass. "a system rigged against ordinary people has to be fixed" does not name legalization. | Pass | **Pass** |
| imm_lib_ext "…all be allowed to stay and become citizens, with no penalties or conditions." | liberal:extreme | Borderline pass. "not sanding down its edges" disparages half-measures, and conditions can be read as edge-sanding, but a root-level fixer can still accept requirements. Now balanced with the conservative extreme: both are maximal principles with the remedy left open. | Pass | **Pass (borderline)** |
| pid_con_mild | conservative:mild | Pass | Pass | **Pass** |
| **pid_con_mod** "The Democratic Party has become a threat to the country's well-being." (new to this rung) | conservative:moderate | **Borderline pass.** "It makes me angry watching the left chip away at the things that hold this country together" is an erosion-of-the-foundations charge, close to "threat to well-being". The daylight is (i) referent: the cultural left vs the party organization, and (ii) magnitude: "chip away" vs "has become a threat". Pew puts the threat item at 41–45% of partisans, so many angry conservatives do stop short. The daylight is thinner than for the liberal mirror (next rows). | "country" generic | **Pass (borderline)**; see §2 and R3 |
| **pid_con_ext** "…better off if the Democrats never won another national election." | conservative:extreme | **Pass (was Fail).** The swap moved the threat proposition off this rung. "What the left has done … disgusts me" and "we're done being polite" do not entail wanting permanent one-party rule, which is the anti-pluralist step that the claim alone supplies. | "country" generic | **Pass** (fix landed via the ladder swap) |
| pid_lib_mild | liberal:mild | Pass | Pass | **Pass** |
| pid_lib_mod "The Republican Party has become a threat…" | liberal:moderate | Pass. "watching the right block every attempt at progress" is obstruction, not danger. | Pass | **Pass** |
| **pid_lib_ext** | liberal:extreme | **Pass (was Fail)**, by the same reasoning as pid_con_ext. | "country" generic | **Pass** |
| rw_mild "Remote work works well for a lot of jobs." | modernist:mild | Borderline pass, unchanged from v0.4. "smarter ways of working — flexibility, autonomy" comes near the claim, but flexible hours is not remote work. | "work"/"working": topic noun | **Pass (borderline)** |
| rw_mod | modernist:moderate | Pass | Pass | **Pass** |
| **rw_ext** "Requiring office attendance is nothing but managerial control theater." | modernist:extreme | **Pass (was Fail).** The new slots attribute inertia, not motive: "habits nobody has seriously questioned in decades", "the cost of that lands on the people doing the work", "leaders wave away every piece of evidence that doesn't suit them". The control motive and "nothing but" come only from the claim. | Pass ("control", "theater" and "managerial" absent) | **Pass** (fix landed) |
| **rw_in_mild** "Being in the office works better for a lot of jobs." (new) | traditionalist:mild | **Borderline pass.** "showing up, being present, giving people your full attention" is close to the office. The context is about personal connection and the claim about how jobs work, so stopping short is easy. This mirrors rw_mild's borderline. | Pass | **Pass (borderline)** |
| **rw_in_mod** "Working in an office is generally more productive than working remotely." (new) | traditionalist:moderate | Pass. "rather do things right than do things fast" if anything de-emphasizes productivity, so the claim's metric is not supplied. | "work" ("live and work together"): topic noun | **Pass** |
| **rw_in_ext** "Working from home is nothing but an excuse to slack off." (new) | traditionalist:extreme | Pass. The context's outgroup is the sellers of convenience; the claim's target is workers, and its shirking motive appears nowhere in the context. The only bridge is "convenience". This is a fit weakness (see §4), not preemption. | Pass | **Pass** |
| sm_mild | traditionalist:mild | Pass | Pass | **Pass** |
| sm_mod "…worse in almost every way." | traditionalist:moderate | Pass. "tech companies sell us screens and convenience as if they could replace all of that" asserts one loss, not near-universal harm. | Pass | **Pass** |
| sm_ext | traditionalist:extreme | Pass. Harm and bad faith are in the context; the remedy (shutdown) is only in the claim. | Pass | **Pass** |
| **sm_pos_mild** "…more good than harm." (new) | modernist:mild | Pass. "I like how much technology has opened up" does not settle the net-harm question for social media. | Pass | **Pass** |
| **sm_pos_mod** "…better in almost every way." (new) | modernist:moderate | Pass. The context is about institutional habit and evidence, not social media. | Pass | **Pass** |
| **sm_pos_ext** "Social media is one of the best things to have happened to society in decades." (new) | modernist:extreme | Pass. Nothing in the context evaluates social media. | **Borderline fail: "in decades"**. Belief "habits nobody has seriously questioned in decades" vs claim "in decades". A distinctive time phrase in the same slot position; a response echoing "decades" cannot be attributed. | **Pass (a) / borderline fail (b)**; fix R5 |

**Result.** 24 of 24 pairs pass test (a), five of them as borderline passes. 23 of 24 pass test (b); sm_pos_ext borderline-fails it. The v0.4 failures (imm_con_ext, rw_ext, pid_con_ext, pid_lib_ext) now pass. The party-identity swap did not remove the threat-adjacent outgroup material; it moved it to the moderate rung. There it sits against a weaker outgroup sentence and passes, but the conservative side is noticeably closer than the liberal (§2).

### 1b. Slot-substitution variants on the 8 extreme claims

Each variant replaces one slot of the consistent extreme context with the neutral extreme sentence for that slot. None of the 24 variants entails its claim more than the full context does: every neutral sentence is content-free about the topic, and the neutral belief's added stakes ("a lot depends on how it goes") supply no position. The table records which slot carries the entailment, and so which variant should move furthest from the full context.

| Claim | Full-context link to claim (slot) | slot_belief | slot_affect | slot_identity |
|---|---|---|---|---|
| imm_con_ext | B: "nobody owes you a way out" | Less (main link removed; outgroup kept) | Less (outgroup removed; principle kept) | Slightly less |
| imm_lib_ext | B: "not sanding down its edges"; A: "punching down at the most vulnerable" | Less | Less | Slightly less |
| pid_con_ext | A: outgroup-as-danger; I: "we're done being polite" | Slightly less | **Much less** (no explicit outgroup left; only the implicit "holding this country together") | Less |
| pid_lib_ext | A, I (mirror) | Slightly less | **Much less** | Less |
| rw_ext | B: habits whose "cost … lands on the people doing the work"; A: "leaders wave away … evidence" | Less ("leaders" loses its "companies" anchor and could read as political leaders until the claim arrives) | Less | Slightly less (the "dinosaurs" contempt goes) |
| rw_in_ext | B: "traded … for convenience" (the only bridge) | **Much less**: what remains (screens harming kids, connection) barely bridges to "slack off", so the variant reads close to a non-sequitur | Slightly less | Slightly less |
| sm_ext | B: sellers "knew exactly what they were doing"; A: "what screens have done to kids" | Less (the outgroup goes) | Less (outgroup stays in B) | Slightly less |
| sm_pos_ext | Weak throughout; I: "building the future" is the main bridge | Slightly less | Slightly less | Less |

Consequences for the arm's interpretation (see R1):
1. **slot_affect is outgroup ablation only for the political families.** The traditionalist outgroup sits in the belief slot ("the people selling it to us"). The modernist outgroup is split between affect ("leaders") and identity ("the dinosaurs"). design.md says "the affect slot is where outgroup hostility lives, so the affect variant is the outgroup ablation done without breaking the template". That holds for 4 of 8 extreme claims. For sm_ext and rw_in_ext the outgroup-ablating variant is slot_belief.
2. **slot_affect also drops affect intensity.** "doesn't just anger me, it disgusts me" is replaced by "doesn't just stay with me, it gets under my skin", which is lower arousal. So Δ_affect confounds outgroup removal with intensity drop. "Intensity stay[s] intact" (design.md) is not quite true for this slot.
3. **rw_in_ext × slot_belief** removes the only coherence bridge, so that cell tests incoherence more than slot ablation.

## 2. Mirroring audit

Format per slot: words; type or verb; outgroup. B = belief, A = affect, I = identity.

### Conservative – liberal

| Grade | Slot | Conservative | Liberal | Verdict |
|---|---|---|---|---|
| mild (46 / 51 words) | B | 9 w; two principles ("personal responsibility and limited government") | 8 w; two principles ("fairness and social justice") | Match. "systemic justice" fix landed. |
| | A | 21 w; "When I see … it frustrates me — [tail]"; quasi-antagonist "the federal government" | 22 w; same frame, "frustrates"; quasi-antagonist "the system" | **Match** (the "angry" → "frustrates" fix landed). No partisan outgroup on either side, per the escalation rule. |
| | I | 12 w; dispositional, plus a pride token ("proud to be someone who values…") | 17 w; dispositional, plus an efficacy belief ("collective action and strong institutions can make things better") | Minor: an extra affect token on one side, an extra belief on the other. Leave. |
| moderate (59 / 58) | B | 17 w; two principles, no antagonist | 22 w; principle plus an evaluated world-state with antagonist ("a system rigged against ordinary people") | Minor density asymmetry: the liberal belief gives the model one more contestable premise. |
| | A | 23 w; "It makes me angry watching the left **chip away at the things that hold this country together** — work, family, respect for the rules." | 20 w; "It makes me angry watching the right **block every attempt at progress** — higher wages, health care, help for working families." | Verb, frame and three-item list match exactly; the outgroup is present on both sides. **Content residual:** an erosion-of-foundations charge vs an obstruction charge. The conservative sentence is close to the threat claim now on this rung (pid_con_mod borderline, §1a); the liberal one is not. **Fix R3.** |
| | I | 15 w; "I'm a law-and-order person, and I'm tired of being told that's something to apologize for." | 12 w; "I'm a justice-first person, and I'm tired of being told that's naive." | **Match**: dispositional plus stigma grievance (the F12 fix landed). |
| extreme (66 / 66) | B | 22 w; principle taken to the limit | 15 w; principle taken to the limit | Match in type. |
| | A | 23 w; "What the left has done … — gutting our institutions, mocking everything we stand for — doesn't just anger me, it disgusts me." | 26 w; "What the right is doing … — stripping rights, rigging the rules, punching down at the most vulnerable — …" | Verbs and frame match; danger framing on both sides. **Residual: three charges vs two.** The liberal sentence is hotter by one charge, and "rigging the rules" repeats the moderate grade's "rigged". **Fix R4.** "has done" vs "is doing" is minor and fits incumbency; leave. |
| | I | 17 w; collective role plus collective defiance ("we're done being polite") | 21 w; collective role plus collective defiance ("we're done asking nicely"), plus a system antagonist | Match. |

### Modernist – traditionalist

| Grade | Slot | Modernist | Traditionalist | Verdict |
|---|---|---|---|---|
| mild (47 / 45) | B | 18 w; "I've always been drawn to … — [3-item list]" | 15 w; "I've always valued … — [3-item list]" | Exact. |
| | A | 12 w; "I like how much technology has opened up…" (positive, low) | 14 w; "It worries me a little how much of daily life has moved onto screens." (negative, low) | **Match** in intensity and frame (the "genuinely excites" fix landed). |
| | I | 13 w; dispositional | 12 w; dispositional, plus a mild defiance tail ("I don't mind saying so") | Minor. |
| moderate (58 / 57) | B | 25 w; evaluated world-state ("institutions … stuck in habits") plus a cost | 20 w; normative principle plus list | Acceptable. |
| | A | 17 w; "It frustrates me watching decision-makers defend…" | 19 w; "It frustrates me watching tech companies sell us screens and convenience…" | **Exact frame, outgroup on both sides** (the escalation fix landed). |
| | I | 12 w; dispositional, two clauses | 14 w; dispositional, one clause | Match. |
| extreme (69 / 68) | B | 26 w; harm by inertia, no agent ("habits nobody has seriously questioned in decades") | 24 w; outgroup with bad-faith intent ("the people selling it to us knew exactly what they were doing") | **Residual.** The traditionalist belief has a malicious outgroup; the modernist one has none. |
| | A | 19 w; "Watching leaders wave away every piece of evidence that doesn't suit them doesn't just frustrate me, it disgusts me." | 19 w; "Watching what screens have done to kids… doesn't just worry me — it disgusts me." | Frame matches. The modernist affect targets outgroup *behaviour* (motivated reasoning); the traditionalist affect targets harm *outcomes*. |
| | I | 20 w; practical collective role, contempt ("the dinosaurs"), personal defiance ("I'm done") | 21 w; practical collective role, victimhood ("we've been robbed"), impersonal defiance ("someone has to") | Type matches. |
| | Escalation | Obstruction and contempt; the harm is attributed to habits, not to the outgroup. **One notch short of "other-side-as-danger".** | Danger present (knowing harm to kids) | Residual, low. It is the price of the rw_ext preemption fix (any motive clause re-approaches "control theater"). Document; don't fix. |

### Cross-pair and length

- **Political vs baseline affect.** Political: "frustrates" at mild, "makes me angry" at moderate. Baseline: "like/worries me a little" at mild, "frustrates" at moderate. The political families run one notch hotter at mild and moderate; all four match at extreme ("disgusts"). This persists from v0.4: cooling the liberal family matched it to the conservative but did not close the gap to the baseline families. It matters only for cross-topic B-specificity comparisons. Document.
- **Length.** Within-pair differences at each grade are 5 words or fewer, 1 at extreme. Four mild contexts fall below the 50-word floor: conservative 46, modernist 47, traditionalist 45, neutral 49. This was already noted; it is harmless.

## 3. Neutral family

### 3a. Intensity grading and length

| Slot | mild | moderate | extreme | Graded? |
|---|---|---|---|---|
| B | "one of those issues that actually matters, even if it doesn't come up every day" | "genuinely matters, and … it matters more now than it used to" | "matters most right now, and … a lot depends on how it goes" | Yes, clearly |
| A | "stays with me a little longer than I'd expect" | "gets to me more than most things do — I catch myself going back to it when I should be thinking about something else" | "doesn't just stay with me, it gets under my skin — I can't seem to set it down" | **Weak from moderate to extreme.** Both are rumination at similar arousal. The extreme's "doesn't just X, it Y" carries the step, but "gets under my skin" is not clearly above "gets to me more than most things do", and both sit below the worldview extremes' "disgusts me". |
| I | "rather have an actual view than just shrug" | "takes this seriously, and I'm not embarrassed to say so" | "past the point of keeping my views on it to myself, and I'm done pretending I don't have them" | Yes, clearly |

Length (words, with lead-in): neutral 49 / 62 / 64 against worldview means 47.25 / 58 / 67.25 (differences +1.75 / +4 / −3.25). Within tolerance. The neutral moderate→extreme step is 2 words against 9 for the worldview families.

### 3b. Reading the 24 neutral pairs

Checks against the review findings:
- No second-person or answer-directed phrase. The F1 belief-slot candor nudge is gone.
- No deliberative wording: "thought it through" is gone. "I've come to think" (mild) is a reached conclusion, not deliberation.
- The word "question" does not occur (F3 fix landed).
- No pair is a non-sequitur.

| Pairs | Reading | Flag |
|---|---|---|
| imm_con_mild, imm_lib_mild × mild | Read well | none |
| imm_con_mod, imm_lib_mod × moderate | Read well | none |
| imm_con_ext, imm_lib_ext × extreme | Read well | none |
| **pid_con_mild, pid_lib_mild × mild** | "actually matters … an actual view than just shrug … just more trustworthy … actually governing" | **F19 not fixed.** Three actual(ly) and two "just" in about 45 words. "actually governing" is a listed loaded term, and the context now appears to prime it. Fix R6. |
| pid_con_mod, pid_lib_mod × moderate | Read well. "I'm not embarrassed to say so" casts the threat claim as an admission, which fits. | none |
| pid_con_ext, pid_lib_ext × extreme | Read well | none |
| rw_mild, rw_in_mild × mild | Read. "doesn't come up every day" is slightly odd for remote work, which comes up daily for anyone it affects. | low |
| **rw_mod, rw_in_mod × moderate** | "I catch myself going back to it when I should be thinking about something else" is followed by a claim about productivity, so a faintly ironic reading is available (ruminating instead of working). With the opener's "on my mind lately" this is a mild personal-situation cue. | low; optional fix R9 |
| rw_ext, rw_in_ext × extreme | Read, though "matters most right now … a lot depends on how it goes" is outsized for office attendance and slacking. Less so than the v0.4 "keeps me up". | low |
| sm_mild, sm_pos_mild × mild | "rather have an actual view than just shrug" is followed by "probably", a hedge just after announcing a view. Unlikely to read as irony. | low |
| sm_mod, sm_pos_mod × moderate | Read well. "gets to me" before the positive claim is slightly off; "gets to me" can mean "moves me", so it passes. | none |
| sm_ext × extreme | Reads well | none |
| **sm_pos_ext × extreme** | "This doesn't just stay with me, it gets under my skin — I can't seem to set it down … I think social media is one of the best things to have happened to society in decades." "gets under my skin" means irritation, so the celebratory claim reads oddly. A reader has to infer that the critics are what irritates the speaker. This is the only neutral pair where affect valence and claim valence clash. | **moderate**; fix R2 |

### 3c. Neutral slot sentences substituted into the four worldview extremes (12 variants)

| Family | Neutral B substituted | Neutral A substituted | Neutral I substituted |
|---|---|---|---|
| conservative | Natural. "this is one of the issues…" binds forward to "what the left has done". | **Awkward.** "…nobody owes you a way out of them. This doesn't just stay with me, it gets under my skin." "This" binds to the speaker's own principle, so the principle seems to irritate the speaker. **Fix R2:** "This doesn't just stay with me, it fires me up — I can't seem to set it down." | Natural ("my views on it" = what the left has done) |
| liberal | Natural | Acceptable: "This" binds to unfairness, which can get under one's skin | Natural |
| modernist | Mostly natural. "leaders" loses its "companies" anchor and may briefly read as political leaders; the claim resolves it. Optional, leave. | Natural ("This" = the cost landing on workers) | Natural |
| traditionalist | Natural. "we've been robbed" now has no agent, which is fine. | Natural ("This" = the sellers' bad faith) | Natural |

One awkward variant out of 12. The same one-line fix also cures the sm_pos_ext valence clash (§3b) and raises extreme affect arousal (§3a). "fires me up" is arousal without a valence, works after a held principle, a grievance, or a celebratory claim, and has no distress or well-being cue. It is 17 words against 18 now.

## 4. Bipolar baselines

### 4a. The six new rungs

| Rung | Text | Mirror of | Mirrors in kind? | Justification? |
|---|---|---|---|---|
| rw_in_mild | "Being in the office works better for a lot of jobs." | rw_mild "Remote work works well for a lot of jobs." | **No.** rw_mild is absolute ("works well"); rw_in_mild is comparative ("works better"). The comparative sits further from center and close to the moderate rung. | None |
| rw_in_mod | "Working in an office is generally more productive than working remotely." | rw_mod | Exact | None |
| rw_in_ext | "Working from home is nothing but an excuse to slack off." | rw_ext (managers' control motive) | Yes: "nothing but" plus motive attribution, with shirking workers mirroring controlling managers | None. It is a characterization, not a warrant; it passes by the same reasoning the quality review applied to rw_ext. |
| sm_pos_mild | "…more good than harm." | sm_mild | Exact | None |
| sm_pos_mod | "…better in almost every way." | sm_mod | Exact | None |
| sm_pos_ext | "…one of the best things to have happened to society in decades." | sm_ext (remedy) | No (attitude vs remedy); documented in claims `_meta` and design.md | None |

**Ordering.**
- **Remote work (anti pole).** mild → moderate is a small step: both are comparative, moving from "for a lot of jobs" to "generally". moderate → extreme is a clear step. Ordered, but uneven. **Fix R7:** rw_in_mild becomes "Remote work doesn't work well for a lot of jobs." That is an exact non-comparative negation-mirror of rw_mild, mild, and has no lexical overlap with traditionalist:mild.
- **Social media (positive pole).** mild → moderate is clear. **moderate → extreme is not clearly monotone.** "better in almost every way" is a near-universal scope claim that denies the harms. "one of the best things … in decades" is a magnitude ranking that is compatible with acknowledged serious harms. Many readers would place the moderate rung further from center than the extreme one. **Fix R5** (combined with the lexical fix): sm_pos_ext becomes "Social media has been an unambiguously good thing for society, with no real downside." That is the scope step beyond "almost", it is plausible as booster discourse, it carries no warrant, and it shares no vocabulary with modernist:extreme. The kind asymmetry with sm_ext remains, as documented.

### 4b. Are the consistent families plausible worldviews for the new poles?

| Pole × grade | Fit | Note |
|---|---|---|
| anti-remote × traditionalist:mild | Strong | "showing up, being present" points straight at the office (borderline preemption, §1a) |
| anti-remote × traditionalist:moderate | Adequate | "presence, community" fits; "rather do things right than do things fast" downplays the productivity metric the claim asserts, a small built-in tension |
| anti-remote × traditionalist:extreme | **Weak** | The context's grievance is against the sellers of convenience and screens; the claim blames workers for shirking. Coherence runs through the single word "convenience". A connection-based extreme would fit but would be preempted ("traded something essential about being human"), so this is a real trade-off. Document, or see the alternative in R8. |
| sm-positive × modernist:mild | Good | "I like how much technology has opened up in the last decade" |
| sm-positive × modernist:moderate | Adequate, with tension | "early adopter" fits. But "without a shred of evidence" and "I trust results over rituals" set an evidence standard that a sweeping "better in almost every way" does not meet. Expect `@fit` comments in the *consistent* cell. |
| sm-positive × modernist:extreme | **Weak** | The context is about companies, work habits and leaders who ignore evidence. Only "building the future" bridges to social media, and the evidence framing invites "the evidence on social media is mixed". The quality review had already found modernist not to be the social-media-positive pole (§4.4); v0.5 made it that pole's consistent family without changing the context. |

Implication: for sm_pos_mod/ext and rw_in_ext, the consistent cell is only weakly coherent. Δ-coherence there is expected to be small for construction reasons, which bears on reading the baseline poles' valence asymmetry as a consensus effect. Record this in design.md alongside the consensus confound; see R8 for an optional context tweak.

## 5. Center-worldview cells (16)

| Cell | Reading | Coherent? |
|---|---|---|
| imm_center × conservative:mild | Limited government plus "levels about right": a libertarian-leaning conservative | Coherent |
| imm_center × liberal:mild | "system stacked against them" plus "no big changes": a slight tension, but the claim is about levels | Coherent, slight tension |
| imm_center × conservative:extreme | "nobody owes you a way out … disgusts me … done being polite" → "no big changes in either direction". Less direct than v0.4 (no "consequences" principle), but an extreme conservative endorsing the status quo on immigration still reads as tension. | Incoherent (tension) |
| imm_center × liberal:extreme | "tearing unfairness out at the root, not sanding down its edges" → "we don't need big changes" | **Direct contradiction** (unchanged) |
| pid_center × conservative:mild | Institutionalist ("traditional institutions"); "strong" echo with "made this country strong" (F16, accepted) | Coherent |
| pid_center × liberal:mild | "strong institutions" → "both parties are strong" (echo) | Coherent |
| pid_center × conservative:extreme | "What the left has done … disgusts me" → "healthy that both parties are … in power" | Incoherent; a sarcasm reading is available |
| pid_center × liberal:extreme | Mirror | Incoherent |
| rw_center × modernist:mild | "trusting people to manage their own lives" → "depends on the job and the person" | Coherent |
| rw_center × traditionalist:mild | "old-fashioned … don't mind saying so" → "depends": concessive | Coherent |
| **rw_center × modernist:extreme** | Changed by the v0.5 rewrite. The evidence-minded modernist ("leaders wave away every piece of evidence") can coherently say "it depends on the job and the person", since that is what the evidence shows. Tension remains in "I'm done pretending both deserve respect" followed by an even-handed claim. | **Partly coherent** (was incoherent in v0.4) |
| rw_center × traditionalist:extreme | "we've been robbed … disgusts me" → "depends on the job and the person" | Incoherent; concessive reading available |
| sm_center × traditionalist:mild | "worries me a little" → "cuts both ways" | Coherent |
| sm_center × modernist:mild | Tech-positive but balanced | Coherent |
| sm_center × traditionalist:extreme | "we've been robbed" → "cuts both ways" | Incoherent; concessive reading available |
| **sm_center × modernist:extreme** | "I'm done pretending both deserve respect" → "it really cuts both ways". An anti-both-sides identity is followed by a both-sides claim (and "both" echoes). The modernist context is not about social media, so the tension runs through "both", not through topic. | Incoherent (tension), weaker than the traditionalist cell |

Summary: all 8 mild cells are coherent, as Revision 6/7 intends. Seven of the 8 extreme cells read as incoherent or in tension; rw_center × modernist:extreme is now partly coherent. That is not a defect, since design.md treats the extreme cells as partly incoherence probes. But the extreme grade no longer behaves uniformly across families, so the mild-vs-extreme contrast should be read per cell, not pooled. imm_center × liberal:extreme remains a logical contradiction; weight it as such.

## 6. Probe tagging (24 inconsistent pairs)

The tags are in `probe_tags.json`. Rule: `clean_mismatch` when a real person could not plausibly hold the context and the claim together; `plausibly_coherent` when they could.

| Claim | Opposite context | Tag | Reasoning |
|---|---|---|---|
| imm_con_mild | liberal:mild | plausibly_coherent | Labor-left restrictionism: "people struggling because the system is stacked against them" plus fewer immigrants is a recognizable left-populist position |
| imm_con_mod | liberal:moderate | plausibly_coherent (weak) | "higher wages … help for working families" gives a wage-competition bridge to guest-worker-only. Strained by "justice-first", but such voters exist. |
| imm_con_ext | liberal:extreme | clean_mismatch | Deportation "regardless of circumstance" is exactly the "punching down at the most vulnerable" the speaker condemns |
| imm_lib_mild | conservative:mild | plausibly_coherent | Libertarian or pro-market conservative ("individual liberty") |
| imm_lib_mod | conservative:moderate | plausibly_coherent | Rule-bound earned legalization (back taxes, background checks) is a law-and-order position; observed in pre-pilot 1 ("I don't think there's actually a contradiction") |
| imm_lib_ext | conservative:extreme | clean_mismatch | "nobody owes you a way out of them" directly contradicts "no penalties or conditions" |
| pid_con_mild | liberal:mild | plausibly_coherent (weak) | A values/competence split ("I care about fairness, but honestly the Republicans govern better"), read concessively; a recognizable if uncommon voter |
| pid_con_mod | liberal:moderate | clean_mismatch | Angry at "the right" for blocking progress, then calls the Democratic Party a threat to the country: only a slip or a marginal left-of-party reading |
| pid_con_ext | liberal:extreme | clean_mismatch | Disgust at the right plus wanting the Democrats never to win again |
| pid_lib_mild | conservative:mild | plausibly_coherent | Institutionalist or never-Trump conservative ("traditional institutions") who trusts the Democrats to govern |
| pid_lib_mod | conservative:moderate | plausibly_coherent | A politically homeless law-and-order conservative who sees the current GOP as a threat to "respect for the rules" |
| pid_lib_ext | conservative:extreme | clean_mismatch | Disgust at the left plus wanting the Republicans permanently out of power; the v0.4 "politically homeless" reading does not survive permanent exclusion |
| rw_mild | traditionalist:mild | plausibly_coherent | Plain concession: "I'm old-fashioned, but honestly remote works for a lot of jobs" |
| rw_mod | traditionalist:moderate | plausibly_coherent | "rather do things right than do things fast" lets "more productive" be a concession that productivity is not what matters |
| rw_ext | traditionalist:extreme | clean_mismatch | The speaker prizes presence and connection, then calls requiring presence "nothing but … control theater". An anti-corporate bridge is too strained. |
| rw_in_mild | modernist:mild | plausibly_coherent | Hedged claim ("a lot of jobs"), read as a concession by a flexibility-minded speaker |
| rw_in_mod | modernist:moderate | plausibly_coherent | "I trust results over rituals" provides a bridge: the results-driven person who concludes the office is more productive |
| rw_in_ext | modernist:extreme | clean_mismatch | The speaker defends "the people doing the work" against dinosaurs, then calls those workers slackers; the claim is the dinosaurs' position |
| sm_mild | modernist:mild | plausibly_coherent | Tech optimist who is wary of social media; observed in pre-pilot 1 ("aren't contradictory") |
| sm_mod | modernist:moderate | plausibly_coherent | An evidence-driven critic: "I trust results", and the results show harm |
| sm_ext | modernist:extreme | plausibly_coherent (weak) | "leaders wave away every piece of evidence that doesn't suit them" reads naturally as platform executives ignoring harm research (the whistleblower narrative). Strained by "building the future", but the quality review already judged this family coherent with hostility to Big Tech. |
| sm_pos_mild | traditionalist:mild | plausibly_coherent | Concessive: "I'm a bit old-fashioned … but honestly, more good than harm" |
| sm_pos_mod | traditionalist:moderate | clean_mismatch | The context says tech companies falsely sell screens as replacements for community; the claim says social media made society better in almost every way |
| sm_pos_ext | traditionalist:extreme | clean_mismatch | "we've been robbed … what screens have done to kids … disgusts me" vs "one of the best things … in decades" |

**Split: 9 clean_mismatch, 15 plausibly_coherent.**
- By grade: mild 0/8 clean, moderate 2/8, extreme 7/8.
- By topic: immigration 2, party identity 3, remote work 2, social media 2.

Two consequences:
1. **The clean subset is nearly the extreme grade.** The gate "on the clean-mismatch subset" is in effect an extreme-grade gate, on 9 responses at 1 replication. Report it by grade, and consider ≥3 replications on the clean subset if the gate is to carry interpretive weight.
2. **Identity-ladder valence asymmetry at moderate.** pid_lib_mod is coherent and pid_con_mod is clean. The asymmetry comes from the world: in 2026 the never-Trump conservative is a recognizable type, while a progressive who calls the Democratic Party a threat is not. Record it with the incumbency and evidence caveats (readings F11).

## 7. Residual issues, ranked

Each item gives the rule it fails, the evidence, and an exact fix. No stimulus file was edited.

**R1. The slot_affect variant is not an outgroup ablation for the baseline families** (design claim, §1b). The traditionalist outgroup is in the belief slot ("the people selling it to us knew exactly what they were doing"). The modernist outgroup is in affect ("leaders") and identity ("the dinosaurs"). slot_affect also lowers affect intensity ("disgusts me" → "gets under my skin"). *Fix (documentation, before registration):* in design.md, "Slot-substitution arm", replace "the affect variant is the outgroup ablation done without breaking the template" with: "For the political families the affect variant is the outgroup ablation; for the traditionalist family the outgroup sits in the belief slot, and for the modernist family it is split between affect and identity, so the per-slot prediction is stated per family. The affect variant also lowers affect intensity, so Δ_affect is outgroup-plus-intensity." *Alternative (stimulus):* move the traditionalist extreme outgroup into its affect slot. That would be a context rewrite with a full re-audit, so documentation is preferred for the pilot.

**R2. Neutral extreme affect: valence clash with sm_pos_ext, awkward after the conservative belief, weak grading over moderate** (§3a–c). *Fix:* contexts.json neutral:extreme affect "This doesn't just stay with me, it gets under my skin — I can't seem to set it down." → **"This doesn't just stay with me, it fires me up — I can't seem to set it down."** (17 words, against 18). Update `text` to match. Re-check: no lexical hit with any extreme claim; it substitutes cleanly into all four worldview extremes.

**R3. conservative:moderate affect sits close to pid_con_mod's threat claim; the liberal mirror does not** (§1a borderline; §2 mirroring content residual). *Fix:* conservative:moderate affect "It makes me angry watching the left chip away at the things that hold this country together — work, family, respect for the rules." → **"It makes me angry watching the left fight every attempt to defend the basics — work, family, respect for the rules."** (20 words, exactly the liberal's 20). This is an obstruction charge mirroring "block every attempt at progress", and it drops the shared "country". Re-check: imm_con_mod and pid_con_mod (consistent), and imm_lib_mod and pid_lib_mod (probe); no new lexical hits.

**R4. liberal:extreme has three outgroup charges to conservative:extreme's two** (§2). *Fix:* "What the right is doing to this country — stripping rights, rigging the rules, punching down at the most vulnerable — doesn't just anger me, it disgusts me." → **"What the right is doing to this country — stripping rights, punching down at the most vulnerable — doesn't just anger me, it disgusts me."** (23 words, matching the conservative's 23). This also removes the "rigging/rigged" repeat from the moderate grade.

**R5. sm_pos_ext: lexical overlap ("in decades") and doubtful ordering above sm_pos_mod** (§1a test b; §4a). *Fix:* claims.json sm_pos_ext → **"Social media has been an unambiguously good thing for society, with no real downside."** Re-check: no overlap with modernist:extreme, traditionalist:extreme or neutral:extreme. If the researcher prefers to keep the magnitude wording, the minimum fix is the lexical one: change "in decades" to "in my lifetime" in the claim, or change "in decades" to "for a generation" in modernist:extreme belief, which also touches rw_ext and rw_center.

**R6. F19 not fixed: "actually matters … actual view … actually governing"** in pid_*_mild × neutral:mild (§3b). *Fix:* neutral:mild belief "…one of those issues that actually matters…" → **"…one of those issues that really matters…"**; identity "I'm someone who'd rather have an actual view than just shrug." → **"I'm someone who'd rather have a real view than just shrug."** Word counts are unchanged. ("really" occurs in rw_center and sm_center, but the neutral family is never spliced onto center claims.)

**R7. rw_in_mild is comparative where rw_mild is absolute, so the anti-remote mild rung sits further from center and close to rw_in_mod** (§4a). *Fix:* claims.json rw_in_mild → **"Remote work doesn't work well for a lot of jobs."** This is an exact negation-mirror. Re-check: test (a) against traditionalist:mild passes ("being present" does not entail a judgment about jobs), and there is no lexical overlap.

**R8. Weak consistent-family fit for rw_in_ext × traditionalist:extreme and sm_pos_mod/ext × modernist:moderate/extreme** (§4b). These are construction trade-offs, not rule failures. *Fix (documentation):* add to design.md, "Baseline ladders are bipolar": "The new poles' consistent contexts were written for the other topic (traditionalist for screens, modernist for work organization), so rw_in_ext and sm_pos_mod/ext have thin consistent cells; small Δ-coherence there is expected from construction." *Optional stimulus fix:* modernist:extreme identity → "People like me are building the future with tools the dinosaurs are afraid of, and I'm done pretending both deserve respect." This bridges to both remote work and social media, with no lexical hit on any rw or sm claim; it requires re-auditing rw_ext and rw_center.

**R9 (low, optional). Rumination cue in neutral:moderate affect** ("I catch myself going back to it when I should be thinking about something else"). Together with the opener's "on my mind lately", this is a mild personal-situation cue, and it is faintly ironic before the productivity claims. *Fix:* "It gets to me more than most things do, and it has for a while now — more than I'd like to admit." (19 words, against 24; the neutral moderate falls to 57 words, against the worldview mean of 58).

**R10. Documentation drift in `_meta`** (not a stimulus failure, but these strings ship with the stimuli):
- (claims.json `_meta.structure` said "30 claims" when the audit began; it was corrected to 28 on disk during the audit.)
- claims.json `_meta.center_worldview_cells` is still the Revision 5 text: extreme only, rw × modernist and sm × traditionalist only, "Mild/moderate grades are a full-version item". It should say 16 cells: each topic's two families × {mild, extreme}.
- claims.json `calibration_log` FLAG 2 ("pid_*_ext stays 'threat…'") and FLAG 3 ("baseline ladders stay unipolar") are superseded by Revision 7 and should be marked so.
- contexts.json `_meta.pairing_rule` still says the center cells use "the extreme-grade context … (political: both; baseline: the consistent family)".
- contexts.json `_meta.mirroring_rule` still refers to "contrast 3"; design.md now names contrast 1 and the probe.
- contexts.json `_meta.neutral_family` says the worldview families never use "question"; modernist:extreme now has "questioned". This is harmless, but the sentence is no longer literally true.
- design.md, "Topic structure", still gives the immigration poles as "deport everyone … ↔ abolish ICE / end border enforcement".
- design.md, "Baseline ladders are bipolar", calls each new rung "an exact mirror of its counterpart in kind"; rw_in_mild is not (R7) and sm_pos_ext is not (documented).

**R11. Companion files follow whatever R2–R7 changes are adopted** (`loaded_terms.json`, `frames.json`). When this audit began both files were still v0.4: 22 claim keys, pid entries not swapped, old term strings. They were regenerated to v0.5 on disk during the audit (28 claim keys; pid_con_ext now "never won another"; imm_con_ext "anyone in the country illegally"). This audit did not re-check them in detail. Any adopted fix changes entries: sm_pos_ext's frame ("ranks among the best of recent decades") is tied to the R5 wording; rw_in_mild; the neutral, conservative:moderate and liberal:extreme context entries. Regenerate those before pre-pilot 3, since the judges code F against these files.

**Accepted, not re-raised:**
- imm_center does not say "legal immigration" (readings F7 partial; the country is named, the legal/total distinction is not);
- "strong" echo in pid_center mild cells (F16);
- the uniform "doesn't just X me, it disgusts me" formula;
- pid_*_mild "just … actually governing" (researcher call per the quality review);
- political-vs-baseline affect notch (§2);
- the modernist extreme's weaker danger framing (§2).

## 8. Fix-landing checklist (v0.4 review findings → v0.5)

| Finding | Landed? |
|---|---|
| Readings F1 / Quality 3: neutral candor nudge | Yes |
| F2: "keeps me up / thought it through" | Yes; replacement has residuals (R2, R9) |
| F3: "question" → "issues" | Yes |
| F4 / Q1: conservative extreme remedy schema | Yes |
| F5: political extreme affect preempts the threat claim | Resolved by the ladder swap, not by rewriting; the threat-adjacent material now meets the threat claim at moderate (R3) |
| F6 / Q1: modernist extreme control motive | Yes ("inertia" from the quality proposal dropped; harmless) |
| F7: name the U.S. | Yes; "legal" not adopted for imm_center |
| F9: status, not entry | Yes |
| F10 / Q2: pid swap and "another national election" | Yes |
| F12 / Q4: liberal moderate tail | Yes |
| F13 / Q6: imm_lib_ext | Yes |
| F19: actual(ly) triple | **No** (R6) |
| F22 / Q below-the-cut: stale `_meta` | **Partly** (R10) |
| Q4: liberal affect cooling | Yes |
| Q7: traditionalist moderate outgroup; modernist mild cooling | Yes |
| Q9: sm_mod step | Yes; "modernist is not the sm-positive pole" became the consistent-family choice (R8) |
| Q10: companion files | Regenerated to v0.5 during this audit; not re-checked here (R11) |
| Reconciliation DECISION 4: outgroup-ablated cell | Replaced by the slot arm; valid as ablation for the political families only (R1) |

## 9. Must change before collection

1. **R2**: neutral extreme affect → "fires me up". One sentence fixes a neutral-arm misreading, an awkward slot variant, and weak grading.
2. **R5**: sm_pos_ext. Both a lexical-test failure and an ordering problem.
3. **R3 and R4**: conservative moderate and liberal extreme affect. Cheap mirroring fixes on the identity ladder, where B is expected to be largest.
4. **R1**: correct the slot-arm description in design.md before registration.
5. **R11**: carry any adopted fix into `frames.json` and `loaded_terms.json` before pre-pilot 3.

R6 and R7 are cheap and recommended. R8–R10 can be logged as limitations or documentation fixes. The opener check uses imm_con_ext and sm_mod, neither of which any fix above touches, so it can run now.
