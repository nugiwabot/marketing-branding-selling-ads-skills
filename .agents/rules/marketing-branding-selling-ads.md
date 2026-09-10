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

## 🎯 Mandatory Global Skill Routing

After strategic diagnosis when applicable, the agent MUST proactively reference and apply only the corresponding specialist skills from the `skills/` directory that are relevant to the task. For narrow execution requests, direct specialist routing remains allowed when strategic direction is already known.

### 1. Paid Ads & Campaign Automation
- **Multi-Platform Ad Automation**: Activate `multi-platform-ads-automation` when planning, auditing, validating, or automating campaigns across **Google Ads** (PMax, Demand Gen, VBB, Consent Mode v2), **Meta Ads** (Advantage+, CAPI, Creative is Targeting), **TikTok Ads** (Smart+, Symphony AI, 3-sec Hook Rate), and **LinkedIn Ads** (Predictive Audiences, ABM, Buying Committee).
- **Ad Copywriting**: Activate `ads` for creating multi-variant ad headlines, descriptions, and creative matrices.
- **Account Health & Auditing**: Activate `ads` / ad audit checklists to diagnose ad fatigue, CPA/ROAS decay, and budget reallocation.

### 2. Branding & Positioning
- **Positioning & Strategy**: Activate `messaging-positioning` and `messaging-positioning-workshop` for April Dunford (*Obviously Awesome*) frameworks.
- **Competitive Differentiation**: Activate `positioning-map` to generate 2x2 competitive positioning matrices.
- **Voice of Customer (VOC)**: Activate `customer-language-bank` to extract verbatim buyer phrases and customer vocabulary.
- **Claim & Consistency Verification**: Activate `claim-check` and `message-consistency-check` to substantiate marketing claims and ensure multi-channel consistency.

### 3. Marketing Strategy & Growth
- **Go-To-Market (GTM)**: Activate `go-to-market` for product launches, tiering, channel strategies, and launch checklists.
- **Campaign Briefs**: Activate `campaign-brief` for structured creative briefs (audiences, angles, deliverables, budgets).
- **Customer & Market Research**: Activate `customer-research` (JTBD framework) and `competitive-intelligence` (battlecards, kill points).
- **Win/Loss Analysis**: Activate `win-loss-reasons` to analyze deal closures, CRM notes, and conversion roadblocks.
- **Editorial & Content Planning**: Activate `editorial-calendar` for rolling 4-week / 3-month content roadmaps.
- **Viral & Growth Playbooks**: Activate `viral-launch-playbook` and `producthunt-launch`.

### 4. Content Creation & High-Conversion Copywriting
- **Conversion Copywriting**: Activate `copywriting` (PAS, AIDA, 4Cs, direct response frameworks, hook banks).
- **SEO & AEO Long-Form Content**: Activate `blog` for SEO & Answer Engine Optimization with Schema JSON-LD.
- **Social Media Content**: Activate `social-posts` and `social-content` for LinkedIn, X/Twitter, Instagram, and TikTok content creation.
- **Email Marketing**: Activate `email` and `email-sequence` for nurture drips, cold outreach, onboarding, and win-back flows.
- **Visual Asset Generation**: Activate `image` for multi-tier visual prompts and creative specifications.

### 5. Selling, Sales Enablement & Monetization
- **Sales Presentations**: Activate `sales-deck` for B2B narrative slide structures and PPTX generation.
- **Objection Handling**: Activate `objection-library` for real-time sales rebuttal scripts (price, timing, trust).
- **Pricing & Packaging**: Activate `pricing-packaging` for pricing tiers, value metrics, and monetization optimization.
- **Asset Review & QA**: Activate `claim-check` / QA verification before publishing marketing collateral.

---

## 🏢 Domain-Specific Context: Real Estate & Property (Yanproland / Rukos)

When the user works on real estate, rukos (rumah kost/ruko komersial), housing developments, or property investment marketing:

- Treat property-specific audience, positioning, channel, media, offer, and performance assumptions as **context to investigate**, not universal defaults.
- Do not automatically prioritize Google Search, Meta, TikTok, WhatsApp, or any other channel. Strategic Intelligence should determine channel roles from evidence about customer behavior, intent, demand, funnel role, economics, competition, measurement, and operational feasibility.
- Do not assume parents, investors, high-net-worth individuals, business owners, or passive-income seekers are the correct audience. Research or use verified first-party context to determine the relevant segment.
- Do not assume ROI, yield, passive-income, location, furnishing, management, or other property value propositions. Use only verified product facts and evidence-supported positioning.
- For investment/property claims, never guarantee returns or fabricate financial outcomes. Any potential-yield or return statement must be based on verified inputs and clearly framed with appropriate assumptions/disclaimers.

Property context can inform hypotheses and research questions, but it must not silently override the Executive Strategic Intelligence Layer.
