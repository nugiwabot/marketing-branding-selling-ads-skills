# Marketing Branding Selling Ads Skills — Multi-Agent Architecture

This repository implements a strategic, evidence-driven AI marketing operating system for Branding, Marketing Strategy, Content Production, Sales Enablement, Paid Acquisition, Measurement, and Learning.

---

## Core Architecture

The system is **not a fixed linear pipeline**. It is a decision architecture in which Strategic Intelligence diagnoses the problem, research supplies evidence, specialist skills execute defined jobs, and measurement/learning feeds material findings back into strategy.

```text
[User Goal / Business Problem]
          │
          ▼
[Orchestrator — Intake & Routing]
          │
          ├── Narrow execution with known direction
          │        └──► Relevant Specialist
          │
          └── Broad / ambiguous / decision-oriented
                   │
                   ▼
          [Strategic Intelligence]
                   │
          ┌────────┼─────────┐
          ▼        ▼         ▼
       Research  Diagnosis  Priorities
          │        │         │
          └────────┼─────────┘
                   ▼
          [Structured Handoff]
                   │
                   ▼
        [Selected Specialists]
                   │
                   ▼
          [Execution / QA]
                   │
                   ▼
          [Measurement / Learning]
                   │
          ┌────────┴────────┐
          │                 │
     No material change   Diagnosis changes
          │                 │
        Continue        ► Strategic Intelligence
```

### Decision hierarchy

1. **Strategic Intelligence** owns the diagnosis, strategic decision framing, research needs, priorities, and cross-functional synthesis.
2. **Research** owns evidence gathering and confidence assessment within the defined decision question.
3. **Specialists** own their domain job-to-be-done and execution/analysis within the strategic boundary.
4. **Measurement & QA** evaluate outcomes, evidence quality, and learning.
5. **Strategic feedback** occurs whenever new evidence materially changes the diagnosis, objective, audience, offer, positioning, channel role, economics, or priority.

---

## Specialist Agent Roles

### 1. Orchestrator (`agents/mos-orchestrator.md`)
- Request intake, work-level detection, routing, prioritization, and handoff coordination.
- Selects the minimum specialist set needed for the actual business problem.

### 2. Researcher (`agents/mos-researcher.md`)
- Market, customer, competitor, channel/media, VOC, and conversion evidence gathering.
- Produces structured evidence rather than unsupported strategic prose.

### 3. Strategist (`agents/mos-strategist.md`)
- Converts validated diagnosis/evidence into GTM, positioning, messaging, offer, channel, campaign, and execution priorities as appropriate.

### 4. Copywriter (`agents/mos-copywriter.md`)
- Converts validated strategy and source material into platform-appropriate copy and content assets.

### 5. Ads Auditor (`agents/ads-auditor.md`)
- Paid-media performance analysis, funnel diagnostics, data-quality checks, and evidence-based optimization recommendations.

### 6. Asset Reviewer (`agents/asset-reviewer.md`)
- Evidence, message, brand, conversion-friction, and compliance QA before publication or execution.

---

## Structured Handoff

Broad strategic work uses `schemas/strategic-diagnosis.json.template` as the machine-readable handoff contract.

A valid handoff carries at minimum:
- business objective;
- decision required;
- known/unknown/assumed context;
- research gaps and evidence confidence;
- diagnosis and strategic tensions;
- customer/market implications;
- channel/media role;
- priorities;
- selected workstreams;
- each specialist's job-to-be-done;
- measurement logic;
- handoff controls.

The diagnosis lifecycle is explicit:

`draft → researching → diagnosed → ready_for_handoff → superseded`

Specialists must preserve the diagnosis unless new evidence creates a material conflict. A material conflict is returned to Strategic Intelligence rather than silently rewriting strategy locally.

---

## Governance Rules

Shared rules under `.agents/rules/` govern cross-cutting behavior, including:

- Strategic routing and specialist decision boundaries
- Customer evidence / VOC discipline
- Positioning, claims, and message consistency
- Brand voice and positioning governance
- Content-planning decision boundaries
- Sales and conversion decision boundaries
- Measurement and learning loops

These are **reasoning constraints**, not additional skills that should all be invoked on every task.

---

## Execution Principle

Use the smallest workflow that can answer the actual question.

Do not:
- invoke every specialist by default;
- assume content, campaigns, paid ads, or sales tactics are the solution;
- turn benchmarks or templates into universal laws;
- allow a specialist to silently replace the strategic diagnosis;
- optimize intermediate metrics while ignoring the business outcome.

For narrow execution requests with strategic direction already known, direct specialist execution is allowed.

For broad, ambiguous, cross-functional, audit, planning, growth, business, marketing, branding, channel, media, sales, or SPV requests, route through Strategic Intelligence first.

---

## Standard End-to-End Loop

```text
Goal
 ↓
Diagnosis
 ↓
Evidence / Research
 ↓
Decision
 ↓
Specialist Workstreams
 ↓
Execution
 ↓
QA / Measurement
 ↓
Learning
 ↓
Strategic Update when warranted
```
