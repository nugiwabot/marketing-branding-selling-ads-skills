# Canonical Skill Source & Conflict Precedence

## Purpose

This repository exposes skills through multiple compatibility locations. The same logical skill must not behave differently merely because it was loaded through a different interface.

## Canonical Source

For shared domain skill behavior, `.agents/skills/<skill-name>/SKILL.md` is the canonical source of strategic logic unless a skill explicitly documents a platform-specific `.claude` extension.

`.claude/skills/` may provide Claude Code compatibility, but it must not override the canonical strategic decision boundary, evidence discipline, or governance rules.

## Precedence

When instructions conflict, use this precedence:

1. Safety, legal, and platform hard constraints
2. Global strategic governance and decision boundaries
3. Current structured strategic handoff
4. Canonical `.agents/skills/<skill-name>/SKILL.md`
5. Platform-specific `.claude/skills/<skill-name>/SKILL.md` implementation details
6. Examples, templates, historical memory, and stylistic defaults

A lower layer must not override a higher layer with a contradictory assumption.

## Duplicate Skill Rule

When `.agents/skills/` and `.claude/skills/` contain the same logical skill:

- Keep strategic reasoning aligned.
- Platform/interface-specific syntax may differ.
- Do not maintain different audience assumptions, business assumptions, strategic objectives, evidence standards, benchmark rules, or decision boundaries between the two copies.
- If a duplicate is stale, apply the shared governance as a minimum compatibility layer and synchronize the duplicate when it is safe to do so.

## Forbidden Silent Overrides

A duplicate or platform-specific skill must not silently reintroduce:

- fixed channel choices;
- universal posting cadences;
- universal content ratios;
- fixed competitor counts;
- universal benchmark thresholds;
- audience stereotypes;
- guaranteed conversion/performance claims;
- mandatory campaign chains;
- unsupported customer or competitor claims;
- specialist authority over strategic decisions.

Examples and templates may contain numbers, but those numbers are contextual examples unless explicitly marked as verified hard constraints.

## Routing Consistency

The canonical routing principle is:

`User outcome/decision → strategic diagnosis when needed → evidence/research → minimum required specialists → synthesis/execution → measurement/learning`

Do not let a compound keyword route such as "campaign", "leads", "content", "ads", or "launch" bypass Strategic Intelligence when the underlying decision is unclear.

## Verification

When updating one interface, check the equivalent skill/rule in the other interface before finalizing. A successful update is not considered complete if it creates a known strategic contradiction elsewhere.
