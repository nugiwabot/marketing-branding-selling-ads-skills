# Global Marketing, Branding, Selling, & Ads Operating Rule

This rule is mandatory across all conversations whenever the USER asks questions or requests tasks related to **Branding, Marketing, Selling, Conversion, Paid Ads, Copywriting, Campaign Strategy, or Real Estate / Property Growth (Yanproland, Rukos, etc.)**.

---

## 🧠 Executive Strategic Intelligence Layer

For broad, ambiguous, cross-functional, or decision-oriented requests, the agent MUST use `strategic-intelligence` as the first diagnostic layer before routing to specialist skills.

This applies to requests involving:
- business or marketing strategy
- strategic audit or diagnosis
- market, customer, competitor, or industry analysis
- GTM or growth strategy
- brand or positioning strategy
- offer, pricing, packaging, or value proposition decisions
- customer journey, funnel, conversion, or sales diagnosis
- channel or media strategy
- integrated marketing planning
- campaign strategy when the underlying problem or objective is unclear
- SPV/manager-level planning, prioritization, roadmap, KPI, or decision support

The strategic layer must:
1. Clarify the business objective and decision to be made.
2. Identify what is known, unknown, assumed, and required as evidence.
3. Determine what research is needed before making strategic claims.
4. Select only the frameworks relevant to the diagnosed problem.
5. Select only the specialist skills required for the next stage.
6. Diagnose root causes rather than treating symptoms as causes.
7. Evaluate channels/media from customer behavior, intent, economics, funnel role, measurement, and operational feasibility.
8. Produce prioritized recommendations and measurable next actions.

Do NOT mechanically activate every specialist skill. Strategic Intelligence is the decision layer; specialist skills are domain executors.

For narrow execution requests where the strategic direction is already known (for example, writing a caption, email, ad copy, sales script, or editing a supplied asset), the agent MAY bypass Strategic Intelligence and route directly to the appropriate specialist skill.

---

## 🔗 Structured Handoff Contract

For broad strategic work, the structured output defined in `schemas/strategic-diagnosis.json.template` is the canonical machine-readable handoff from Strategic Intelligence to downstream specialists.

A downstream specialist MUST, when a structured diagnosis is available:
1. Confirm the handoff `status` is appropriate for specialist consumption, normally `ready_for_handoff`.
2. Consume the existing business objective, decision, evidence map, assumptions, diagnosis, priorities, channel/media role, and specialist job-to-be-done instead of reconstructing them from scratch.
3. Treat `strategic-intelligence` as the source of truth for strategic decisions unless new evidence materially contradicts it.
4. Preserve evidence classifications and distinguish facts from observations, inferences, hypotheses, and benchmarks.
5. State material conflicts or missing inputs rather than silently changing the diagnosis.
6. Return material new evidence or changed assumptions to Strategic Intelligence when they could alter the strategic decision.

If no structured diagnosis is available, the specialist may use the applicable governance rule and available context, but must not pretend that an unverified strategic decision is validated.

The human-readable strategic synthesis may be adaptive; the structured handoff must remain complete enough for routing and execution.

---

## 🎯 Mandatory Global Skill Routing

After strategic diagnosis when applicable, the agent MUST proactively reference and apply only the corresponding specialist skills from the `skills/` directory that are relevant to the task. For narrow execution requests, direct specialist routing remains allowed when strategic direction is already known.

### 1. Paid Ads & Campaign Automation
- **Multi-Platform Ad Automation**: Activate `multi-platform-ads-automation` when planning, auditing, validating, or automating campaigns across **Google Ads**, **Meta Ads**, **TikTok Ads**, and **LinkedIn Ads**. Platform-specific features are implementation options, not automatic strategic priorities.
- **Ad Copywriting**: Activate `ads` for creating multi-variant ad headlines, descriptions, and creative matrices.
- **Account Health & Auditing**: Activate `ads-auditor` / applicable ad audit checklists to diagnose ad fatigue, CPA/ROAS decay, and budget allocation issues.

### 2. Branding & Positioning
- **Positioning & Strategy**: Activate `messaging-positioning` and `messaging-positioning-workshop` when the diagnosed problem requires positioning or messaging work.
- **Competitive Differentiation**: Activate `positioning-map` when competitive positioning analysis is required.
- **Voice of Customer (VOC)**: Activate `customer-language-bank` when customer-language evidence is required.
- **Claim & Consistency Verification**: Activate `claim-check` and `message-consistency-check` when claims or cross-surface consistency require verification.

### 3. Marketing Strategy & Growth
- **Go-To-Market (GTM)**: Activate `go-to-market` when the diagnosis indicates a GTM decision is required.
- **Campaign Briefs**: Activate `campaign-brief` when a campaign is strategically justified and needs a structured brief.
- **Customer & Market Research**: Activate `customer-research` and `competitive-intelligence` when research gaps require those specialists.
- **Win/Loss Analysis**: Activate `win-loss-reasons` when deal evidence is relevant.
- **Editorial & Content Planning**: Activate `editorial-calendar` when content planning is a diagnosed workstream.
- **Viral & Growth Playbooks**: Activate `viral-launch-playbook` or `producthunt-launch` only when the strategic diagnosis supports those interventions.

### 4. Content Creation & High-Conversion Copywriting
- **Conversion Copywriting**: Activate `copywriting` when the diagnosed workstream requires conversion copy.
- **SEO & AEO Long-Form Content**: Activate `blog` when search content is strategically relevant.
- **Social Media Content**: Activate `social-posts` and `social-content` when social content is a relevant execution layer.
- **Email Marketing**: Activate `email` and `email-sequence` when lifecycle or communication needs justify them.
- **Visual Asset Generation**: Activate `image` when visual production is required.

### 5. Selling, Sales Enablement & Monetization
- **Sales Presentations**: Activate `sales-deck` when the sales narrative requires a deck.
- **Objection Handling**: Activate `objection-library` when buyer/deal evidence indicates objection handling is relevant.
- **Pricing & Packaging**: Activate `pricing-packaging` when pricing/packaging is a diagnosed decision.
- **Asset Review & QA**: Activate `claim-check` / QA verification before publishing or shipping material when appropriate.

---

## 🏢 Domain-Specific Context: Real Estate & Property (Yanproland / Rukos)

When the user works on real estate, rukos (rumah kost/ruko komersial), housing developments, or property investment marketing:

- Treat property-specific audience, positioning, channel, media, offer, and performance assumptions as **context to investigate**, not universal defaults.
- Do not automatically prioritize Google Search, Meta, TikTok, WhatsApp, or any other channel. Strategic Intelligence should determine channel roles from evidence about customer behavior, intent, demand, funnel role, economics, competition, measurement, and operational feasibility.
- Do not assume parents, investors, high-net-worth individuals, business owners, or passive-income seekers are the correct audience. Research or use verified first-party context to determine the relevant segment.
- Do not assume ROI, yield, passive-income, location, furnishing, management, or other property value propositions. Use only verified product facts and evidence-supported positioning.
- For investment/property claims, never guarantee returns or fabricate financial outcomes. Any potential-yield or return statement must be based on verified inputs and clearly framed with appropriate assumptions/disclaimers.

Property context can inform hypotheses and research questions, but it must not silently override the Executive Strategic Intelligence Layer.
