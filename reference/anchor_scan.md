# Survey Instrument Anchor Scan for LLM-Behavior Experiment
## Political Claims Stimulus Design

This document compiles exact survey items from established instruments (ANES, GSS, Pew Research) to anchor the bipolar Likert-style ladders for the LLM-behavior experiment stimulus design. Two political topics are covered: (1) **immigration policy** and (2) **partisan identity/us-vs-them claims**.

---

## 1. ANES Immigration Items

### 1.1 Border Wall Question
**Question:** "Do you favor, oppose, or neither favor nor oppose building a wall on the U.S. border with Mexico?"

- **Variable:** V201424
- **Label:** PRE: Favor or oppose building a wall on border with Mexico
- **Response Scale:** 3-point (Favor / Oppose / Neither)
- **Years:** 2020 Time Series Study
- **Source:** ANES 2020 Time Series Study
- **Availability:** https://electionstudies.org

### 1.2 Unauthorized Immigration Policy (Multi-option Scale)
**Question:** "Which comes closest to your view about what government policy should be toward unauthorized immigrants now living in the United States?"

**Response Options (Ordered from Most Restrictive to Most Permissive):**
1. Make all unauthorized immigrants felons and send them back to their home country
2. Have a guest worker program that allows unauthorized immigrants to remain in the United States in order to work, but only for a limited amount of time
3. Allow unauthorized immigrants to remain in the United States and eventually qualify for U.S. citizenship, but only if they meet certain requirements like paying back taxes and fines, learning English, and passing background checks
4. Allow unauthorized immigrants to remain in the United States and eventually qualify for U.S. citizenship, without penalties

- **Variable:** V201417
- **Response Scale:** 4-point ordered categorical
- **Years:** 2020 Time Series Study (and earlier waves)
- **Source:** ANES Time Series
- **Availability:** https://electionstudies.org

### 1.3 Border Security Spending
**Question:** "What about tightening border security to prevent illegal immigration? Should federal spending on tightening border security to prevent illegal immigration be increased, decreased, or kept the same?"

- **Variable:** V201306
- **Response Scale:** 3-point (Increased / Decreased / Kept the same)
- **Years:** 2020 Time Series Study
- **Source:** ANES 2020 Time Series Study
- **Availability:** https://electionstudies.org

**NOTE:** ANES lacks a dedicated 7-point immigration scale comparable to GSS LETIN. The multi-option unauthorized immigration question (V201417) provides granular policy differentiation but is categorical rather than scalar.

---

## 2. GSS Immigration Items

### 2.1 Immigration Levels (LETIN1A)
**Question:** "Do you think the number of immigrants from foreign countries who are permitted to come to the United States to live should be increased a lot, increased a little, left the same as it is now, decreased a little, or decreased a lot?"

- **Variable:** LETIN1A
- **Response Scale:** 5-point ordered (Increased a lot / Increased a little / Left the same / Decreased a little / Decreased a lot)
- **Available Years:** Appears in GSS waves through 2024 (at minimum: 2020, 2021, 2022, 2024)
- **Source:** General Social Survey (GSS), NORC at the University of Chicago
- **Availability:** https://gss.norc.org / https://gssdataexplorer.norc.org

**Codebook/Documentation References:**
- GSS 2022 Codebook: https://gss.norc.org/content/dam/gss/get-documentation/pdf/codebook/GSS%202022%20Codebook.pdf
- Quick Guide to 2024 Variables: https://gss.norc.org/content/dam/gss/get-documentation/pdf/other/GSS%202024%20Release%20Variables%20R2.pdf
- GSS Data Explorer: https://gssdataexplorer.norc.org/variables/1611/vshow

---

## 3. Affective & Identity Polarization Instruments

### 3.1 ANES Feeling Thermometer (0–100 Scale)
**Question:** "I'd like to get your feelings toward some of our political leaders and public figures. I'll read the name of a person and I'd like you to rate that person using something we call the feeling thermometer. Ratings between 50-100 degrees mean you feel favorably and warm toward the person; ratings between 0 and 50 degrees mean you don't feel favorably toward the person and don't care too much for that person. If you don't feel particularly warm or cold toward a person, you would rate them at 50 degrees."

- **Applied to:** Democratic Party, Republican Party (in separate instances)
- **Response Scale:** 0–100 (0 = "as cold and negative as possible"; 50 = neutral; 100 = "as warm and positive as possible")
- **Years:** Fielded in every ANES Time Series year since 1968
- **Source:** American National Election Studies (ANES)
- **Availability:** https://electionstudies.org (questionnaires and codebooks for each year)
- **Recent Examples:** ANES 2016, 2020 Time Series questionnaires

**Coverage Note:** This 0–100 scale provides continuous measurement of affect toward the parties; widely used in affective polarization research.

---

### 3.2 Pew Research: Party Threat ("Policies Threaten Nation's Well-being")
**Question:** "Would you say the [other] party's policies are so misguided that they threaten the nation's well-being, or wouldn't you go that far?"

- **Response Options:** Yes / No (or variants: "Threaten the nation's well-being" vs. "Wouldn't go that far")
- **Response Scale:** Binary
- **Years Fielded:** 2014 (original baseline); 2016 (comparative wave)
- **Results (2014):** 36% of Republicans and Republican leaners; 27% of Democrats and Democratic leaners
- **Results (2016):** 45% of Republicans; 41% of Democrats
- **Source:** Pew Research Center, "Political Polarization and Growing Partisan Antipathy" (June 2014); "Partisanship and Political Animosity in 2016" (June 2016)
- **Availability:** https://www.pewresearch.org/politics/2014/06/12/section-2-growing-partisan-antipathy/

**Methodological Note:** This exact wording ("threaten the nation's well-being") is the key item you identified and is highly reliable for anchoring the "extreme" rung of the party-identity ladder (liberal/conservative pair).

---

### 3.3 Pew Research: Emotional Responses (Fear, Anger, Frustration)
**Emotions Measured:** Respondents were asked whether the [other] party makes them feel:
- Afraid
- Angry
- Frustrated
- Hopeful
- Enthusiastic
- Proud

**Results (2016):**
- Fear: 55% of Democrats say Republican Party makes them "afraid"; 49% of Republicans say same about Democratic Party
- Anger: 47% of Democrats; 46% of Republicans say the other party makes them "angry"
- Frustration: 58% of Democrats; 57% of Republicans say the other party makes them "frustrated"
- **Negative feelings aggregate:** 87% in both parties report at least one negative feeling about the other party

**Survey Details:**
- **Sample Size:** 4,385 adults
- **Sample Frame:** Pew Research Center's American Trends Panel (nationally representative)
- **Fielded:** March 2–28 and April 5–May 2, 2016
- **Source:** Pew Research Center, "Partisanship and Political Animosity in 2016" (June 22, 2016)
- **Availability:** https://www.pewresearch.org/politics/2016/06/22/partisanship-and-political-animosity-in-2016/

**Response Scale:** UNVERIFIED (results are reported as percentages; exact response scale—binary yes/no, or other—not explicitly stated in published report)

**Specific Section:** https://www.pewresearch.org/politics/2016/06/22/6-how-do-the-political-parties-make-you-feel/

---

### 3.4 Pew Research: Party Favorability ("Very Unfavorable")
**General Finding:** For the first time in surveys dating to 1992, majorities in both parties express not just unfavorable but *very unfavorable* views of the other party.

**Results:**
- **2008:** 32% of Republicans had "very unfavorable" view of Democratic Party
- **2014:** 46% of Republicans held "very unfavorable" view
- **2016 and later:** 58% of Republicans held "very unfavorable" view of Democratic Party (upward trend continued)

**Response Scale:** Appears to be multi-point favorability scale (at minimum: favorable / unfavorable / very unfavorable)

**Source:** Pew Research Center trend data on party favorability

**Availability:** https://www.pewresearch.org/politics/2016/06/22/1-feelings-about-partisans-and-the-parties/

---

### 3.5 Pew Research: Partisan Immorality ("The Other Party Is More Immoral")
**Finding:** Pew Research asked respondents whether the opposing party members are more immoral than other Americans.

**Results:**
- **2016:** 47% of Republicans; 35% of Democrats
- **2022:** 72% of Republicans; 63% of Democrats (sharp rise in 7 years)

**Source:** Pew Research Center, "Partisan Hostility Grows Amid Signs of Frustration With Two-Party System" (August 2022)

**Question Wording:** UNVERIFIED (exact wording not found in available summaries)

**Availability:** https://www.pewresearch.org/politics/2022/08/09/as-partisan-hostility-grows-signs-of-frustration-with-the-two-party-system/

---

### 3.6 Partisan Identity Scale (Bankert, Huddy, & Rosema 2017)
**Eight-Item Scale Measuring Partisan Social Identity**

The Bankert, Huddy, & Rosema (2017) Partisan Identity Scale consists of eight items, all with the same response scale (typically 1–5 Likert, though exact response anchors UNVERIFIED in available sources):

**Known Items:**
1. "When people praise this party, it makes me feel good." 
2. [Six additional items—exact wording NOT verified]

**Shorter 4-Item Subscale:** Items 3, 6, 7, and 8 (for space-constrained applications)

**Scale Scoring:** Unweighted mean of all items; higher values = stronger partisan identity

**Source:** Bankert, A., Huddy, L., & Rosema, M. (2017). "Measuring Partisanship as a Social Identity in Multi-Party Systems." *Political Behavior*, 39(1), 103–132.

**Original Publication:** https://access.gesis.org/zis/386 (GESIS Zentralarchiv für Empirische Sozialforschung)

**Full Item List:** UNVERIFIED—items 2–8 exact wording not confirmed from primary sources during this scan. Recommend consulting the original paper or GESIS archive.

---

### 3.7 Iyengar et al. Social Distance (Marriage across Party Lines)
**Question Concept:** Respondents are asked how they would feel if their son or daughter married someone from the other political party.

**Response Options:** Appear to include: "Very upset" / "Somewhat upset" / (neutral/okay implied)

**Key Result (2008 YouGov Survey):**
- 27% of Democrats indicated feeling "somewhat upset" or "very upset" at prospect of child marrying a Republican
- 20% of Republicans indicated the same about a Democrat marrying their child

**Source:** Iyengar et al. (2012) study cited in multiple affective polarization reviews

**Primary Citation:** 
- Iyengar, S., Sood, G., & Lelkes, Y. (2012). "Affect, Not Ideology: A Social Identity Perspective on Polarization." *Public Opinion Quarterly*, 76(3), 405–431.
- https://pcl.sites.stanford.edu/sites/g/files/sbiybj22066/files/media/file/iyengar-poq-affect-not-ideology.pdf

**Exact Question Wording:** UNVERIFIED (concept confirmed; full wording not extracted from primary source during this scan)

---

## 4. Non-Political Baseline Items

### 4.1 Social Media and Democracy
**Question:** "Overall, do you think social media has been a good or bad thing for democracy in [country]?"

**Response Scale:** Good / Bad (binary)

**Global Results (Pew 2022–2023, 27 countries surveyed):**
- Median across countries: **64% say social media good for democracy**
- **U.S. outlier:** Only 34% say social media good; 64% say bad for democracy
- Highest positive: Nigeria and Mexico (~77% say good)
- Strongest negative: Netherlands and France (more say bad than good)

**Additional Finding on Misinformation:** 84% median across 19 countries surveyed believe access to internet and social media make people easier to manipulate with false information and rumors.

**Survey Details:**
- **Years:** 2022–2023
- **Sample Frame:** Nationally representative in each country
- **Source:** Pew Research Center, "Social Media Seen as Mostly Good for Democracy Across Many Nations, But U.S. is a Major Outlier" (December 2022 / February 2024 update)

**Availability:** 
- https://www.pewresearch.org/global/2022/12/06/social-media-seen-as-mostly-good-for-democracy-across-many-nations-but-u-s-is-a-major-outlier/
- https://www.pewresearch.org/short-reads/2024/02/23/majorities-in-most-countries-surveyed-say-social-media-is-good-for-democracy/

**Response Scale Detail:** UNVERIFIED (binary inferred from results; exact scale options—e.g., 3-point/5-point/other—not confirmed)

---

### 4.2 Remote Work Productivity
**Question:** "How does working from home affect your ability to get your work done and meet deadlines?"

**Response Options:**
- Helps (56% of respondents)
- Neither helps nor hurts (37%)
- Hurts (7%)

**Additional Related Finding:** 71% of people who work from home said it helped balance work and personal life.

**Survey Details:**
- **Source:** Pew Research Center (2023)
- **Sample:** Working adults in the U.S. with remote-capable jobs
- **Note:** Intensity variation ("helps a lot" vs. "helps a little") not confirmed in published findings

**Availability:** https://www.pewresearch.org/short-reads/2023/03/30/about-a-third-of-us-workers-who-can-work-from-home-do-so-all-the-time/

---

## 5. Mapping to Stimulus Ladder Rungs

### Overview
The bipolar Likert-style ladder structure is: CENTER → MILD (each direction) → MODERATE (each direction) → EXTREME (each direction)

Each rung requires exact question wordings that can serve as anchors and be justified against established instruments rather than invented.

---

### 5.1 Immigration Policy Ladder

| Rung | Valence | Suggested Anchor Item | Source | Scale Point(s) | Coverage Quality | Notes |
|------|---------|----------------------|--------|-----------------|-----------------|-------|
| **CENTER** | Neutral | "Keep border spending the same" | ANES V201306 | "Kept the same" | High | Clear neutral position from 3-point scale |
| **MILD (Restrictive)** | Conservative | "Decreased a little" (immigration levels) | GSS LETIN1A | Point 4 of 5 | High | Exact wording available; 5-point scale; well-established |
| **MODERATE (Restrictive)** | Conservative | "Guest worker program, limited time" | ANES V201417 | Option 2 of 4 | High | Restrictive but permissive of presence; ordered categorical |
| **EXTREME (Restrictive)** | Conservative | "Felonize and deport all unauthorized" | ANES V201417 | Option 1 of 4 | High | Most restrictive policy position available in ANES; anchor for extreme rung |
| **MILD (Permissive)** | Liberal | "Increased a little" (immigration levels) | GSS LETIN1A | Point 2 of 5 | High | Mirror of restrictive mild; exact wording |
| **MODERATE (Permissive)** | Liberal | "Citizenship with requirements" | ANES V201417 | Option 3 of 4 | High | Permissive with conditions; clear middle ground |
| **EXTREME (Permissive)** | Liberal | "Citizenship without penalties" | ANES V201417 | Option 4 of 4 | High | Most permissive policy position; extreme liberal rung anchor |

**Coverage Assessment:**
- **CENTER:** Strong (single neutral point identified)
- **MILD (both directions):** Strong (GSS 5-point scale provides symmetric mild points)
- **MODERATE (both directions):** Strong (ANES 4-point categorical provides clear moderate options)
- **EXTREME (both directions):** Strong (ANES provides most restrictive and most permissive endpoints)

**Overall Immigration Ladder:** Full coverage with direct instrument anchors at all rungs. No gaps.

---

### 5.2 Partisan Identity / Us-vs-Them Ladder

**Challenge:** No single established instrument provides a symmetric bipolar party-identity scale with clear CENTER, MILD, MODERATE, and EXTREME rungs in both ideological directions.

**Mapping Strategy:** Layer multiple instruments to approximate ladder rungs, with explicit flagging of gaps where instruments fall short.

| Rung | Valence | Suggested Anchor Concept | Source | Scale/Wording | Coverage Quality | Notes |
|------|---------|------------------------|--------|----------------|-----------------|-------|
| **CENTER** | Neutral | Feeling Thermometer 50 | ANES FT | 50 (explicit neutral) | **STRONG** | The 0–100 scale explicitly codes 50 as neutral; high validity |
| **MILD (Anti-GOP/Pro-Dem)** | Liberal | "Frustrated with Republican Party" | Pew 2016 | Binary (frustrated: yes/no) | Medium | 58% of Dems reported; emotion-based rather than belief-based; no scalar intensity variation |
| **MODERATE (Anti-GOP/Pro-Dem)** | Liberal | "Republican policies bad for country" | Pew (general trend) | Binary (yes/no) | Medium | 62% of Dems cite this reason; specific question wording NOT verified from codebook |
| **EXTREME (Anti-GOP/Pro-Dem)** | Liberal | "GOP policies threaten nation's well-being" | Pew 2016 | Binary (yes/no) | **STRONG** | Exact wording verified; 41% of Dems in 2016; high-threat endpoint anchor |
| **MILD (Anti-Dem/Pro-GOP)** | Conservative | "Frustrated with Democratic Party" | Pew 2016 | Binary (frustrated: yes/no) | Medium | 57% of Reps reported; symmetric to liberal mild |
| **MODERATE (Anti-Dem/Pro-GOP)** | Conservative | "Democratic policies bad for country" | Pew (general trend) | Binary (yes/no) | Medium | 78% of Reps cite; UNVERIFIED exact wording from codebook |
| **EXTREME (Anti-Dem/Pro-GOP)** | Conservative | "Democratic policies threaten nation's well-being" | Pew 2016 | Binary (yes/no) | **STRONG** | Exact wording verified; 45% of Reps in 2016; high-threat endpoint anchor |

**Coverage Assessment – Critical Gaps Identified:**

1. **CENTER:** ✓ Strong – Feeling Thermometer 50 is explicit neutral.

2. **MILD Rungs:** ⚠️ **WEAK** – Pew's emotion items (fear, frustration, anger) are binary and emotion-based, not belief-based. No intensity variation within "frustrated" category. Could substitute with *any* partisan dislike (e.g., unfavorable view), but "frustrated" lacks nuance for a "mild" rung. Consider using Pew favorability data (unfavorable vs. very unfavorable) as intensity proxy, though exact question wording not verified.

3. **MODERATE Rungs:** ⚠️ **UNVERIFIED** – The statement "policies are bad for the country" appears in Pew trend narratives (62% of Dems, 78% of Reps) but **exact question wording NOT found** in primary sources during this scan. This is a critical gap: recommend verifying against Pew's 2022–2024 polling toplines (referenced in reports but not extracted here).

4. **EXTREME Rungs:** ✓ Strong – Pew's "threaten nation's well-being" question has exact wording verified and is the direct anchor you identified.

5. **Missing Alternative Items:**
   - **"Other party would be bad if in power" / "Would be better off if other party never won":** Not found in ANES or Pew codebooks during this scan. Likely exists in some form but would require deeper documentation search.
   - **Kalmoe & Mason partisan threat items:** Referenced in literature but exact question wordings NOT extracted (PDFs were binary-encoded).
   - **Bankert/Huddy/Rosema Partisan Identity Scale:** Only one of eight items verified; full scale wording needed.
   - **Iyengar social distance (marriage):** Concept confirmed; exact wording not verified.

**Recommendation for MODERATE Rungs:**
To fill the moderate-rung gap with verified anchors, either:
- Fetch the full Pew 2022 or 2024 topline/questionnaire to extract exact "policies bad for the country" wording.
- Use Pew's favorability categories (unfavorable vs. very unfavorable) as intensity proxy within negative affect.
- Develop moderate statements de novo and justify against the literature rather than existing instruments.

---

## 6. Source List

### Primary Data Repositories

1. **American National Election Studies (ANES)**
   - Main Website: https://electionstudies.org
   - Question Search Tool: https://electionstudies.org/data-tools/anes-question-search/
   - 2020 Time Series Questionnaire: https://electionstudies.org/wp-content/uploads/2021/07/anes_timeseries_2020_questionnaire_20210719.pdf
   - 2020 Time Series Methodology Report: https://electionstudies.org/wp-content/uploads/2022/08/anes_timeseries_2020_methodology_report.pdf
   - ICPSR Archive: https://www.icpsr.umich.edu/web/ICPSR/series/3

2. **General Social Survey (GSS)**
   - Main Website: https://gss.norc.org
   - Data Explorer: https://gssdataexplorer.norc.org
   - 2022 Codebook: https://gss.norc.org/content/dam/gss/get-documentation/pdf/codebook/GSS%202022%20Codebook.pdf
   - 2024 Codebook (Release 3): https://gss.norc.org/content/dam/gss/get-documentation/pdf/codebook/GSS%202024%20Codebook%20R3.pdf
   - Quick Guides to Variables: https://gss.norc.org/get-documentation.html
   - LETIN1A Variable Explorer: https://gssdataexplorer.norc.org/variables/1611/vshow

3. **Pew Research Center**
   - Politics & Elections: https://www.pewresearch.org/politics/
   - Partisanship and Political Animosity (2016): https://www.pewresearch.org/politics/2016/06/22/partisanship-and-political-animosity-in-2016/
   - Section: How Do Political Parties Make You Feel? https://www.pewresearch.org/politics/2016/06/22/6-how-do-the-political-parties-make-you-feel/
   - Political Polarization (2014): https://www.pewresearch.org/politics/2014/06/12/section-2-growing-partisan-antipathy/
   - Partisan Hostility (2022): https://www.pewresearch.org/politics/2022/08/09/as-partisan-hostility-grows-signs-of-frustration-with-the-two-party-system/
   - Social Media and Democracy (2024): https://www.pewresearch.org/short-reads/2024/02/23/majorities-in-most-countries-surveyed-say-social-media-is-good-for-democracy/
   - Remote Work (2023): https://www.pewresearch.org/short-reads/2023/03/30/about-a-third-of-us-workers-who-can-work-from-home-do-so-all-the-time/

### Scholarly Sources on Affective Polarization & Partisan Identity

4. **Iyengar et al. on Social Distance and Affective Polarization**
   - Iyengar, S., Sood, G., & Lelkes, Y. (2012). "Affect, Not Ideology: A Social Identity Perspective on Polarization." *Public Opinion Quarterly*, 76(3), 405–431.
   - PDF: https://pcl.sites.stanford.edu/sites/g/files/sbiybj22066/files/media/file/iyengar-poq-affect-not-ideology.pdf
   - Origins and Consequences: https://pcl.sites.stanford.edu/sites/g/files/sbiybj22066/files/media/file/iyengar-ar-origins.pdf

5. **Bankert, Huddy, & Rosema on Partisan Identity Scale**
   - Bankert, A., Huddy, L., & Rosema, M. (2017). "Measuring Partisanship as a Social Identity in Multi-Party Systems." *Political Behavior*, 39(1), 103–132.
   - GESIS Archive Entry: https://access.gesis.org/zis/386

6. **Kalmoe & Mason on Radical Partisanship**
   - Kalmoe, N. P., & Mason, L. (2022). *Radical American Partisanship: Mapping Violent Hostility, Its Causes, and the Consequences for Democracy*. University of Chicago Press.
   - Lethal Mass Partisanship (2019 working paper): https://www.dannyhayes.org/uploads/6/9/8/5/69858539/kalmoe___mason_ncapsa_2019_-_lethal_partisanship_-_final_lmedit.pdf

7. **Other Affective Polarization Resources**
   - Druckman, J. N., & Levendusky, M. S. "Affective Polarization, Local Contexts, and Public Opinion in America." *Journal of Politics*, forthcoming.
   - PDF: https://faculty.wcas.northwestern.edu/jnd260/pub/Druckman%20and%20Levendusky%20Affective%20Polarization%20Measurement.pdf

---

## 7. Summary of Verification Status

| Category | Items Found | Exact Wording Verified | Coverage Quality |
|----------|-------------|----------------------|-----------------|
| **ANES Immigration** | 3 main items | ✓ Yes (border wall, unauthorized policy options, border spending) | High for policy specifics; lacks 7-point bipolar scale |
| **GSS Immigration** | 1 primary item (LETIN1A) | ✓ Yes | High; 5-point symmetric scale ideal for center ± rungs |
| **Pew Party Threat** | 1 main threat item + emotion/favorability items | ✓ Yes (threat item); ⚠️ Partial (emotions/favorability) | Strong for extremes; weak for moderate rungs |
| **ANES Feeling Thermometer** | 1 scale (0–100) | ✓ Yes (concept); ⚠️ Partial (exact question wording) | High for center; useful for mapping overall affect gradient |
| **Partisan Identity Scales** | 2 identified (Bankert/Huddy, Iyengar social distance) | ⚠️ Partial or UNVERIFIED | Medium; full item wording needs confirmation |
| **Baseline Items (Social Media, Remote Work)** | 2 items | ⚠️ Partial (response scale not fully verified) | Medium |

---

## 8. Recommendations for Next Steps

### High-Priority Gaps
1. **Moderate Rung for Party-Identity Ladder:** Verify the exact wording of the "policies bad for the country" item from Pew 2022–2024 surveys. This is currently marked UNVERIFIED but widely cited.
2. **Bankert/Huddy Partisan Identity Scale:** Obtain the full eight-item scale wording. Only one item was confirmed.
3. **Iyengar Social Distance Item:** Extract exact question wording and response scale from the original paper.
4. **ANES Party-Identity Items:** Check whether ANES has any items asking about "better off if other party never won" or similar existential threat language beyond the policy-threat questions currently coded.

### Secondary Priority
5. **Kalmoe & Mason Partisan Threat Items:** The PDFs encountered during search were binary-encoded. Recommend obtaining a readable version of the full paper to extract exact item wordings.
6. **Pew Emotion Items Exact Wording:** Fetch the full Pew 2016 and 2022–2024 toplines to confirm response scales for fear/anger/frustration items (currently inferred as binary from results).

### Design Decisions
- The **immigration ladder has full coverage** with strong instrument anchors at all rungs; no gaps.
- The **party-identity ladder has strong anchors only at CENTER and EXTREME rungs**; MILD and MODERATE rungs lack verified instruments and should either be filled via deeper documentation search (see above) or justified explicitly as informed-by-literature rather than instrument-anchored in the final writeup.
- **Baseline items (social media, remote work)** provide proof-of-concept but would benefit from verification of exact response scales before use in stimulus design.

