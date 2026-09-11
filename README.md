# 🚀 Marketing Branding Selling Ads Skills — Strategic Marketing AI OS

> **Evidence-driven AI Strategic Marketing OS** untuk membantu diagnosis bisnis, riset market/customer/competitor, branding, marketing, selling, paid acquisition, execution, measurement, dan learning.

Repositori ini bukan sekadar kumpulan prompt. Arsitekturnya menempatkan **Strategic Intelligence** sebagai decision layer, specialist skills sebagai domain executors, dan measurement/learning sebagai feedback loop.

---

## 🧠 Core Architecture

```text
Business Problem / Goal
        ↓
Orchestrator
        ↓
Strategic Intelligence
        ↓
Research + Evidence
        ↓
Diagnosis + Priorities + Decisions
        ↓
Structured Handoff
        ↓
Selected Specialist Skills
        ↓
Execution / QA
        ↓
Measurement
        ↓
Learning
        ↓
Strategic Intelligence when the diagnosis changes
```

### Prinsip utama

- **Strategic Intelligence First** untuk request yang broad, ambigu, lintas fungsi, audit, planning, growth, business, branding, marketing, sales, channel/media, atau SPV-level.
- **Research before unsupported conclusions.** Channel, audience, competitor behavior, pricing, positioning, dan benchmark tidak boleh diasumsikan hanya karena populer.
- **Minimum necessary specialists.** Tidak semua skill dipanggil dalam setiap task.
- **Specialist ≠ Strategy Owner.** Specialist mengerjakan domain job-to-be-done dalam batas diagnosis.
- **Evidence ≠ certainty.** FACT, OBSERVATION, INFERENCE, HYPOTHESIS, BENCHMARK, dan RECOMMENDATION harus tetap dibedakan.
- **Learning feeds strategy.** Hasil campaign, ads, sales, win/loss, QA, dan eksperimen dapat mengubah diagnosis.

---

## 🏛️ Framework Foundations

Repositori ini mengkurasi dan mengintegrasikan berbagai pendekatan marketing dan product marketing, termasuk:

1. **ericosiu/marketing-os-starter** — fondasi multi-agent marketing OS, orchestration, memory, dan handoff.
2. **pmalliance/product-marketing-skills** — product marketing, positioning *Obviously Awesome*, STP, GTM, VOC, competitive intelligence, dan pricing/packaging.
3. **j1ngg/tech-marketing-framework** — content, SEO/AEO, paid media, sales enablement, launch workflows, dan autoresearch.
4. **Custom governance layer** — strategic diagnosis, evidence discipline, structured handoffs, specialist boundaries, measurement/causality guardrails, dan feedback loops.

Framework dipakai sebagai **alat berpikir**, bukan sebagai formula universal yang harus selalu diterapkan.

---

## 📑 Skill Domains

### 🎨 1. Branding & Positioning
| Skill | Deskripsi |
| :--- | :--- |
| **messaging-positioning** | Positioning & messaging berbasis *Obviously Awesome* dengan evidence dan validation. |
| **messaging-positioning-workshop** | Workshop terstruktur untuk merumuskan positioning/differentiation. |
| **positioning-map** | Competitive positioning visualization dan whitespace analysis berbasis evidence. |
| **brand-voice** | Voice, tone, vocabulary, dan brand communication guidance. |
| **customer-language-bank** | Ekstraksi bahasa customer/VOC dari sumber yang tersedia. |
| **claim-check** | Verifikasi klaim, proof, dan traceability. |
| **message-consistency-check** | QA alignment pesan antar-surface dan journey stage. |
| **how-they-market** | Competitive marketing intelligence dan channel/funnel observation. |

### 🚀 2. Marketing Strategy & Growth
| Skill | Deskripsi |
| :--- | :--- |
| **go-to-market** | GTM architecture, market entry/expansion, offer/channel alignment. |
| **campaign-brief** | Structured campaign/creative brief setelah strategic direction tersedia. |
| **customer-research** | Customer/JTBD research dan synthesis. |
| **competitive-intelligence** | Competitive offers, positioning, proof, distribution, dan battlecard intelligence. |
| **win-loss-reasons** | Synthesis bukti deal won/lost/no-decision. |
| **editorial-calendar** | Content planning berdasarkan objective, audience, role, dan capacity. |
| **producthunt-launch** | Product Hunt launch execution guidance; taktik dan timing tetap context-dependent. |
| **viral-launch-playbook** | Launch/experiment ideas untuk referral, distribution, dan attention; bukan jaminan virality. |
| **launch-roundup** | Rilis fitur menjadi paket komunikasi/distribution assets. |
| **autoresearch** | Controlled skill/prompt experimentation dan learning loop. |

### ✍️ 3. Content & Conversion
| Skill | Deskripsi |
| :--- | :--- |
| **copywriting** | Conversion copy execution berbasis strategi, offer, audience, dan evidence. |
| **blog** | Long-form SEO/AEO content dengan research dan claim discipline. |
| **social-posts** | Platform-specific social copy. |
| **social-content** | Social content planning/generation yang terikat pada strategic objective. |
| **email** | Newsletter/editorial/product communication. |
| **email-sequence** | Lifecycle/nurture/sales sequence berdasarkan journey dan objective. |
| **image** | Visual prompt/asset specifications untuk kebutuhan komunikasi. |

### 💼 4. Selling, Paid Acquisition & QA
| Skill | Deskripsi |
| :--- | :--- |
| **multi-platform-ads-automation** | Paid-media planning/validation/automation framework dengan platform-specific guardrails. |
| **ads** | Paid ad creative execution untuk platform yang relevan. |
| **ads-auditor** | Paid-media performance audit, funnel diagnosis, dan optimization recommendations. |
| **sales-deck** | B2B sales narrative dan deck structure. |
| **objection-library** | Evidence-based objection analysis dan handling support. |
| **pricing-packaging** | Pricing, packaging, value metric, dan monetization analysis. |
| **asset-reviewer** | Evidence/message/brand/conversion QA sebelum publikasi atau eksekusi. |
| **skill-builder** | Meta-skill untuk membuat dan menguji skill AI baru. |

---

## 🤖 Agent Architecture

### `mos-orchestrator`
Menilai work level, menentukan routing, menjaga handoff, dan memilih specialist minimum yang diperlukan.

### `mos-researcher`
Mengumpulkan evidence untuk market, customer, competitor, channel/media, VOC, dan conversion. Kesimpulan strategis final bukan kewenangannya. 

### `mos-strategist`
Mengubah diagnosis/evidence menjadi strategic priorities, GTM, positioning, messaging, offer, channel, campaign, dan execution direction sesuai kebutuhan.

### `mos-copywriter`
Menerjemahkan strategi dan source material menjadi copy/content assets.

### `ads-auditor`
Menganalisis paid-media performance dan mengeskalasi masalah upstream ketika akar masalah ternyata bukan iklan.

### `asset-reviewer`
Menjadi quality gate untuk evidence, positioning/message fit, brand, conversion friction, dan compliance.

---

## 🔗 Structured Handoff

Broad strategic requests menghasilkan `schemas/strategic-diagnosis.json.template` sebagai machine-readable contract.

Handoff membawa:

- business objective dan decision;
- known / unknown / assumptions;
- evidence dan research gaps;
- diagnosis, bottlenecks, tensions, opportunities;
- customer/market implications;
- competitive context;
- channel/media role;
- priorities;
- specialist workstreams dan **job-to-be-done**;
- measurement logic;
- handoff controls.

Lifecycle diagnosis:

`draft → researching → diagnosed → ready_for_handoff → superseded`

Specialist tidak boleh diam-diam mengganti diagnosis. Jika evidence baru mengubah strategic conclusion, temuan dikembalikan ke Strategic Intelligence.

---

## ⚙️ Governance Layer

Cross-cutting rules berada di `.agents/rules/` dan berfungsi sebagai **reasoning constraints**:

- strategic routing & specialist decision boundary;
- customer evidence / VOC;
- positioning, claims & message consistency;
- brand voice / positioning;
- content planning;
- sales & conversion;
- measurement, attribution, experimentation & learning.

Tujuannya menghindari pola seperti:

> “CTR turun → ganti creative.”

ketika masalah sebenarnya mungkin offer, audience, positioning, landing page, sales follow-up, measurement, atau channel fit.

---

## 🛠️ Usage

### Google Antigravity / Claude Code / Codex

Gunakan repository sebagai context dan skill library. Untuk request strategis, mulai dari Strategic Intelligence; untuk request narrow dengan direction yang sudah jelas, direct specialist execution tetap diperbolehkan.

Contoh:

```text
/strategic-intelligence
/messaging-positioning
/customer-research
/go-to-market
/ads
/ads-auditor
/sales-deck
```

---

## 📁 Repository Structure

```text
├── .agents/
│   ├── rules/                 # Shared reasoning constraints
│   ├── skills/                # Domain skills (SKILL.md)
│   └── product-marketing-context.md
├── .claude/
│   ├── agents/                # Claude agent definitions
│   ├── rules/                 # Claude-specific guidance
│   └── skills/                # Claude skill collection
├── agents/                    # Named specialist agent definitions
├── brands/                    # Brand context/templates
├── docs/                      # Product/brand/persona inputs
├── memory/                    # Persistent marketing memory
├── schemas/                   # Structured handoff templates
├── examples/                  # Examples and evaluations
├── AGENTS.md                  # Agent architecture and routing contract
├── CLAUDE.md                  # Master operating rules
└── README.md                  # Repository documentation
```

---

## 📄 License & Credits

Repositori ini dikurasi dan dikembangkan oleh **nugiwabot**. Fondasi awal dan metodologi yang dirujuk antara lain:

- **Eric Siu** — [marketing-os-starter](https://github.com/ericosiu/marketing-os-starter)
- **Product Marketing Alliance** — [product-marketing-skills](https://github.com/pmalliance/product-marketing-skills)
- **Jing / Tech Marketing Engine** — [tech-marketing-framework](https://github.com/j1ngg/tech-marketing-framework)

Framework dan sumber tetap tunduk pada lisensi, attribution, dan penggunaan yang berlaku dari sumber aslinya.
