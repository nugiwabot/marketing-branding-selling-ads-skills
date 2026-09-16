---
name: visual-asset-discovery
description: Translates marketing strategy and content intent into reusable visual-search strategies for discovering relevant footage or visual assets, then iterates from retrieved assets toward the strongest final narrative expression.
metadata:
  version: 1.0.0
---

# Visual Asset Discovery

## Purpose

Use this skill when a marketing, branding, content, campaign, or storytelling task needs visual assets to be discovered from external clip, stock, archive, image, or video libraries before the final story, headline, or edit is locked.

The skill teaches a reusable search method. It does not depend on a fixed keyword bank, a specific media database, a specific film catalog, or previously successful searches.

## Core Principle

Translate strategy into observable visual situations rather than translating marketing language literally into search text.

The operating loop is:

`Strategic intent → human meaning → observable situation → search dimensions → query families → retrieval → scene interpretation → strategic alignment → refine or accept → final expression`

Retrieved assets are real-world constraints. Do not force a prewritten headline, script, or story onto footage that does not naturally support it.

## Inputs

Use the strongest available inputs from the task and connected context:

- marketing objective
- audience or human situation
- positioning and message
- content role or funnel stage
- emotional or experiential territory
- brand boundaries
- product facts when the asset must remain product-relevant
- target asset type and media source constraints
- retrieved asset metadata, transcripts, subtitles, or scene descriptions when available

If the strategic context is incomplete, preserve the known intent and avoid inventing product-specific facts.

## Procedure

### 1. Extract strategic intent

Reduce the source strategy to a compact intent model:

- **Objective:** what communication outcome is needed.
- **Audience state:** what the intended audience is thinking, feeling, doing, or deciding.
- **Message:** the central meaning the content should communicate.
- **Emotional territory:** the feeling or human significance the asset may carry.
- **Brand territory:** the meanings and associations the asset may safely reinforce.
- **Constraints:** product truth, tone, platform, duration, rights, and other explicit limits.

Do not begin by writing a final headline.

### 2. Convert abstract meaning into observable situations

Ask:

> What could a camera actually show that would make this meaning understandable?

Convert abstract concepts into visible human situations, interactions, actions, environments, transitions, or expressions.

Prefer situations over labels. A situation contains something that can be observed: who is present, what they are doing, how they relate, where it happens, and what is changing.

Do not require the visual to literally depict the product or repeat the wording of the strategy.

### 3. Decompose the situation into search dimensions

Construct the minimum useful combination of dimensions:

- **Subject:** who or what is visible.
- **Action:** what is happening.
- **Relationship:** who is interacting with whom or what.
- **Setting:** where the action occurs.
- **Emotion / behavior:** visible affect, posture, or behavioral cue.
- **Context:** circumstance, life stage, time, or narrative condition when it materially improves retrieval.
- **Visual form:** shot type, composition, movement, or other asset characteristics when supported by the source.

Not every query needs every dimension.

### 4. Build query families

Generate multiple search formulations for the same strategic intent instead of relying on one sentence.

Use a progression:

1. broad semantic formulation
2. concrete scene formulation
3. action or interaction formulation
4. contextual refinement

Diversify by changing the representation of the same intent, not by generating random synonyms.

Query language should match the retrieval system. For subtitle/quote databases, favor language likely to occur in dialogue or transcripts. For scene-description search, favor concrete observable events. For stock or visual search, favor concise visual descriptors.

### 5. Search iteratively

Treat retrieval as a feedback loop, not a one-shot request.

For each search round:

1. inspect the returned results;
2. identify what the results actually depict or say;
3. compare them with the intended strategic meaning;
4. keep, broaden, narrow, or reframe the query family;
5. repeat until useful candidates appear or the source has been reasonably exhausted.

When the source offers transcript, quote, scene-description, metadata, or filters, use the dimension that best matches the type of situation being sought.

### 6. Interpret the retrieved asset before writing the story

For each candidate, establish:

- what literally happens;
- what human meaning the scene plausibly communicates;
- what emotional tone it carries;
- what parts of the original strategic intent it can support;
- what parts it cannot support;
- whether the asset introduces an unintended meaning or brand risk.

Do not infer a meaning that contradicts obvious context merely because the frame looks visually convenient.

### 7. Score strategic alignment

Use a qualitative alignment check across:

- **Strategic fit:** supports the intended communication objective.
- **Visual fit:** clearly depicts the desired situation.
- **Emotional fit:** carries the intended human tone.
- **Narrative utility:** can support a beginning, middle, end, or single-message structure.
- **Brand fit:** does not create a materially conflicting association.
- **Practical fit:** suitable duration, aspect ratio, source constraints, and production use.

Reject candidates that look attractive but materially distort the intended message.

### 8. Let the asset constrain the final expression

Once a useful asset is selected, create the final headline, story, caption, or edit direction from the intersection of:

`Original strategic intent ∩ Actual asset meaning ∩ Brand boundaries`

Preserve the strategic intent, but adapt the wording to what the footage can truthfully and naturally communicate.

If no candidate provides adequate support, return to the search stage rather than fabricating a stronger story than the footage can carry.

## Output Contract

When asked to produce a visual discovery plan, return:

1. **Strategic intent** — the normalized communication target.
2. **Visual situation model** — the observable situations that could express it.
3. **Search dimensions** — the dimensions selected for retrieval.
4. **Query families** — multiple search formulations organized by retrieval level.
5. **Iteration guidance** — how to broaden, narrow, or reframe after results appear.
6. **Candidate evaluation** — how retrieved assets should be judged against the strategy.
7. **Post-retrieval expression rule** — how the final story/headline should be derived from the actual selected asset.

Do not output a static keyword dictionary unless the user explicitly requests one. Prefer generative rules that work for new products, new campaigns, new themes, and new media sources.

## Guardrails

- Do not invent scenes, dialogue, metadata, or asset availability.
- Do not assume a search engine understands marketing language the same way a strategist does.
- Do not force exact semantic matches when the underlying visual meaning can be expressed indirectly.
- Do not let a visually attractive asset override strategic relevance.
- Do not create a final message that asserts meaning unsupported by the actual retrieved asset.
- Keep product claims grounded in verified product knowledge; this skill is a visual-discovery procedure, not a source of product facts.
- Do not hard-code a vendor-specific workflow unless the task explicitly requires it.
- For copyrighted media, distinguish discovery from rights to use the asset commercially; availability in a search system does not establish usage rights.

## Completion Test

A run is complete when one of these conditions is true:

**Success:** at least one candidate asset supports the required strategic meaning with acceptable visual, emotional, narrative, brand, and practical fit.

**Controlled stop:** the available source has been reasonably searched and no suitable asset has been found; the system should state the gap and either recommend changing the visual interpretation or using another asset source.

The skill should optimize for a useful, truthful bridge between strategy and available visuals — not for finding a perfect literal match.