---
name: ads
description: Generates paid ad copy for Google, Meta, and LinkedIn using strategy-aligned creative variants.
autoload: false
---

# Paid Ads Generator

This skill is an **execution specialist** for paid-ad creative. It converts an existing marketing direction into platform-appropriate ad assets.

## Strategic Boundary

For broad, ambiguous, cross-functional, or decision-oriented requests, consume `strategic-intelligence` first.

The strategic layer determines, when relevant:
- business objective and decision required
- audience and journey context
- offer and positioning
- bottleneck or opportunity
- whether paid media is appropriate
- channel/media role
- funnel role
- measurement and business outcome
- constraints and evidence confidence

Do not independently decide that Google, Meta, LinkedIn, or any other platform is the right strategic channel. Do not treat ad copy as the automatic solution to a conversion problem.

If no strategic diagnosis exists because the request is narrow execution, preserve the user's stated objective and context rather than inventing strategy.

## Evidence Discipline

Use these evidence labels when material claims are involved:
- **FACT** — supplied or verified evidence.
- **OBSERVATION** — directly visible from supplied material.
- **INFERENCE** — interpretation of evidence.
- **HYPOTHESIS** — proposition requiring testing.
- **BENCHMARK** — external comparison with source/context.
- **RECOMMENDATION** — proposed creative decision.

Never invent testimonials, customer results, competitor weaknesses, product capabilities, statistics, performance claims, or business outcomes.

## Creative Selection

Do not mechanically generate every Topics × Personas × Angles combination.

Select creative directions from the strategic context, available evidence, audience language, offer, funnel role, and platform constraints.

Possible creative angles include:
- Problem/context
- Outcome or benefit
- Education/how-to
- Proof/social proof when verified
- Comparison when competitor evidence is verified
- Product mechanism
- Objection/trust response
- Other contextually justified angles

These are creative hypotheses, not universal performance formulas. Do not claim an angle will convert better without evidence.

## Platform Specifications

Respect the platform's **current documented limits and requirements** when generating assets. Verify current official platform documentation when a specification is uncertain or materially important.

Character recommendations, truncation behavior, image dimensions, text-overlay rules, targeting assumptions, and delivery behavior can change. Do not present historical guidance as a performance law.

Platform context:
- Google Search: align language with verified search intent and keyword context supplied by the strategy.
- Meta: optimize the creative for the actual audience, placement, journey role, and offer rather than assuming generic feed behavior.
- LinkedIn: do not assume VPs, CTOs, executives, or budget holders are the audience unless strategy/evidence establishes it.

## Claim and Proof Rules

- Use social proof only when the proof is real and approved/verified.
- Competitor comparisons require evidence; competitor presence or activity does not prove competitor weakness or effectiveness.
- Numeric claims require evidence.
- If proof is unavailable, write without proof rather than inventing it.
- Do not convert a benchmark into a product claim.

## CTA Rules

CTA should match the funnel stage and desired next action. Do not default to "Book a Demo", "Start", "Try", or another CTA without strategic justification.

## Output

For each selected variant provide:

### Strategic Context
- Objective
- Audience
- Funnel role
- Channel role
- Key bottleneck/opportunity
- Evidence/confidence

### Creative Variant
- Angle
- Core message
- Headline(s)
- Primary text / description as applicable
- CTA
- Creative brief
- Platform constraints checked
- Claims/proof used and their evidence status

### Test Priority
Prioritize variants using evidence, strategic relevance, differentiation, feasibility, and learning value. Do not promise performance.

## Quality Gate

Before delivery:
- [ ] Strategic direction is preserved when supplied.
- [ ] Paid media is not treated as an automatic solution.
- [ ] Audience is not assumed from platform stereotypes.
- [ ] Claims match verified product/context information.
- [ ] No fabricated social proof, metrics, or competitor claims.
- [ ] Current platform requirements are verified when necessary.
- [ ] Creative angles are hypotheses, not guaranteed performance formulas.
- [ ] CTA matches the intended journey stage.
- [ ] No unsupported performance prediction is presented as fact.
