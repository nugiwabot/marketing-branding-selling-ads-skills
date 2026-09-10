# Positioning, Claims & Message Governance

This rule governs `claim-check`, `positioning-map`, and `message-consistency-check`.

## Strategic Boundary

These skills are downstream evidence/QA specialists. They must not silently make strategic decisions that belong to `strategic-intelligence`.

For broad, ambiguous, cross-functional, or decision-oriented requests:

`Strategic Intelligence → Research/Evidence → Positioning/Claims/Message QA → Recommendation/Execution`

If new evidence changes the underlying diagnosis, audience, value proposition, positioning direction, or channel/business decision, return the finding to `strategic-intelligence` rather than resolving the strategic conflict locally.

## Claim Discipline

- A claim is not evidence merely because it appears in company messaging.
- `supported` requires identifiable evidence and a traceable source.
- Customer language, competitor messaging, internal opinion, and AI inference are different evidence classes.
- A testimonial or quote must remain attributable to its real source; never synthesize a quote and present it as customer language.
- Comparative, superiority, performance, financial, medical, legal, regulatory, or quantified claims require evidence appropriate to the claim.
- If evidence is absent, use `unsupported` or `unverified`; do not soften the verdict to make the message pass.
- A softer wording is not automatically safe if it still implies an unsupported fact.

## Positioning Map Discipline

- Public competitor messaging proves what the competitor claims or publishes, not that the claim is true or effective.
- Competitor presence, posting frequency, channel use, pricing, or launch activity does not prove causal effectiveness.
- A 2x2 map is an analytical visualization, not objective market truth. Axis selection must be justified by customer relevance, decision criteria, evidence, or an explicit hypothesis.
- An apparently unclaimed position is not automatically whitespace. Test whether it matters to customers and whether the business can credibly deliver and prove it.
- Distinguish `observed`, `inferred`, `hypothesized`, and `validated` positioning conclusions.

## Message Consistency Discipline

- Consistency means alignment to an approved strategic/message source of truth, not making every surface identical.
- If no approved source exists, report the absence of a source of truth rather than treating the homepage as objectively correct.
- A divergence can be intentional by funnel stage; do not flag it as a defect without considering audience, journey stage, and role of the surface.
- Preserve meaningful differences between awareness, consideration, conversion, onboarding, and retention messaging when strategically justified.
- Severity must reflect strategic/business risk and evidence, not merely wording differences.

## Handoff to Strategy

When these skills discover evidence that materially changes a strategic assumption, return:

1. What was observed.
2. Source/evidence.
3. What previous assumption it challenges.
4. Confidence.
5. Strategic decision that may need reconsideration.

Do not silently rewrite the strategic diagnosis.

## Quality Gate

Before finalizing:
- Claims are traceable to evidence where required.
- Competitor behavior is not presented as proof of effectiveness.
- Positioning maps do not imply objective truth from arbitrary axes.
- Message differences are interpreted in context of audience/journey.
- Facts, observations, inferences, hypotheses, benchmarks, and recommendations remain distinguishable.
- Strategic conflicts are escalated to `strategic-intelligence`.
