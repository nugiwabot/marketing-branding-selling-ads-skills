---
name: autoresearch
description: Optimize an existing skill through controlled prompt experiments, binary evaluations, and evidence-based mutation logs.
---

# Autoresearch for Skills

Autoresearch is a **skill-improvement experiment loop**. It improves an existing skill by testing targeted prompt mutations against defined evaluations.

## Strategic Boundary

Autoresearch optimizes how a skill executes its defined job. It must not silently change the skill's strategic purpose, decision authority, evidence standards, or specialist boundaries merely to improve an eval score.

If an experiment reveals that the skill's role or strategic boundary is wrong, stop the mutation loop and escalate the design issue rather than optimizing around it.

## Experiment Principles

1. Define the target skill and desired outcome.
2. Establish representative test inputs.
3. Define binary, behavior-based evals.
4. Establish a baseline before mutation.
5. Change one meaningful variable at a time where practical.
6. Run the same evaluation suite.
7. Keep a mutation only when evidence shows a meaningful improvement without regressions.
8. Record the reason, result, and remaining failure modes.
9. Prefer simplification when it preserves or improves performance.

Do not optimize against a narrow metric at the expense of truthfulness, strategic correctness, evidence quality, usability, or generalization.

## Required Experiment Inputs

Before a run, establish:
- **Target skill** — exact skill file.
- **Test inputs** — representative scenarios covering the intended job.
- **Eval criteria** — 3–6 binary checks that test behavior, not superficial wording.
- **Runs per experiment** — choose according to reliability/cost; a default is only a starting point.
- **Budget/experiment cap** — define a finite limit unless the environment explicitly supports supervised continuation.

Do not require arbitrary fixed counts such as 3–5 test prompts or 5 runs when another design is better supported by the task.

## Eval Design

Good evals test whether the output:
- follows the intended strategic boundary;
- preserves evidence discipline;
- handles known and unknown information correctly;
- completes the skill's actual job;
- avoids known failure modes;
- generalizes across representative inputs.

Do not reward an output merely for mentioning the eval criteria.

## Baseline

Run the original skill as-is before changing it when the environment supports controlled evaluation.

Record:
- baseline score
- test inputs
- eval definitions
- model/runtime context when relevant
- known limitations

If the baseline is already strong, consider whether further mutation has enough expected value to justify its cost.

## Mutation Loop

For each experiment:

1. Inspect failing outputs.
2. Identify one likely failure mechanism.
3. Form one mutation hypothesis.
4. Make one targeted change.
5. Run the evaluation suite.
6. Compare against the prior baseline.
7. Keep or discard the mutation.
8. Log the result.

Avoid large rewrites, unrelated additions, and changes that make the skill longer without solving an observed failure.

## Guardrails

Never optimize toward:
- fabricated evidence;
- unsupported market/customer claims;
- guaranteed performance;
- generic benchmark compliance;
- strategic decisions outside the skill's authority;
- gaming the evaluator rather than improving the underlying behavior.

If a mutation improves a score but introduces a material regression in truthfulness, strategic alignment, or task quality, discard it.

## Stopping Conditions

Use a finite experiment budget or another explicit stopping rule.

Stop when:
- the experiment cap is reached;
- the improvement ceiling is reached with diminishing returns;
- repeated mutations fail to improve the result;
- the remaining failures require new evidence or a redesign rather than prompt wording;
- a strategic/design boundary problem is discovered.

Do not use an unconditional infinite loop or claim that autonomous optimization should run forever.

## Results Log

Maintain a changelog containing:

```markdown
## Experiment [N] — KEEP/DISCARD

**Score:** [X]/[max]
**Change:** [one targeted mutation]
**Hypothesis:** [why it should help]
**Result:** [what changed]
**Regression check:** [what was preserved or harmed]
**Remaining failures:** [if any]
```

A machine-readable results file may also be maintained when useful, but it is optional and should not add unnecessary infrastructure.

## Promotion

An improved version should remain separate from the original until its results have been reviewed.

Promotion criteria:
- measurable improvement on representative evals;
- no material regression on strategic/evidence guardrails;
- failure modes documented;
- change is understandable and maintainable.

Only then replace or merge into the production skill according to the user's repository workflow.

## Final Quality Gate

Before promoting a mutation:
- [ ] It improves the actual skill job, not just the eval score.
- [ ] It preserves strategic decision boundaries.
- [ ] It preserves evidence discipline.
- [ ] It does not introduce fabricated claims or universal rules.
- [ ] It generalizes beyond a single test case.
- [ ] The change is smaller/simpler where equally effective.
- [ ] Results and remaining limitations are documented.
