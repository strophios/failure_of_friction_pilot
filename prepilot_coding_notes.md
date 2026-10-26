# Notes with `prepilot_coding_sheet_01.csv` - 2026-10-07

These are miscellaneous notes and thoughts recorded while coding the 10 responses for the pre-pilot: 

- Dimension D: 
    - Under D, "Balanced/no position" seems, as stated, to be different in kind from "qualified (dis)agreement"; as written, it's not "I partly agree and partly disagree" or "I agree with a version of your argument, but I think it's overreaching as stated". It could be that we mean it to cover both and for the other dimensions to capture the difference, but the one sentence statement in the schema is not totally clear there. 
- Dimension C:
    - Make sure we are (and stay) clear on the differentiation between "considerations" and follow up questions/clarifications
    - What do we count as a "neutral" consideration, for C?
- Dimension M: 
    - On M-own and M-form, we need to decide what to do when multiple are present; e.g., response aea82dd711 has both "hedged" ("I get the appeal...But I don't think it holds up well") and "interrogative" ("A few questions that might sharpen your view")
        - see also response 7ae09bb34a
        - f4ee562338 is interesting here (and with respect to some other dimensions as well): a lot of the pushback is kind of assigned or impersonal (e.g., "Plenty of people across the political spectrum organize their lives around those same commitments") but there is an owned aspect in that the point isn't "you're saying x, but the evidence/a lot of people say y", it's "actually the world is like this". 
    - And what do we do in cases, as with 23a429e04a, where the model is making a strong counter argument, but never with direct self-identified "I disagree", but also without a clear "most people think", etc.? Like, I lean towards maybe calling it "owned", but maybe it should be something else?
    - Similarly, a21a6237a0 is interesting in that it the model takes a clear first person position "I don't have a settled view on this", it's just that that position is "I don't know". 
    - 66de89f3f0 is another interesting case where it's not clear what we'd call it on either part of the dimension; like, my leaning is "impersonal"/"assertive", but there's a decent argument that all of the pushback is in the form of "but you should also consider..." that's arguably kind of "interrogative" in character (though maybe we want to make dimension M more specifically grammatical in nature?)
- Dimension F:
    - F-lex and F-struct fundamentally don't work with the blind coding, since they rely on the coder knowing what the user's framing was. Now, they could potentially be tweaked so that instead of measuring framing pickup directly, they're like counting emotively/ideologically charged word use (F-lex) and maybe like trying to guess the user's framing based on the answer working under the assumption that the framings match (F-struct) or something. 
        - even separately from the blinding issue, I think we'll need to clarify what counts as emotively/ideologically charged word use for F-lex and we need to think through what to do with cases where the user doesn't use any charged words. In fact, more generally, we should identify what we're counting as "charged" words in each prompt ahead of time (and think about whether all prompts should have them, or whether there are other aspects of vocabulary pickup we want to be monitoring, and we want to make sure that we have a good sense of the space of alternatives for all of them; like vocab pickup matters more when there are clear synonyms available as alternatives). Likewise, we want to be really clear about what we mean by framing: is the provided context the frame? are components of that context? if so, which ones? etc.
        - the blinding is also kind of an issue for dimension C: it's not always self-evident in the model's response what the relationship between various "considerations" and the prompt are
        - heck, it can be an issue for dimension D: with, e.g., response fa2be0f6ee, it's not actually that clear from the response what the user's position was, and the model responds in a way that is clearly at least partial disagreement, but the degree of disagreement is difficult to infer given that we don't know that specific position its responding to. 
- Dimension E: 
    - We'll want to clarify the exact boundary between E-followup and E-clarify (i.e., on response ff3968359f, is "what's the specific stuff that has you concerned" clarification or followup?). 
        - aea82dd711: does "I get the appeal of a bright line rule" count as "validation"?
    - fa2be0f6ee is an example of a patter we see a few times, I think, which isn't so much "bothsides" as in "surveys both sides without committing", but rather "surveys both sides/the complicating factors while *committing to the complexity*"; i.e., it's not the model going "well, one side thinks x and the other y, whose to say" but instead "well, there are some good things about it and some bad things about it, so we can definitely say that 'it's all bad/good' is oversimplifying". 
        - note that this isn't just relevant to dimension E; it's more broadly relevant to thinking about how we conceptualize agreement/disagreement etc. 
- Dimension R:
    - We need to clarify what R-refusal means. I'm treating it as requiring basically complete refusal; i.e., not "I don't want to give an opinion, but have you thought about xyz?" but "I'm sorry, but I can't talk about that". This would also mean that, e.g., "That's a harmful idea and I refuse to talk about it further" (or something) would code as a strong disagreement rather than a refusal. Do we think that's the right call?
        - by the same token, is something like response 7c512449c3 a "refusal" insofar as the model engages, but purely in a "hm, what *would* make this true or false" way? I don't think that's what we mean here, but it is an interesting kind of engagement that we may or may not feel is fully captured by, e.g., D-3, M-impersonal/interrogative, etc.
    - Also need to clarify/give examples of what exactly we mean by "safety-flavored caveats". 
- General: 
    - I'm not sure our coding scheme does a great job of capturing wholely equivocal or interrogative responses, or at least not in the detail it does responses with more direct agreement/disagreement. In particular, I'm not sure M-own makes a ton of sense in this context, at least as currently defined (i.e., what do we do with "I want to explore what makes you feel this way")
    - We should make sure we understand clearly the relationship between the dimensions (or lack of one); for instance, maybe M-own "owned" can include cases where there's no direct "I" statement partly because that's what E-position is for
        - On a related note: especially without that, it's not totally clear what all the E flags are for. 
    - I wonder whether a version of this where we allow more thinking, longer responses, and (especially) web search would be better? I'm thinking especially in the context responses like a21a6237a0, where the model says "I have no idea, I know there's evidence on both sides out there" but obviously, given our set up, can't go out and look. And this matters because it may well be that *the looking* is particularly shaped by the framing (or lack thereof). So instead of web search and evidence gathering making the model more equivocal, or more consistent in position overall (which it could also do, to be clear), it could actually make it more likely to be captured by the user's framing. 
    - What was the prompt (the context/view combination) for fa2be0f6ee? Cause it had the model trying to work around a potential contradiction in the user's views (which might be good and what we expect, I just want to check). 
    - Another interesting pattern we see, that the dimensions don't capture, but might be worth attending to: the model commenting (either directly or indirectly) on the user's thinking or epistemic position; e.g., in fa2be0f6ee the user's views "don't obviously belong together" and are an "interesting tension"; in 712e502b9a the user is making "a statement of identity and grievance than something I can evaluate as true or false"; etc.
    - Need to double check what our prompts currently asking; are they specifically "do you agree"? or a broader "what do you think"? should they be something even broader, or maybe something more specified (i.e., not necessarily "do you agree or disagree?" but "can you help me think through this" or "how would you develop these ideas" etc.)


Responding to the model as we develop the schema: 

- should we even be distinguishing between the claim and the context?

- alternative version of this experiment where we source claim + context together from real text, e.g., debate transcripts, political twitter posts, etc.
    - hmmm, but we'd ideally want real text that we're pretty sure isn't in the training corpus, I think. though maybe for something like this it doesn't matter as much. 

