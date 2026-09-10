# Specialist Evidence & Decision Boundary

## Purpose

This rule applies to specialist skills across the Marketing, Branding, Selling, and Ads system. It prevents downstream playbooks from becoming accidental executive strategy.

## Architecture

For broad, ambiguous, cross-functional, audit, planning, growth, business, marketing, branding, sales, channel, media, or SPV requests:

`User Request → Strategic Intelligence → Evidence/Research → Specialist Selection → Specialist Work → Strategic Synthesis → Execution`

A specialist may execute a narrow task directly when the strategic direction is already established.

## Decision Boundary

Strategic Intelligence owns:
- the business objective and decision to be made;
- diagnosis of bottlenecks, opportunities, and root causes;
- research scope and evidence requirements;
- framework selection;
- strategic priorities and trade-offs;
- whether a specialist/channel/tactic is actually needed.

Specialists own:
- domain-specific analysis or execution after receiving the relevant strategic context;
- implementation details, templates, technical constraints, and domain methods;
- specialist-level hypotheses and recommendations within the approved strategic boundary.

A specialist must not silently replace an upstream strategic decision with a favorite framework, channel, benchmark, playbook, or platform default.

## Evidence Discipline

Label material claims as appropriate:
- **FACT** — verified evidence;
- **OBSERVATION** — directly observed from supplied data;
- **INFERENCE** — reasoned interpretation;
- **HYPOTHESIS** — testable but unverified;
- **BENCHMARK** — external reference, not a fact about the business;
- **RECOMMENDATION** — proposed action.

Never fabricate business-specific numbers, market size, customer counts, performance metrics, competitor facts, pricing, conversion rates, or economics.

Numerical examples, suggested sample sizes, timelines, tier ratios, KPI thresholds, and performance targets are not universal truths unless verified as genuine hard constraints. Treat them as benchmarks, examples, or hypotheses and state which.

## Competitive Intelligence Controls

When using `competitive-intelligence`:
- Competitor claims about pricing, features, positioning, customers, market presence, growth, traffic, funding, headcount, strategic direction, strengths, weaknesses, or channel activity must be treated as **unverified until supported by an appropriate source**.
- Distinguish **competitor-stated claims** from independently verified facts, customer-reported experience, analyst/review evidence, and internal win/loss evidence.
- Do not infer competitor effectiveness merely from the existence of a tactic or channel. Presence is evidence of activity, not evidence of performance.
- Do not use fixed competitor counts such as "top 3-5" as a universal rule. Select the competitive set based on the decision, market structure, customer overlap, threat, and available evidence.
- Do not treat fixed monitoring cadences (for example weekly/monthly/quarterly) as mandatory defaults. Cadence should follow volatility, strategic importance, signal frequency, research cost, and decision needs.
- Do not treat fixed research timing or sample-size guidance as universal. Adapt win/loss research timing and depth to the buying cycle, accessibility of participants, recency of the decision, and the question being answered.
- Do not publish competitor comparison claims, testimonials, customer outcomes, pricing, migration timelines, or superiority statements unless they are supported, attributable, or explicitly marked as unknown/hypothesis.
- When evidence conflicts, preserve the conflict and confidence level rather than forcing a single narrative.

## Specialist Feedback Loop

If specialist research or execution produces evidence that changes the diagnosis, do not continue optimizing inside the specialist's original assumption. Return the new evidence and implications to Strategic Intelligence for synthesis.

## Anti-Pattern

Do not mechanically invoke every available skill. Select only specialists whose work addresses the diagnosed problem or a clearly required decision.
