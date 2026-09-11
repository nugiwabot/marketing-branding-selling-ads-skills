# Portable Agent Skills Architecture

This repository is designed so its core strategic intelligence can be reused across AI agents that support the Agent Skills `SKILL.md` format.

## Canonical Source

The canonical skill library is:

`.agents/skills/<skill-name>/SKILL.md`

These files contain the portable domain instructions. They should not require Claude-specific commands, APIs, hooks, or runtime behavior.

The strategic entry point is:

`.agents/skills/strategic-intelligence/SKILL.md`

This is the portable executive/diagnostic skill. It contains the core strategic behavior needed even when vendor-specific orchestration files are unavailable.

## Compatibility Layers

Vendor-specific directories may exist for compatibility with clients that do not discover `.agents/skills/` by default.

Examples:

- `.claude/skills/`
- `.codex/skills/`
- `.cursor/skills/`
- other client-specific skill locations

Compatibility copies must not introduce a different strategic decision model. If a client-specific copy differs from the canonical skill, the canonical `.agents/skills/` behavior is the intended source of truth.

## What Is Portable vs. Runtime-Specific

### Portable

- `SKILL.md` instructions
- YAML `name` and `description`
- Supporting `references/`, `scripts/`, and `assets/` shipped with a skill
- Strategic diagnosis and evidence methodology
- Specialist job-to-be-done definitions
- Evaluation cases and rubrics

### Runtime-specific

- Skill discovery directory
- File-reading implementation
- Web/search capability
- MCP/tool integrations
- Subagent delegation
- Permissions and sandboxing
- Slash-command syntax
- Memory/storage systems

A skill must not claim to perform an action that the host runtime cannot perform.

## Tool Capability Contract

The same strategic skill can run in different agents, but results can differ because tools differ.

For current or externally verifiable facts:

- With web/search access: research and cite current evidence.
- Without web/search access: state that external verification is unavailable; do not invent current facts.

For first-party files:

- With file access: inspect the repository or supplied documents.
- Without file access: state the limitation; do not imply the files were checked.

This distinction is a runtime capability issue, not a strategic-methodology issue.

## Portable Operating Flow

The intended runtime-independent flow is:

`User outcome → Strategic Intelligence → Research/Evidence → Diagnosis → Decision → Selected Specialists → Execution/QA → Measurement/Learning`

The system must not require a Claude-specific orchestrator for this behavior to exist.

## Agent Compatibility

The Agent Skills specification defines the `SKILL.md` package format but does not require every client to use the same discovery directory. The `.agents/skills/` convention is used here as the cross-client canonical location; clients may additionally load their own native paths.

A compatible client should:

1. Discover `.agents/skills/` or its configured skill path.
2. Read skill metadata first.
3. Load the full `SKILL.md` only when relevant.
4. Resolve bundled resources relative to the skill directory.
5. Preserve skill instructions across the task/session.

## Design Rule

**Write strategic intelligence once. Adapt only the runtime interface.**

Do not fork the strategic method per vendor.
