# Strategic Marketing OS — Trial Readiness Gate

## Purpose

This gate marks the point where the repository should stop expanding its architecture and start learning from real business cases.

The repository is **trial-ready** when the operating system can consistently behave as an evidence-driven strategic consultant and the remaining issues are ordinary model/performance refinements rather than missing architecture.

## Release Criteria

### 1. Strategic Diagnosis

- Broad, ambiguous, audit, planning, growth, SPV, and decision requests enter `strategic-intelligence` first.
- The system identifies the business outcome and decision.
- Symptoms are separated from candidate root causes.
- Alternatives and disconfirming evidence are considered when material.

### 2. Evidence & Research

- Current or externally verifiable claims are researched when required.
- Facts, observations, inferences, hypotheses, benchmarks, and recommendations remain distinguishable.
- Missing evidence is surfaced rather than invented.
- Research is proportional to the decision and has a stopping condition.

### 3. Strategic Completeness

When material to the decision, the analysis considers:

- business model and commercial economics;
- customer and market dynamics;
- competition and alternatives;
- offer, pricing, packaging, and value;
- brand and positioning;
- customer journey, funnel, and sales;
- channel/media fit and economics;
- operational capability and constraints;
- external/regulatory risk;
- measurement feasibility.

### 4. Specialist Routing

- Only the minimum necessary specialists are invoked.
- Specialist playbooks do not override the strategic diagnosis.
- Structured handoffs preserve objective, decision, evidence, assumptions, priorities, job-to-be-done, and measurement intent.
- New material evidence returns to Strategic Intelligence.

### 5. Measurement & Learning

- Recommendations connect to business outcomes or justified leading indicators.
- Attribution and causality limitations are visible.
- Results are interpreted as evidence, not automatically as proof.
- Material learning can update the strategic diagnosis.

### 6. Regression Cases

The evaluation suite in `examples/evaluations/strategic-intelligence-eval-suite.md` should be used for manual model evaluation and regression testing.

A response fails when it:

- converts a user-mentioned tactic into the diagnosis;
- treats a benchmark as a universal law;
- claims a channel is best without evidence;
- invents metrics, market facts, customer evidence, or business outcomes;
- confuses correlation with causation;
- ignores economics/capability/risk when material;
- routes every request through every specialist;
- ends with activity rather than a decision/test/investigation.

## Static Audit Status

The repository has been statically reviewed for the major architecture conflicts identified during the modernization pass, including:

- legacy linear routing;
- duplicate `.claude` vs `.agents` strategic logic;
- unsupported benchmark/threshold defaults;
- specialist decision-boundary violations;
- weak customer/VOC evidence handling;
- missing measurement/learning feedback;
- stale knowledge treated as current fact.

Static review is **not** the same as executing the prompts with a model. Model-behavior validation still requires running the regression cases in an actual model environment.

## Freeze Rule

After this gate is accepted, do **not** add new strategic skills merely for completeness.

Only make architectural changes when a real trial case demonstrates a repeatable failure such as:

- wrong diagnosis;
- missing research dimension;
- bad specialist routing;
- evidence hallucination;
- broken handoff;
- incorrect measurement logic;
- material business-domain blind spot.

The default mode is now:

`TRIAL → OBSERVE FAILURE → PATCH → REGRESSION TEST → CONTINUE`

not:

`ADD MORE SKILLS → ADD MORE RULES → ADD MORE SKILLS`
