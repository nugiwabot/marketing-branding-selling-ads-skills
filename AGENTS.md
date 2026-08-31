# Marketing Branding Selling Ads Skills — Multi-Agent Architecture

This repository implements an autonomous, multi-agent AI marketing department structured for high-performance Branding, Marketing Strategy, Content Production, Sales Enablement, and Paid Ads Automation.

---

## 👥 Specialized Agent Roles

### 1. Orchestrator (`agents/mos-orchestrator.md`)
- **Role**: Team lead and workflow conductor.
- **Responsibilities**: Decomposes user goals, routes tasks to specialist agents, ensures handoff integrity, and synthesizes final deliverables.

### 2. Researcher (`agents/mos-researcher.md` & `agents/how-they-market.md`)
- **Role**: Market & competitive intelligence analyst.
- **Responsibilities**: Conducts JTBD customer research, extracts Voice of Customer (VOC) verbatim, builds competitive battlecards, and reverse-engineers competitor funnels.

### 3. Strategist (`agents/mos-strategist.md`)
- **Role**: GTM architect & positioning master.
- **Responsibilities**: Defines April Dunford positioning matrices, develops messaging hierarchies, designs pricing/packaging tiers, and formulates creative briefs.

### 4. Copywriter (`agents/mos-copywriter.md`)
- **Role**: Direct-response and conversion copywriter.
- **Responsibilities**: Writes high-converting headlines, ad copy, long-form SEO/AEO blogs, multi-channel social posts, and email nurture sequences.

### 5. Ads Auditor (`agents/ads-auditor.md` & `skills/multi-platform-ads-automation/`)
- **Role**: Paid acquisition & ad automation specialist.
- **Responsibilities**: Audits ad accounts (Google, Meta, TikTok, LinkedIn), calculates health scores, enforces pre-flight validation rules, diagnoses fatigue, and executes automated campaign workflows.

### 6. Asset Reviewer (`agents/asset-reviewer.md`)
- **Role**: Quality gatekeeper and conversion auditor.
- **Responsibilities**: Reviews drafts against evidence rules, tone guidelines, policy compliance standards, and conversion friction points before publishing.

---

## 🔄 Standard Workflow Pipelines

```text
[Goal Intake] ──► [Orchestrator]
                        │
                        ▼
                 [Researcher] ────► Builds Customer & Competitor Insights
                        │
                        ▼
                 [Strategist] ────► Develops GTM / Positioning / Campaign Brief
                        │
                        ▼
                 [Copywriter] ────► Crafts Ads / Blogs / Emails / Decks
                        │
                        ▼
               [Asset Reviewer] ──► QA & Validation (Pass / Iterate)
                        │
                        ▼
                 [Ads Auditor]  ──► Pre-Flight Validation & Campaign Launch
                        │
                        ▼
                 [Final Output / Live Campaign]
```
