# Strategic Intelligence Evaluation Suite

## Purpose

This suite tests whether the Marketing AI OS behaves like an evidence-driven strategic consultant rather than a tactic generator.

Use these cases for manual evaluation, model comparison, regression testing, and `autoresearch`.

## Universal Pass Criteria

A strong response should, where relevant:

1. Identify the business outcome and decision.
2. Separate symptoms from root-cause hypotheses.
3. Distinguish FACT, OBSERVATION, INFERENCE, HYPOTHESIS, BENCHMARK, and RECOMMENDATION.
4. Research current or externally verifiable facts rather than inventing them.
5. Consider customer, market, competitor, offer, economics, channel, funnel, capability, and risk dimensions when material.
6. Select frameworks because they answer the decision question.
7. Evaluate channels/media using audience, intent, economics, funnel role, measurement, operational feasibility, and competitive context.
8. Present alternatives and trade-offs.
9. State confidence, unknowns, and disconfirming evidence where material.
10. Route only the minimum necessary specialists.
11. Produce a decision, test, investigation, delay, stop, or strategic-change recommendation rather than merely more activity.
12. Preserve a clear path from evidence → diagnosis → decision → action → measurement → learning.

## Scoring Rubric

Score each dimension 0–2:

| Dimension | 0 | 1 | 2 |
|---|---|---|---|
| Outcome/decision clarity | Missing | Partly inferred | Explicit and decision-focused |
| Evidence discipline | Hallucinates/confuses evidence | Mostly separated | Consistently traceable and calibrated |
| Root-cause quality | Tactic/symptom only | Some alternatives | Clear diagnosis with competing hypotheses |
| Research design | No research or random research | Some relevant research | Decision-oriented and proportionate |
| Strategic completeness | Marketing-only | Some business context | Material business system considered |
| Framework selection | Framework dumping | Partly relevant | Minimum sufficient, purpose-driven |
| Channel/media analysis | Popularity/assumption | Some fit analysis | Evidence + economics + operational fit |
| Commercial/economic reasoning | Ignored | Mentioned | Explicit and assumption-aware |
| Alternatives/trade-offs | One answer | Alternatives listed | Choices, trade-offs, and dependencies clear |
| Specialist routing | Over-routed | Mostly relevant | Minimum sufficient routing |
| Measurement/learning | Vanity KPI | Some measurement | Outcome-linked feedback loop |

Suggested interpretation:

- **20–22:** strong strategic behavior
- **16–19:** useful but needs review
- **12–15:** tactical/partial strategist
- **<12:** fails strategic-intelligence objective

The ranges are evaluation guidance, not scientific thresholds.

---

## Case 01 — Tactic-Framed Business Problem

### Prompt

> "Bisnis saya sepi. Tolong buatkan Instagram, Meta Ads, dan konten 30 hari supaya penjualan naik."

### Expected behavior

The model should not immediately produce 30 days of content and an ads plan.

It should determine what "sepi" means, identify the sales objective, inspect demand, audience, offer, pricing, location/channel fit, sales process, and current baseline where available, then decide whether Instagram/Meta/content is actually relevant.

### Fail conditions

- Automatically produces a content calendar.
- Declares Meta the best channel without evidence.
- Invents target CPL/ROAS/CVR.
- Assumes low sales = low awareness.

---

## Case 02 — Channel Selection

### Prompt

> "Saya punya produk B2C di Indonesia. Lebih bagus Instagram, TikTok, Google, atau WhatsApp?"

### Expected behavior

The model should ask or infer the buying decision, product category, purchase intent, customer journey, economics, geography, and conversion mechanism before ranking channels.

It should compare channels by role rather than popularity and may recommend different roles for discovery, demand capture, conversion, and retention.

### Fail conditions

- "TikTok is best in 2026" without research.
- One universal channel recommendation.
- Ranking channels without considering margins or conversion path.

---

## Case 03 — Expensive Leads

### Prompt

> "CPL kami naik 70%. Solusinya ganti creative dan interest targeting, kan?"

### Expected behavior

Treat creative and targeting as hypotheses, not conclusions. Investigate auction/media changes, audience mix, offer, message, landing/inquiry experience, tracking, qualification, downstream sales conversion, and customer value.

### Fail conditions

- Immediately recommends new creative.
- Treats CPL as the business outcome.
- Claims a specific fix will reduce CPL without evidence.

---

## Case 04 — Competitor Copying

### Prompt

> "Competitor kami aktif di TikTok dan posting 5 kali seminggu. Kita harus meniru."

### Expected behavior

Separate observed competitor activity from effectiveness. Research the competitor's audience, content role, engagement/customer evidence where available, commercial role, and alternative channels. Recommend copying only mechanisms that plausibly fit the user's context.

### Fail conditions

- Assumes frequency causes growth.
- Assumes competitor channel = optimal channel.
- Labels competitor tactic as proven best practice without evidence.

---

## Case 05 — Low Closing Rate

### Prompt

> "Lead banyak tapi closing rendah. Buatkan sales script baru."

### Expected behavior

Examine lead quality, qualification, offer, positioning, trust/proof, pricing, follow-up, discovery, proposal, objections, customer fit, and stage definitions before deciding whether a script is the bottleneck.

### Fail conditions

- Script automatically becomes the solution.
- Blames salesperson performance without process evidence.
- Ignores lead quality or offer fit.

---

## Case 06 — Pricing Decision

### Prompt

> "Harga produk kami sebaiknya dinaikkan 20% supaya margin lebih besar."

### Expected behavior

Consider value perception, willingness-to-pay evidence, elasticity, segment differences, competitor alternatives, margin structure, volume effects, retention risk, and possible packaging alternatives. Use scenarios where data is incomplete.

### Fail conditions

- Recommends 20% increase as fact.
- Uses competitor price alone as proof.
- Ignores demand/volume and customer-value implications.

---

## Case 07 — Brand Positioning

### Prompt

> "Brand kita kurang premium. Buatkan tone yang lebih mewah."

### Expected behavior

Test whether the underlying issue is positioning, offer, proof, customer experience, pricing, visual identity, or voice before prescribing a tone change.

### Fail conditions

- Treats premium tone as a complete strategy.
- Writes copy before diagnosis.
- Assumes premium = formal language.

---

## Case 08 — New Market Entry

### Prompt

> "Kami mau ekspansi ke kota baru bulan depan. Buatkan campaign launch."

### Expected behavior

Assess market attractiveness, customer fit, competitive structure, local demand, distribution, economics, operational readiness, regulation where relevant, and entry alternatives before approving a launch campaign.

### Fail conditions

- Jumps directly into launch assets.
- Assumes existing positioning transfers unchanged.
- Ignores supply/operations and local economics.

---

## Case 09 — Retention Problem

### Prompt

> "Churn naik. Kirim email win-back ke semua customer."

### Expected behavior

Investigate churn definition, cohort/segment differences, product/service experience, onboarding, customer success, pricing, competitive switching, customer-fit issues, and whether win-back is suitable for all segments.

### Fail conditions

- Sends one universal win-back sequence.
- Treats email as the root-cause fix.
- Ignores product/service causes.

---

## Case 10 — SPV Prioritization

### Prompt

> "Saya SPV marketing dengan tim kecil. Mana yang harus dikerjakan dulu: website, Instagram, Meta Ads, SEO, CRM, sales training, atau rebranding?"

### Expected behavior

Build a prioritization decision using business objective, current bottleneck, impact, evidence, feasibility, dependencies, economics, time-to-value, reversibility, and team capacity.

The correct answer may be to do fewer items or investigate first.

### Fail conditions

- Gives a generic checklist.
- Says "do all channels but prioritize consistency."
- Uses popularity rather than bottleneck/evidence.

---

## Case 11 — Missing Data

### Prompt

> "Tolong hitung apakah campaign ini profitable."

### Expected behavior

Identify required inputs such as spend, attributable revenue, margin/contribution basis, conversion events, time window, and attribution assumptions. Show the calculation logic and indicate what is unknown instead of fabricating the result.

### Fail conditions

- Invents missing revenue/margin/CAC.
- Uses ROAS alone to declare profitability when margin is unknown.

---

## Case 12 — Conflicting Evidence

### Prompt

> "Customer bilang mahal, tapi survey bilang harga sudah oke. Jadi sebenarnya siapa yang benar?"

### Expected behavior

Preserve the conflict. Examine sample, segment, context, question wording, purchase stage, actual behavior, and transaction evidence. Explain which evidence is stronger for the decision and what test could resolve uncertainty.

### Fail conditions

- Chooses one source automatically.
- Calls the survey or customer quote "truth" without context.
- Hides the conflict.

---

## Regression Test: Strategic Boundary

For each case, verify the response does **not**:

- turn a user-mentioned tactic into the diagnosis;
- treat benchmark numbers as universal laws;
- route every task through every specialist;
- confuse observation with causality;
- overstate certainty;
- omit meaningful business/economic constraints;
- end with activity instead of a decision.

## Regression Test: Strategic Synthesis

A passing answer should make it possible to trace:

`Problem → Decision → Evidence → Diagnosis → Alternatives → Strategic Choice → Specialist Work → Action → Measurement → Learning`

without hidden leaps.
