---
name: social-posts
description: Generates social media posts from source content. Produces brand or personal posts for LinkedIn or Twitter, tailored to each channel's audience and format.
autoload: false
---

# Social Media Post Generator

This skill transforms validated source content and strategic context into platform-specific social media posts.

## Strategic Position in the System

Social posts are an execution layer. For broad, ambiguous, cross-functional, or decision-oriented requests, consume the `strategic-intelligence` diagnosis before deciding whether social content is appropriate and what role it should play.

When a strategic handoff exists, preserve its:
- objective and decision
- audience and journey stage
- diagnosed bottleneck/opportunity
- positioning/message direction
- channel role
- constraints
- measurement logic

Do not assume social media, engagement, or a specific platform is the correct strategic answer. For narrow execution requests with established direction, proceed with the supplied source and context.

## Step 1: Channel and Account Selection

Ask only for information that is genuinely missing.

**Platform:** LinkedIn, Twitter/X, or another supported surface.

**Account type:** Brand, Personal, or Both.

Do not ask for a decision that already exists in the strategic handoff or campaign brief.

## Step 2: Gather Inputs

Use the supplied source content or validated handoff. Obtain only missing execution inputs, such as:
- Author context for personal posts
- Brand/company attribution
- Key link or CTA destination

Never invent author affiliation, customer stories, results, or proof.

## Step 3: Generate Posts

Generate only the requested posts. The source content and strategic handoff are the source of truth for substantive claims.

## Evidence Discipline

Use:
- **FACT** — directly supported by source/evidence
- **OBSERVATION** — observed pattern
- **INFERENCE** — reasoned interpretation
- **HYPOTHESIS** — unvalidated idea
- **BENCHMARK** — external reference with context
- **RECOMMENDATION** — creative/execution choice

Do not invent statistics, performance results, testimonials, competitor claims, or customer quotes.

Concrete numbers should appear only when supported by the source. If a useful proof point is missing, flag the gap rather than manufacture one.

## Channel Rules

### LinkedIn

Tailor the message to the actual audience and objective. Business impact can be emphasized when relevant, but do not assume every LinkedIn audience is a VP, CTO, or budget holder.

Brand posts may lead with a problem, insight, evidence, or relevant announcement. Personal posts may lead with genuine experience or learning when the author actually has that experience.

Format, length, hashtag, and link-placement guidance are practical defaults, not universal performance laws. Follow an established campaign or brand convention when one exists.

### Twitter / X

Use single posts or threads according to the complexity of the source and communication objective. Technical detail should come from real source material.

Do not claim that a particular hook, reply pattern, posting behavior, or format guarantees algorithmic distribution.

## Content Transformation Rules

Extract:
- Supported concrete evidence
- Genuine personal narrative
- Technical architecture when relevant
- Business implications when supported
- Surprising but defensible insights
- Required affiliation/disclosure

Cut unnecessary background, repetition, and unsupported hype. Do not remove legitimate uncertainty merely to make copy sound more confident.

## Formatting Rules

Maintain applicable brand/platform requirements, but avoid universal claims such as "this always performs" or "the algorithm rewards X".

Specific beats vague. Evidence beats invented precision. Clarity beats formula.

## Output Format

### LinkedIn

```
## [Brand/Personal] LinkedIn

[Post content]

---
Character count: [X]
```

### Twitter/X

```
## [Brand/Personal] Twitter/X

**Post 1 of N**
[Content]
[Character count: X]

**Post 2 of N**
[Content]
[Character count: X]

...
```

## Review Checklist

Before delivery:
- [ ] Strategic objective is inherited or explicitly established
- [ ] Audience matches the strategy/source
- [ ] Claims and numbers are supported
- [ ] No invented quotes, results, or affiliations
- [ ] Platform format serves the objective
- [ ] Engagement is not treated as the business outcome unless intended
- [ ] Platform behavior is not presented as guaranteed
- [ ] CTA matches the intended next action

## LinkedIn Carousel

Only suggest a carousel when it is useful to the objective or requested by the user. If invoked, consume the established brand/style reference and source material rather than assuming a carousel is always the next step.

## Adaptation Notes

- If source lacks personal narrative and personal posts are requested, flag the missing author input
- If source lacks concrete proof, flag the evidence gap
- If the requested format does not fit the objective, explain briefly and propose the closest suitable execution
- For shallow source content, prefer a simpler format rather than padding it into a thread
