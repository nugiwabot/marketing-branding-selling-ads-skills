# Multi-Agent Architecture & Operating Guidelines

This repository implements an autonomous, multi-agent AI marketing department structured for high-performance Branding, Marketing Strategy, Content Production, and Sales Enablement.

---

## 👥 Specialized Agent Roles

### 1. Orchestrator (gents/mos-orchestrator.md)
- **Role**: Team lead and workflow conductor.
- **Responsibilities**: Decomposes user goals, routes tasks to specialist agents, ensures handoff integrity, and synthesizes final deliverables.

### 2. Researcher (gents/mos-researcher.md & gents/how-they-market.md)
- **Role**: Market & competitive intelligence analyst.
- **Responsibilities**: Conducts JTBD customer research, extracts Voice of Customer (VOC) verbatim, builds competitive battlecards, and reverse-engineers competitor funnels.

### 3. Strategist (gents/mos-strategist.md)
- **Role**: GTM architect & positioning master.
- **Responsibilities**: Defines April Dunford positioning matrices, develops messaging hierarchies, designs pricing/packaging tiers, and formulates creative briefs.

### 4. Copywriter (gents/mos-copywriter.md)
- **Role**: Direct-response and conversion copywriter.
- **Responsibilities**: Writes high-converting headlines, ad copy, long-form SEO/AEO blogs, multi-channel social posts, and email nurture sequences.

### 5. Ads Auditor (gents/ads-auditor.md)
- **Role**: Paid acquisition performance specialist.
- **Responsibilities**: Audits ad accounts (Meta, Google, LinkedIn), calculates health scores, diagnoses fatigue, and suggests budget/bid optimizations.

### 6. Asset Reviewer (gents/asset-reviewer.md)
- **Role**: Quality gatekeeper and conversion auditor.
- **Responsibilities**: Reviews drafts against evidence rules, tone guidelines, compliance standards, and conversion friction points before publishing.

---

## 🔄 Standard Workflow Pipelines

`	ext
[Goal Intake] ──► [Orchestrator]
                        │
                        ▼
                 [Researcher] ────► Builds Customer & Competitor Insights
                        │
                        ▼
                 [Strategist] ────► Develops GTM / Positioning / Brief
                        │
                        ▼
                 [Copywriter] ────► Crafts Ads / Blogs / Emails / Decks
                        │
                        ▼
               [Asset Reviewer] ──► QA & Validation (Pass / Iterate)
                        │
                        ▼
                 [Final Output]
`
