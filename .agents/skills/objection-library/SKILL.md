---
name: objection-library
description: >
  Extract every objection buyers raise across your full set of sales calls, rank
  them by how often they come up, capture them in the buyer's own words, and tag
  each to the point in the funnel where it lands. Use when you want the real
  objections instead of the three sales happens to remember, when building or
  refreshing objection handling and enablement, or when you have a stack of call
  recordings and no time to listen through them. Triggers: "what objections are
  we getting," "objection handling," "build a rebuttal doc," "what's blocking
  deals," "sales enablement from calls."
---

# Objection Library

## Strategic Boundary

This is a **sales diagnosis and enablement specialist**, not the owner of the overall business strategy.

For broad, ambiguous, cross-functional, or decision-oriented requests, consume the output of `strategic-intelligence` first. Preserve its objective, decision, diagnosis, priorities, evidence status, and constraints.

Do not assume that an objection is merely a persuasion problem. A recurring objection may indicate a problem with the product, offer, pricing, positioning, audience fit, qualification, trust, proof, sales process, customer experience, or market readiness. If the evidence points upstream, flag that issue instead of inventing a stronger rebuttal.

If new evidence changes the strategic diagnosis, return the finding to Strategic Intelligence rather than silently overriding it.

## What this does

Reads sales conversations and returns a ranked library of the objections buyers actually raise - each one in the buyer's own language, counted by frequency when the evidence permits, and tagged to the stage of the funnel where it shows up. It also records how reps currently respond and whether the available evidence suggests that response helps move the deal forward.

The point is coverage. Teams usually build objection handling from the handful of objections that stung most recently. This gives you the broader set represented in the supplied evidence.

## Why this is a Fable-recommended job

Objections are scattered across many hours of talk. To rank them honestly you have to hear all of them and count across the whole set, which means holding every transcript at once. Claude Fable 5 can take the full call library in a single run and surface patterns no one person sitting through calls would tally.

**If Fable is not available or the budget is spent:** batch it. Run manageable batches of calls, produce a partial objection list per batch, then merge and re-rank the partial lists in a final pass. Batch size is an operational choice, not a quality guarantee.

## Evidence to gather first

- Sales and demo call transcripts across the funnel (discovery through negotiation)
- Objection notes from reps or deal desk
- Support and onboarding calls, if pre-sale concerns surface there
- Lost-deal notes

Read `.agents/product-marketing-context.md` first if it exists, so objections can be mapped against positioning and competitors.

## Process

1. Confirm the call set and time window. Report the actual evidence included.
2. Read the available calls. Pull each moment where a buyer raises a concern, hesitation, or blocker - stated as a question, a worry, or a flat no.
3. Normalize duplicates: the same underlying objection phrased multiple ways becomes one entry, with variant phrasings retained as examples.
4. Count how many supplied calls each objection appears in when reliable, and tag the funnel stage.
5. Capture the current rep response for each and distinguish observed outcomes from interpretation.
6. Diagnose whether the objection is primarily a sales-handling issue or evidence of an upstream problem.
7. Produce the library.

## Output format

- **Summary** - calls analyzed, time window, top objections by frequency when measurable, and by funnel stage.
- **Objection table** - objection (in buyer language) | funnel stage | frequency/evidence basis | representative quote with source | current response | observed or inferred effect.
- **Root-cause signals** - objections that may indicate offer, pricing, positioning, qualification, product, trust, proof, process, or market issues.
- **Gaps** - objections with no consistent response, or where the current response appears weak based on available evidence.
- **Recommended handling** - suggested responses for relevant objections, grounded in responses that appear to work in the supplied calls before general practice.
- **Strategic feedback** - findings that should be returned upstream to Strategic Intelligence.

## The evidence standard

Every objection entry must quote at least one real buyer moment and cite its source (call name, date, or line). Use the buyer's words, not a tidied-up paraphrase.

If frequency cannot be counted reliably from the material, say so rather than inventing a number. A response that appears to work in one or a few calls is evidence of an observed pattern, not proof of causal effectiveness.

Recommended responses should be built from responses that appear to work in your own calls before any that are added from general practice - and anything added from general practice must be labeled as such.

Never fabricate buyer objections, quotes, deal outcomes, customer claims, competitor claims, conversion rates, win rates, or revenue impact.

## Decision Boundary

The specialist may:
- extract and classify buyer objections;
- analyze patterns in supplied sales evidence;
- evaluate current handling against observed outcomes;
- suggest response language;
- identify likely upstream causes and send them back to strategy.

The specialist may not independently decide:
- the company's strategic objective;
- the target market or ICP without evidence;
- the positioning or value proposition;
- pricing or commercial policy;
- which channel or sales motion the business should prioritize;
- that objection handling is the highest-leverage intervention.

Those decisions belong to Strategic Intelligence and the appropriate upstream specialists.