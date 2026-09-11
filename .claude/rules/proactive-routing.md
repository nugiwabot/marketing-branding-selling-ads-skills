# Proactive Marketing OS Routing

## Purpose

Automatically route marketing requests without forcing the user to know internal skill names. Routing should be **outcome-led and diagnosis-aware**, not a collection of keyword-triggered pipelines.

## Routing Hierarchy

Use this order:

1. **Detect the user's outcome / decision.**
2. **Classify work level.**
3. **For broad, ambiguous, cross-functional, audit, planning, growth, business, branding, marketing, channel/media, sales, or SPV-level work, route to `strategic-intelligence` first.**
4. **For narrow execution with already-established strategic direction, route directly to the relevant specialist.**
5. **After strategic diagnosis, select only the minimum specialist set required by the diagnosed workstream.**
6. **Carry the structured diagnosis/handoff into specialist execution when available.**

## Tier 1 — Direct Execution

These requests can bypass Strategic Intelligence **when the strategic direction is already known in context**:

| User Request | Specialist |
|---|---|
| write/rewrite a page, headline, ad copy | `/copywriting` |
| write a defined email/newsletter | `/email` or `/email-sequence` |
| create a defined LinkedIn/X/Instagram post | `/social-content` or `/social-posts` |
| produce a blog from an established brief | `/blog` |
| create a defined sales deck | `/sales-deck` |
| create ad creative from an established campaign direction | `/ads` |
| review an existing asset | `/asset-reviewer` / `/claim-check` |

Do not infer a new business strategy from a narrow execution request unless the user asks for it or material evidence requires escalation.

## Tier 2 — Strategic / Diagnostic Entry

These patterns should route to `/strategic-intelligence` first:

- "How should we market this?"
- "How do we get more customers/leads/sales?"
- "What channels should we use?"
- "Should we use Instagram/Google/Meta/TikTok/LinkedIn?"
- "Audit this business/marketing/sales funnel."
- "Why aren't our ads/content/sales working?"
- "Build a marketing plan/GTM strategy."
- "Position this brand/product."
- "We need a campaign" when the audience, bottleneck, offer, channel role, or objective is not already established.
- "We need more users" / "we need more leads" / "we need more revenue."
- "What should the SPV/team prioritize?"

Strategic Intelligence decides whether research, positioning, GTM, content, paid media, sales, pricing, or another intervention is actually warranted.

## Tier 3 — Compound Requests

Do **not** use fixed chains such as `Research → Brief → Copy` automatically.

Instead:

`User outcome → Strategic Intelligence (when required) → Diagnosis → Evidence/Research → Selected specialists → Strategic synthesis → Execution → Measurement/Learning`

A broad request to "promote X" does not prove that a campaign is the answer.

A request for "more leads from channel X" does not prove channel X is the correct channel.

A request to "fix ads" does not prove ads are the root cause.

## Specialist Routing Rules

After strategic diagnosis:

| Diagnosed workstream | Relevant specialist(s) |
|---|---|
| Customer/VOC evidence | `/customer-research`, `/customer-language-bank` |
| Competitive intelligence | `/competitive-intelligence`, `/how-they-market` |
| Positioning / messaging | `/messaging-positioning`, `/positioning-map`, `/claim-check`, `/message-consistency-check` |
| GTM / channel decision | `/go-to-market` plus only required channel specialists |
| Campaign strategy | `/campaign-brief` |
| Content strategy/planning | `/editorial-calendar`, `/blog`, `/social-content`, `/email` as required |
| Paid media strategy/execution | `/multi-platform-ads-automation`, `/ads`, `/ads-auditor` as required |
| Sales/conversion | `/sales-deck`, `/objection-library`, `/pricing-packaging`, `/win-loss-reasons` as required |
| QA | `/asset-reviewer`, `/claim-check`, or other relevant verifier |

Never invoke every available skill by default.

## Ambiguity

If the intent is ambiguous, ask about the **business outcome or decision**, not which skill to use.

Good:
> "Are you trying to increase qualified leads, improve conversion from existing leads, or decide where to invest marketing budget?"

Avoid:
> "Which skill should I use?"

Do not ask for clarification when existing context already answers the question.

## Structured Handoff

When `schemas/strategic-diagnosis.json.template` is used, downstream specialists should consume the handoff rather than reconstruct strategy from scratch.

A handoff should normally be in a state appropriate for specialist use, such as `ready_for_handoff`.

Specialists must preserve:
- objective
- decision
- diagnosis
- evidence status
- assumptions
- priorities
- channel/media role
- job-to-be-done
- measurement intent

If specialist evidence materially changes the diagnosis, return the new evidence and implications to Strategic Intelligence.

## Memory / Context

Before marketing execution, inspect relevant existing context where available:
- `memory/marketing-os/brand-voice.md`
- `memory/marketing-os/campaign-history.md`
- brand/product/customer context
- prior strategy and measurement results

Do not treat memory as proof of current market conditions when the claim is time-sensitive; verify current external facts when required.

## Core Rule

**Route by the decision the user needs, not by the keyword they happened to type.**
