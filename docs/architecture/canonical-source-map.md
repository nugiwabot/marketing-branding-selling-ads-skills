# Canonical Source Map

This document defines where strategic behavior lives and how compatibility layers should relate to it.

## Authority Order

1. Safety, legal, regulatory, and platform hard constraints
2. `.agents/rules/` and applicable global governance
3. Current `schemas/strategic-diagnosis.json.template` handoff
4. `.agents/skills/<skill>/SKILL.md` canonical domain behavior
5. `.claude/skills/<skill>/SKILL.md` Claude Code compatibility behavior
6. `examples/`, `memory/`, templates, and historical notes

Lower layers may add implementation detail, but must not contradict higher layers.

## Core Canonical Artifacts

| Concern | Canonical location | Purpose |
|---|---|---|
| Global strategic boundary | `.agents/rules/marketing-branding-selling-ads.md` | Strategic-first behavior and specialist routing |
| Specialist evidence boundary | `.agents/rules/specialist-evidence-and-decision-boundary.md` | Evidence classes and specialist authority |
| Customer/VOC governance | `.agents/rules/customer-evidence-and-voc.md` | Customer evidence interpretation |
| Positioning/claims governance | `.agents/rules/positioning-claims-decision-boundary.md` | Positioning and claim evidence |
| Brand/positioning governance | `.agents/rules/brand-voice-positioning-governance.md` | Positioning → messaging → voice |
| Content planning governance | `.agents/rules/content-planning-decision-boundary.md` | Content role, channel, cadence, and ratios |
| Sales/conversion governance | `.agents/rules/sales-conversion-decision-boundary.md` | Funnel and commercial diagnosis |
| Measurement/learning | `.agents/rules/measurement-and-learning-loop.md` | Metrics, causality, experiments, learning |
| Strategic handoff contract | `schemas/strategic-diagnosis.json.template` | Machine-readable strategy handoff |
| Master agent behavior | `CLAUDE.md` | Master operating instructions |
| Agent architecture | `AGENTS.md` | Agent roles and system architecture |

## Compatibility Layers

`.claude/rules/` and `.claude/skills/` exist for Claude Code compatibility. They may contain platform-specific instructions, but strategic behavior must remain consistent with the canonical layer.

When an equivalent logical skill exists in both `.agents/skills/` and `.claude/skills/`, treat them as one skill with two interfaces.

## Handoff Integrity

Broad work follows:

`Outcome/Decision → Strategic Intelligence → Evidence/Research → Diagnosis → Structured Handoff → Minimum Necessary Specialists → Execution/QA → Measurement/Learning`

A specialist should not reconstruct or silently replace upstream strategy when a valid handoff exists.

## Framework Policy

Frameworks such as JTBD, STP, Obviously Awesome, MKT1 Perceptions, content ratios, pricing tiers, funnel models, ad benchmarks, and launch playbooks are **methods**.

They may be selected because they fit the problem. They do not become universal laws merely because they appear in a skill.

Numbers, thresholds, timings, sample sizes, cadence, ratios, and benchmark claims require context and evidence.

## Drift Audit Targets

When reviewing the repository, search for:

- `ALWAYS trigger` or equivalent automatic routing that bypasses strategic diagnosis;
- fixed `Research → Brief → Copy` chains presented as universal;
- audience stereotypes tied to platforms;
- universal content ratios or cadence;
- fixed competitor counts;
- universal KPI/CPA/CPL/ROAS/CTR thresholds;
- claims of guaranteed conversion, reach, virality, or algorithmic behavior;
- specialist instructions that silently redefine ICP, positioning, pricing, channel, or business objective;
- examples that are written as if they are verified business facts.

A finding should be patched only when it creates a real contradiction or materially increases hallucination/decision risk. Do not rewrite stable specialist knowledge merely to remove every number or template.
