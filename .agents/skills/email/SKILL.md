---
name: email
description: Generates email sequences for different contexts. Currently supports event follow-up sequences. Produces ready-to-send emails with subject lines, body copy, and timing guidance.
autoload: false
---

# Email Generator

This skill generates email sequences tailored to specific contexts. Each email type has its own rules derived from sequences that performed well in production.

## Strategic Position in the System

Email is an execution/channel layer, not an independent strategy engine.

For broad, ambiguous, cross-functional, or decision-oriented requests, consume the `strategic-intelligence` diagnosis before selecting email as an intervention. Preserve the established objective, audience, journey stage, diagnosed bottleneck/opportunity, offer/message direction, channel role, constraints, and measurement logic.

Do not assume email is appropriate merely because a contact list exists, or that a fixed sequence is appropriate for every audience. If the diagnosis points to offer, positioning, product, sales, channel, or retention issues, surface that rather than forcing an email sequence.

For narrow execution requests with established direction, proceed with the supplied context.

## Evidence Discipline

Use these evidence classes:
- **FACT** — directly supported by source material
- **OBSERVATION** — observed pattern
- **INFERENCE** — reasoned interpretation
- **HYPOTHESIS** — unvalidated idea
- **BENCHMARK** — external reference with source/context
- **RECOMMENDATION** — execution choice

Never fabricate customer names, testimonials, quotes, conversation details, outcomes, response rates, open rates, conversion rates, or other performance data.

Timing, sequence length, CTA type, and copy patterns are defaults or hypotheses unless supported by the actual campaign strategy or evidence.

## Step 1: Select Email Type

Before generating, identify the requested context. Current supported workflow:

- Event follow-up (post-conference, post-meeting, post-demo)
- Customer (retention, upsell, product updates) — *coming soon*
- Prospect (cold outreach, nurture) — *coming soon*

If a requested type is not implemented, state that clearly rather than pretending it is supported.

Do not ask the user to re-specify information already available in a strategic handoff.

## Step 2: Gather Inputs (Event Follow-Up)

Read available project context before asking questions:

| What you need | Where to find it |
|---------------|------------------|
| Product name | `docs/inputs/product_brief.md` |
| Product capabilities | `docs/inputs/product_brief.md` |
| Pain points | `docs/inputs/messaging_positioning.md` |
| Social proof / customers | `docs/inputs/testimonials.md` |
| Target persona context | `docs/inputs/target_personas.md` |
| Asset links | `docs/inputs/product_brief.md` |

Then ask only for what the repository or handoff cannot establish:

1. **Event name** — What event/conference did you meet them at?
2. **Specific conversation context** — Optional context that genuinely differs from the established pain points.

Never invent sender identity, company identity, recipient details, or conversation history.

## Step 3: Generate Sequence (Event Follow-Up)

Use the following four-email structure as a practical template, not a universal law. Adapt the number, timing, thread structure, and CTA to the actual audience, journey, and campaign objective.

### Email 1: The Recall

**Timing:** A reasonable starting hypothesis is shortly after the event. Use the campaign's established cadence when available.

**Job:** Remind them of the shared context and surface relevant pain without presuming their individual situation.

Rules:
- Reference only genuine shared context.
- Frame pain points as patterns heard from the group when that is true.
- Never fabricate what the recipient specifically said, asked, or mentioned.
- End with an open question when appropriate.

### Email 2: The Peer Voice

**Timing:** Use the established campaign cadence; do not assume a fixed delay is universally optimal.

**Job:** Add credible peer evidence and introduce the product when relevant.

Rules:
- Use only approved customer/company references.
- Never invent quotes or paraphrases.
- Do not name drop merely for persuasion if the names are not relevant or approved.
- CTA should match the journey stage and strategic objective.

### Email 3: The Proof

**Timing:** Follow the established cadence or test hypothesis.

**Job:** Lead with credible customer evidence or a useful resource when available.

Rules:
- Customer outcomes must be real and approved.
- If proof is unavailable, state the evidence gap rather than manufacture one.
- Offer a resource only if it genuinely exists and is relevant.

### Email 4: The Soft Close

**Timing:** Use the campaign cadence rather than treating a fixed delay as a universal rule.

**Job:** Close the sequence respectfully while preserving a relevant next step.

Rules:
- No pressure tactics.
- Problems listed must be grounded in the actual offer and audience.
- CTA should remain appropriate to the journey.

## Formatting Rules (All Emails)

Maintain concise, readable email copy. The following are practical defaults, not laws:
- Greeting should fit the relationship and brand voice.
- Sign-off should fit the sender identity.
- Keep each email focused on one job and one primary CTA where possible.
- Use bullets when they improve scanability.
- Avoid unsupported urgency or artificial personalization.
- Avoid marketing buzzwords.

## Programmatic Personalization

Personalization must be real, not fabricated.

**Do:**
- Reference genuine shared context.
- Use established audience pain points as patterns, not assumed personal facts.
- Ask open questions when the recipient's situation is unknown.

**Don't:**
- Fabricate 1:1 conversation details.
- Presume the recipient's situation.
- Invent quotes or moments.
- Fabricate customer names, references, testimonials, or results.

## Link Requirements

Links must be real, relevant, and approved. Never invent URLs or use placeholder links in final ready-to-send copy.

Where to get links:
1. Check project documentation for approved asset URLs.
2. If no appropriate link exists, ask for one when a link is required by the strategy.

Do not hardcode a domain or resource path as a universal default. Use the actual project context.

## Quality Check

Before delivery verify:
- [ ] Strategic objective and audience are established or inherited
- [ ] Email is appropriate to the diagnosed journey/bottleneck
- [ ] Claims, customer evidence, and quotes are supported
- [ ] No fabricated personalization
- [ ] CTA matches the intended next action
- [ ] Timing and sequence structure are treated as context-dependent
- [ ] Links are real and relevant
- [ ] No unsupported performance promises
