# Compatibility Layer Guardrails

These rules protect Claude Code compatibility skills that may contain older templates or platform-specific defaults. They do not replace the canonical skill; they prevent known stale assumptions from becoming strategic decisions.

## Editorial / Content Planning

When executing `.claude/skills/editorial-calendar`:

- Treat MKT1 Perceptions, content pillars, 70/30, reactive buffers, pillar coverage, repurposing, cadence, and fixed calendar horizons as methods or starting hypotheses.
- Do not fail a calendar merely because a fixed ratio, frequency, or pillar-coverage rule is not met.
- Do not require every pillar to appear on a fixed interval.
- Do not assume a 70/30 product/non-product split is optimal.
- A reduced calendar, a single high-value content piece, a repurposing-first plan, or no new content can be the correct recommendation when supported by the diagnosis.
- Channel and format selection must follow audience evidence, customer journey, business objective, content role, measurement, and capacity.

## Paid Media Automation

When executing `.claude/skills/multi-platform-ads-automation`:

- Platform configuration values such as lookalike percentages, audience ranges, refresh cadence, ad counts, exclusions, bidding modes, frequency thresholds, or conversion-volume requirements are implementation defaults or hypotheses unless the platform documentation or account requirements make them hard constraints.
- Do not describe an audience percentage as universally better for quality or reach.
- Do not automatically exclude competitors unless that exclusion is strategically justified, technically valid, and relevant to the campaign objective.
- Do not require a fixed 30-day refresh cadence; use performance, audience availability, platform behavior, seasonality, and test design.
- Do not infer that a platform feature is strategically appropriate because the feature exists.
- Account automation must preserve the strategic diagnosis and measurement intent provided upstream.

## General Compatibility Rule

If a legacy compatibility skill conflicts with `.agents/rules/`, the current structured strategic handoff, or the canonical `.agents/skills/<skill>/SKILL.md`, follow the higher-authority layer.

Do not silently convert a template into a business rule.
