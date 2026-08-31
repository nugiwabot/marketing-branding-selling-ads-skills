---
name: multi-platform-ads-automation
description: |
  Operational brain for AI Agent to plan, validate, and automate ad campaigns
  across Google Ads, Meta Ads, TikTok Ads, and LinkedIn Ads via MCP or REST APIs.
  Includes 2026 algorithmic intelligence, technical constraint matrices,
  policy compliance guardrails, and pre-flight validation logic.
version: "2026.08"
author: Senior Growth Engineer & Ad Automation Architect
platforms:
  - google-ads
  - meta-ads
  - tiktok-ads
  - linkedin-ads
---

# Multi-Platform Ad Campaign Automation — SKILL.md

> **Revision:** 2026-08-31  
> **API Versions:** Google Ads API v19, Meta Marketing API v22.0, TikTok Business API v1.3, LinkedIn Marketing API v202608  
> **Compliance Baseline:** GDPR, CCPA, DMA, DSA, ePrivacy Directive

---

## Table of Contents

1. [2026 Algorithmic Intelligence & Strategy](#1-2026-algorithmic-intelligence--strategy)
2. [Technical Constraint Matrix](#2-technical-constraint-matrix)
3. [Policy & Compliance Guardrails](#3-policy--compliance-guardrails)
4. [Pre-Flight Validation Logic](#4-pre-flight-validation-logic)
5. [API Authentication & Token Matrix](#5-api-authentication--token-matrix)
6. [UTM & Tracking Standards](#6-utm--tracking-standards)
7. [Official Reference Sources](#7-official-reference-sources)
8. [MCP (Model Context Protocol) Integration](#8-mcp-model-context-protocol-integration)
9. [Bidding Strategy Decision Trees](#9-bidding-strategy-decision-trees)
10. [Budget Allocation Logic](#10-budget-allocation-logic)
11. [A/B Testing Framework](#11-ab-testing-framework)
12. [Performance Benchmarks & KPI Thresholds](#12-performance-benchmarks--kpi-thresholds)
13. [Retargeting & Remarketing Funnel Logic](#13-retargeting--remarketing-funnel-logic)
14. [API Rate Limits](#14-api-rate-limits)
15. [Error Handling & Retry Logic](#15-error-handling--retry-logic)
16. [Cross-Platform Reporting Schema](#16-cross-platform-reporting-schema)

---

## 1. 2026 Algorithmic Intelligence & Strategy

### 1.1 Google Ads — Performance Max & Demand Gen

#### Decision Framework

```
IF campaign_objective IN [sales, leads, store_visits]:
    USE campaign_type = PERFORMANCE_MAX
    SET bidding_strategy = VALUE_BASED  # tROAS or tCPA
    REQUIRE asset_strength >= "GOOD"    # REJECT if "POOR" or "AVERAGE"
    ENABLE url_expansion = TRUE
    ENABLE final_url_expansion = TRUE
    SET audience_signal = FIRST_PARTY_DATA + CUSTOM_SEGMENTS

IF campaign_objective IN [awareness, consideration, demand_generation]:
    USE campaign_type = DEMAND_GEN
    REQUIRE creative_formats = [IMAGE, VIDEO, CAROUSEL]
    SET audience = LOOKALIKE(seed=first_party_data, expansion=NARROW)
    ENABLE optimized_targeting = TRUE
```

#### Value-Based Bidding (VBB) Rules

| Parameter | Constraint | Action on Violation |
|---|---|---|
| `target_roas` | Min 100%, recommended 200–800% | WARN if < 150%, FAIL if < 100% |
| `target_cpa` | Must be ≥ 50% of avg. historical CPA | FAIL if set below floor |
| `conversion_action` | Must have ≥ 30 conversions in last 30 days | WARN, recommend MAXIMIZE_CONVERSIONS first |
| `conversion_value` | Must import revenue values via offline conversion import or GA4 | FAIL if no value signal |

#### Asset Strength Scoring — Mandatory Checks

- [ ] Minimum 8 Headlines provided (recommend 15)
- [ ] Minimum 3 Descriptions provided (recommend 4)
- [ ] At least 1 Landscape Image (1200×628)
- [ ] At least 1 Square Image (1200×1200)
- [ ] At least 1 Portrait Image (960×1200)
- [ ] At least 1 Video asset (landscape or square, ≥ 10 sec)
- [ ] At least 1 Logo (1200×1200)
- [ ] Business Name provided
- [ ] Long Headline provided
- [ ] Asset Strength API response ∈ {`GOOD`, `EXCELLENT`} → PASS; else → FAIL

#### Consent Mode v2 & 1st-Party Data

```
REQUIRE consent_mode_v2 = ENABLED
REQUIRE consent_signals:
  - ad_storage: GRANTED | DENIED
  - analytics_storage: GRANTED | DENIED  
  - ad_user_data: GRANTED | DENIED       # MANDATORY for EEA
  - ad_personalization: GRANTED | DENIED  # MANDATORY for EEA

IF target_region IN [EEA, UK, CH]:
    REQUIRE enhanced_conversions = TRUE
    REQUIRE customer_match.consent = EXPLICIT_OPT_IN
    VALIDATE data_processing_terms = SIGNED
```

---

### 1.2 Meta Ads — Advantage+ Ecosystem

#### Decision Framework

```
IF campaign_objective == SALES AND product_catalog_available:
    USE campaign_type = ADVANTAGE_PLUS_SHOPPING
    SET budget_optimization = CAMPAIGN_LEVEL (CBO)
    SET creative_optimization = ADVANTAGE_PLUS_CREATIVE
    SET audience = ADVANTAGE_PLUS_AUDIENCE  # Broad, AI-driven
    DISABLE manual_audience_exclusions      # Let Meta AI optimize
    SET country_targeting = [target_countries]  # Only geo restriction

IF campaign_objective IN [leads, traffic, awareness]:
    USE campaign_type = STANDARD
    ENABLE advantage_plus_audience = TRUE
    ENABLE advantage_plus_creative = TRUE
    SET original_audience_as_suggestion = TRUE  # Not hard constraint

IF creative_count >= 5:
    ENABLE dynamic_creative = TRUE
    # "Creative is Targeting" — minimize manual segmentation
```

#### "Creative is Targeting" Principles

| Principle | Implementation |
|---|---|
| Volume over precision | Supply ≥ 5 creative variations per ad set |
| Format diversity | Mix static image + video + carousel per ad set |
| Audience breadth | Use Advantage+ Audience (broad) — avoid hyper-segmentation |
| Creative rotation | Let Meta AI select winning creative; do NOT manually pick |
| Testing framework | Use A/B Test tool for creative concepts, not manual splits |
| Refresh cadence | Replace bottom 20% creatives every 7–14 days |

#### Conversions API (CAPI) Requirements

```json
{
  "capi_requirements": {
    "server_events_required": true,
    "event_match_quality_minimum": 6.0,
    "deduplication": {
      "method": "event_id + event_name",
      "pixel_and_capi": "BOTH_REQUIRED"
    },
    "mandatory_parameters": [
      "event_name",
      "event_time",
      "action_source",
      "event_source_url",
      "user_data.em",
      "user_data.ph"
    ],
    "recommended_parameters": [
      "user_data.fn",
      "user_data.ln",
      "user_data.ct",
      "user_data.st",
      "user_data.zp",
      "user_data.country",
      "user_data.external_id",
      "user_data.fbc",
      "user_data.fbp"
    ],
    "hashing": "SHA-256 lowercase, trimmed, no spaces"
  }
}
```

---

### 1.3 TikTok Ads — Smart+ & Creative AI

#### Decision Framework

```
IF campaign_objective IN [website_conversions, app_installs, product_sales]:
    USE campaign_type = SMART_PLUS
    SET automation_level = FULL
    # Smart+ automates: targeting, bidding, creative selection
    PROVIDE creative_assets >= 5 videos
    SET budget_type = DAILY | LIFETIME
    SET optimization_goal = VALUE | CONVERSION | CLICK

IF campaign_type == SMART_PLUS:
    DISABLE manual_targeting     # AI handles audience
    DISABLE manual_bidding       # AI handles bid
    ENABLE creative_rotation = AUTO
```

#### Creative Fatigue Mitigation

```
MONITOR creative_metrics:
  IF ctr_decline >= 20% over 3_days:
      FLAG creative_fatigue = TRUE
      ACTION: Rotate new creative variant
  
  IF frequency >= 4.0:
      FLAG audience_saturation = TRUE
      ACTION: Expand audience OR refresh creative

  IF hook_rate_3sec < 25%:
      FLAG weak_hook = TRUE
      ACTION: Regenerate first 3 seconds
      RECOMMEND: Text overlay hook, movement in frame 1
```

#### 3-Second Hook Rate Optimization

| Hook Strategy | Implementation |
|---|---|
| Text-first hook | Large text overlay in first 0.5 sec |
| Motion hook | Camera movement / zoom in first 1 sec |
| Pattern interrupt | Unexpected visual/audio in first 0.3 sec |
| Question hook | On-screen question addressing pain point |
| UGC-style opener | "POV" or "Wait for it" native format |
| Minimum hook rate target | ≥ 30% (3-sec view / impression) |

#### TikTok Symphony AI Guidelines

- [ ] Use TikTok Symphony for AI-generated script variations
- [ ] Avatar videos must disclose AI generation
- [ ] AI-generated voices must match brand tone guidelines
- [ ] Symphony Creative Studio outputs must pass creative review
- [ ] Respect content originality — no cloning of existing creator content

---

### 1.4 LinkedIn Ads — B2B Predictive & ABM

#### Decision Framework

```
IF campaign_objective == LEAD_GENERATION:
    USE objective = LEAD_GEN_FORMS
    SET audience_type = PREDICTIVE_AUDIENCE
    SEED predictive_audience WITH:
      - contact_list (min 300 members)
      - OR conversion_data (last 90 days)
      - OR lookalike_source = website_visitors
    SET bid_strategy = MAXIMUM_DELIVERY | TARGET_COST

IF campaign_objective == ACCOUNT_BASED_MARKETING:
    USE targeting = COMPANY_LIST_UPLOAD
    REQUIRE company_list.size >= 300
    LAYER with:
      - job_function
      - seniority (Director+, VP+, C-Suite)
      - job_title (keyword matching)
    SET content_type = THOUGHT_LEADERSHIP | CASE_STUDY
```

#### Predictive Audiences Rules

| Parameter | Constraint |
|---|---|
| Seed list minimum | 300 contacts or company matches |
| Data freshness | Seed data ≤ 90 days old |
| Lookalike expansion | NARROW (1–3%) for quality, BROAD (4–10%) for reach |
| Exclusion lists | Always exclude current customers + competitors |
| Refresh cadence | Re-seed predictive audience every 30 days |

#### Buying Committee Attribution

```
DEFINE buying_committee_roles:
  - CHAMPION: Job functions = [Marketing, Product, Engineering]
  - DECISION_MAKER: Seniority = [Director, VP, C-Suite]
  - INFLUENCER: Seniority = [Manager, Senior]
  - END_USER: Seniority = [Entry, Senior]

ATTRIBUTION_MODEL:
  - Track engagement across ALL committee roles
  - Weight DECISION_MAKER interactions 3x
  - Weight CHAMPION interactions 2x
  - Minimum 2 unique committee roles engaged = QUALIFIED_ACCOUNT
  - Report at ACCOUNT level, not individual lead level
```

---

## 2. Technical Constraint Matrix

### 2.1 Google Ads — Search & Performance Max

| Element | Min | Max | Optimal | Validation Rule |
|---|---|---|---|---|
| **RSA Headlines** | 3 | 15 | 10–15 | `3 ≤ count ≤ 15` |
| RSA Headline length | 1 char | 30 chars | 25–30 chars | `len(headline) ≤ 30` |
| **RSA Descriptions** | 2 | 4 | 4 | `2 ≤ count ≤ 4` |
| RSA Description length | 1 char | 90 chars | 60–90 chars | `len(desc) ≤ 90` |
| Path URL 1 | — | 15 chars | 10–15 chars | `len(path1) ≤ 15` |
| Path URL 2 | — | 15 chars | 10–15 chars | `len(path2) ≤ 15` |
| Final URL | — | 2048 chars | — | `is_https(url) AND is_valid_url(url)` |
| Display URL | — | 35 chars | — | Auto-generated from Final URL |
| **PMax Headlines** | 3 | 15 | 8–15 | `3 ≤ count ≤ 15` |
| PMax Long Headline | 1 | 90 chars | 60–90 chars | `len(long_headline) ≤ 90` |
| PMax Descriptions | 2 | 5 | 4–5 | `2 ≤ count ≤ 5` |
| PMax Description length | 1 | 90 chars | — | `len(desc) ≤ 90` |
| PMax Business Name | 1 | 25 chars | — | `len(biz_name) ≤ 25` |
| Callout Extensions | — | 25 chars each | 12–15 chars | `len(callout) ≤ 25` |
| Sitelink Title | — | 25 chars | — | `len(sitelink_title) ≤ 25` |
| Sitelink Description | — | 35 chars each (2 lines) | — | `len(desc_line) ≤ 35` |
| Structured Snippets | — | 25 chars per value | — | `len(value) ≤ 25` |
| WhatsApp Message Trigger | — | 140 chars | < 100 chars | `len(trigger_text) < 140` |

#### Image Asset Specifications

| Asset Type | Dimensions | Aspect Ratio | Max File Size | Format |
|---|---|---|---|---|
| Landscape | 1200×628 | 1.91:1 | 5120 KB | JPG, PNG |
| Square | 1200×1200 | 1:1 | 5120 KB | JPG, PNG |
| Portrait | 960×1200 | 4:5 | 5120 KB | JPG, PNG |
| Logo (square) | 1200×1200 | 1:1 | 5120 KB | PNG (transparent bg) |
| Logo (landscape) | 1200×300 | 4:1 | 5120 KB | PNG (transparent bg) |

---

### 2.2 Meta Ads

| Element | Max Length | Optimal | Validation Rule |
|---|---|---|---|
| **Primary Text** | 2200 chars (hard) | ≤ 125 chars (before truncation) | `len(primary_text) ≤ 2200; WARN if > 125` |
| **Headline** | 255 chars (hard) | ≤ 40 chars | `len(headline) ≤ 255; WARN if > 40` |
| **Link Description** | 255 chars (hard) | ≤ 30 chars | `len(link_desc) ≤ 255; WARN if > 30` |
| CTA Button | Predefined list only | — | `cta IN ALLOWED_CTA_LIST` |
| URL Parameters | — | — | `is_https(url)` |
| Ad Name | 255 chars | — | `len(ad_name) ≤ 255` |

#### Media Specifications

| Placement | Aspect Ratio | Resolution (min) | Video Duration | File Size |
|---|---|---|---|---|
| Feed (Image) | 1:1 | 1080×1080 | — | ≤ 30 MB |
| Feed (Video) | 1:1 or 4:5 | 1080×1080 | 1–240 sec | ≤ 4 GB |
| Stories / Reels | 9:16 | 1080×1920 | 1–60 sec (Reels: 3–90 sec) | ≤ 4 GB |
| In-stream Video | 16:9 | 1280×720 | 5–15 sec (mid-roll: 5–600 sec) | ≤ 4 GB |
| Carousel (Image) | 1:1 | 1080×1080 | — | ≤ 30 MB per card |
| Carousel (Video) | 1:1 | 1080×1080 | 1–240 sec | ≤ 4 GB per card |
| Carousel Cards | 2–10 cards | — | — | — |
| Right Column | 1.91:1 | 1200×628 | — | ≤ 30 MB |

#### Allowed CTA Buttons

```json
[
  "APPLY_NOW", "BOOK_NOW", "CONTACT_US", "DOWNLOAD",
  "GET_OFFER", "GET_QUOTE", "GET_SHOWTIMES", "LEARN_MORE",
  "LISTEN_NOW", "ORDER_NOW", "PLAY_GAME", "REQUEST_TIME",
  "SEE_MENU", "SHOP_NOW", "SIGN_UP", "SUBSCRIBE",
  "WATCH_MORE", "SEND_WHATSAPP_MESSAGE", "GET_DIRECTIONS",
  "CALL_NOW", "SEND_MESSAGE", "OPEN_LINK"
]
```

---

### 2.3 TikTok Ads

| Element | Constraint | Validation Rule |
|---|---|---|
| **Ad Text** | 1–100 Latin chars (12–100 for CJK) | `1 ≤ len(ad_text) ≤ 100` |
| **App Name / Brand Name** | 2–40 chars | `2 ≤ len(brand_name) ≤ 40` |
| **Video Aspect Ratio** | 9:16 (vertical), 16:9 (landscape), 1:1 (square) | `aspect_ratio IN [9:16, 16:9, 1:1]` |
| Video Resolution | 540×960 (min) → 1080×1920 (recommended) | `width ≥ 540 AND height ≥ 960` |
| **Video Duration** | 5–60 sec | `5 ≤ duration_sec ≤ 60` |
| Optimal Duration | 9–15 sec | `WARN if duration < 9 OR duration > 15` |
| Video File Size | ≤ 500 MB | `file_size_mb ≤ 500` |
| Video Bitrate | ≥ 516 kbps (recommended ≥ 2500 kbps) | `bitrate_kbps ≥ 516` |
| Video Format | .mp4, .mov, .mpeg, .3gp, .avi | `format IN ALLOWED_FORMATS` |
| Image (Spark Ads) | 1200×628 (1.91:1) or 640×640 (1:1) | Size check |
| CTA Button | Predefined list | `cta IN TIKTOK_CTA_LIST` |
| Display URL | Optional, max 40 chars | `len(display_url) ≤ 40` |

#### Safe Zone Rules (CRITICAL)

```
┌─────────────────────────────────┐
│          TOP 15%                │  ← UI elements: profile, follow
│     NO text/CTA here           │
│                                 │
│                                 │
│     ████████████████            │  ← SAFE ZONE (center 50%)
│     █  MAIN CONTENT █           │     Place key visuals + text here
│     ████████████████            │
│                                 │
│                      ┌────┐     │
│                      │10% │     │  ← RIGHT 10%: interaction icons
│                      │    │     │     NO text/CTA here
│─────────────────────────────────│
│          BOTTOM 35%             │  ← UI elements: CTA bar, captions
│     NO key text here            │     Description overlay zone
└─────────────────────────────────┘

VALIDATION:
  - text_top_boundary > 15% from top
  - text_bottom_boundary < 65% from top (above bottom 35%)
  - text_right_boundary < 90% from left (avoid right 10%)
  - CTA_button_position: WITHIN safe zone
```

---

### 2.4 LinkedIn Ads

| Element | Max Length | Optimal | Validation Rule |
|---|---|---|---|
| **Single Image: Headline** | 200 chars (hard) | ≤ 70 chars | `WARN if > 70` |
| **Single Image: Intro Text** | 600 chars (hard) | ≤ 150 chars (before truncation) | `WARN if > 150` |
| Single Image: Description | 300 chars | ≤ 100 chars | `WARN if > 100` |
| **Video Ad: Headline** | 200 chars | ≤ 70 chars | `WARN if > 70` |
| Video Ad: Intro Text | 600 chars | ≤ 150 chars | `WARN if > 150` |
| **Carousel: Card Headline** | 45 chars | 40 chars | `len(card_headline) ≤ 45` |
| Carousel: Cards | 2–10 cards | 3–5 cards | `2 ≤ card_count ≤ 10` |
| **Message Ad: Subject** | 60 chars | ≤ 40 chars | `len(subject) ≤ 60` |
| **Message Ad: Body** | 1500 chars | ≤ 1000 chars | `len(body) ≤ 1500` |
| **Conversation Ad: CTA buttons** | 25 chars per button | — | `len(cta_text) ≤ 25` |
| Conversation Ad: Max buttons | 5 per message | — | `button_count ≤ 5` |
| Lead Gen Form: Headline | 60 chars | — | `len(form_headline) ≤ 60` |
| Lead Gen Form: Details | 160 chars | — | `len(form_details) ≤ 160` |
| Company Name | 25 chars | — | Auto from company page |

#### Media Specifications

| Format | Spec | Constraint |
|---|---|---|
| Single Image | 1200×627 (1.91:1) or 1080×1080 (1:1) or 628×1200 (1:2.4) | ≤ 5 MB, JPG/PNG |
| Video | 360p–1080p, 16:9 or 1:1 or 9:16 | 3 sec – 30 min, ≤ 200 MB, MP4 |
| Carousel Image | 1080×1080 (1:1) | ≤ 10 MB per card, JPG/PNG |
| Event Image | 1920×1080 (16:9) | ≤ 5 MB |
| Document Ad | PDF, DOC, PPT | ≤ 100 MB, max 300 pages |

---

## 3. Policy & Compliance Guardrails

### 3.1 Universal Forbidden Triggers (ALL PLATFORMS)

#### Text Pattern Blocklist

```python
FORBIDDEN_PATTERNS = [
    # Exaggerated Claims
    r"(?i)(100%\s*(guaranteed|results|success))",
    r"(?i)(get\s*rich\s*quick)",
    r"(?i)(make\s*\$?\d+[kK]?\s*(per|a)\s*(day|week|month))",
    r"(?i)(guaranteed\s*(income|returns|profit))",
    r"(?i)(no\s*risk)",
    r"(?i)(instant\s*(results|cure|fix))",
    r"(?i)(miracle\s*(cure|solution|product))",
    r"(?i)(once\s*in\s*a\s*lifetime)",
    r"(?i)(limited\s*time.*act\s*now)",
    r"(?i)(secret\s*(method|formula|technique))",
    
    # Discriminatory Language
    r"(?i)(based\s*on\s*(your\s*)?(race|religion|ethnicity|disability))",
    r"(?i)(are\s*you\s*(overweight|fat|ugly|poor|broke|sick))",
    r"(?i)(people\s*like\s*you)",
    
    # Misleading Health Claims
    r"(?i)(cures?\s*(cancer|diabetes|covid|hiv))",
    r"(?i)(fda\s*approved)\s+(?!.*\bactually\b)",
    r"(?i)(doctors?\s*(hate|don'?t\s*want\s*you\s*to\s*know))",
    
    # Financial Misrepresentation
    r"(?i)(guaranteed\s*(roi|returns|investment))",
    r"(?i)(bitcoin|crypto)\s*(guaranteed|no\s*risk)",
    r"(?i)(double\s*your\s*money)",
]

VALIDATION:
  FOR each text_field IN ad_payload:
    FOR each pattern IN FORBIDDEN_PATTERNS:
      IF regex_match(text_field, pattern):
        RETURN FAIL(reason=f"Forbidden trigger: {pattern}", field=text_field)
  RETURN PASS
```

#### Visual Content Blocklist

- [ ] No extreme Before/After comparisons (weight loss, skin, cosmetic)
- [ ] No shocking / graphic imagery (violence, gore, accidents)
- [ ] No misleading UI elements (fake buttons, fake notifications, fake system alerts)
- [ ] No competitor logos without explicit comparison context
- [ ] No unauthorized celebrity / public figure imagery
- [ ] No deepfake content without disclosure
- [ ] No content targeting minors with age-restricted products
- [ ] No weapons, drugs, or tobacco imagery (unless platform-approved regulated category)

---

### 3.2 Google Ads — Platform-Specific Policies

| Policy Area | Rule | Action on Violation |
|---|---|---|
| Trademarks | Cannot use competitor trademarks in ad text (headlines/descriptions) | FAIL + suggest removal |
| Destination mismatch | Final URL domain must match display URL domain | FAIL |
| Repeated punctuation | No `!!!`, `???`, or excessive caps | FAIL |
| Gimmicky formatting | No unusual spacing, symbols as letters (e.g., "FR33") | FAIL |
| Countdown timers | Must reflect real deadlines | WARN |
| Price in ad | Must match landing page price | FAIL if mismatch |
| Restricted categories | Healthcare, financial services, gambling → extra review | FLAG for manual review |
| Editorial standards | Proper grammar, no all-caps (except acronyms) | FAIL |

---

### 3.3 Meta Ads — Platform-Specific Policies

| Policy Area | Rule | Remediation |
|---|---|---|
| **Personal attributes** | NEVER call out personal characteristics directly | Rewrite to solution-focused copy |
| | ❌ "Are you in debt?" | ✅ "Financial management solutions" |
| | ❌ "Struggling with your weight?" | ✅ "Explore wellness programs" |
| | ❌ "Are you single?" | ✅ "Meet new people" |
| | ❌ "Do you have diabetes?" | ✅ "Managing blood sugar levels" |
| Discriminatory practices | Cannot target by race, ethnicity, religion for housing, credit, employment | FAIL — remove sensitive targeting |
| Special Ad Categories | Housing, Credit, Employment, Social Issues → restricted targeting | AUTO-ENABLE special_ad_category flag |
| Cryptocurrency | Crypto ads require prior written permission | FAIL unless pre-approved |
| Political / social issues | Requires "Paid for by" disclaimer + identity verification | FAIL if disclaimer missing |
| Landing page quality | No pop-ups, no misleading content, functional page | FAIL |
| Text overlay on images | No longer enforced as hard limit, but < 20% text recommended | WARN if > 20% text detected |

---

### 3.4 TikTok Ads — Platform-Specific Policies

| Policy Area | Rule | Action |
|---|---|---|
| **Watermarks** | Zero tolerance for competitor watermarks (Instagram, YouTube, etc.) | FAIL |
| **Video quality** | No pixelated, blurry, or low-res content | FAIL if resolution < 540×960 |
| **Audio** | No unlicensed commercial music; use TikTok Commercial Music Library | FAIL if audio not licensed |
| UI mimicry | Cannot mimic TikTok UI elements (fake like buttons, etc.) | FAIL |
| Shock/scare tactics | No jump scares, anxiety-inducing content | FAIL |
| User-generated content | Must have creator authorization for Spark Ads | FAIL if no auth code |
| Age-gating | Alcohol, gambling → age restriction required | FAIL if not age-gated |
| Unsubstantiated claims | "Best", "#1", "Award-winning" → must have proof | WARN + request substantiation |
| Disclosure requirements | Paid partnerships, sponsored content must be labeled | FAIL if no disclosure |

---

### 3.5 LinkedIn Ads — Platform-Specific Policies

| Policy Area | Rule | Action |
|---|---|---|
| **Professional tone** | B2B professional language only | FAIL if informal / slang |
| **ALL CAPS** | Prohibited in headlines and body (except acronyms ≤ 5 chars) | FAIL |
| **Excessive emojis** | Max 3 emojis per text field | FAIL if > 3 |
| **Clickbait** | No misleading headlines ("You won't believe...") | FAIL |
| Job discrimination | Cannot target by age, gender, religion for job ads | FAIL |
| Profanity | Zero tolerance | FAIL |
| Third-party data | Cannot claim to have scraped LinkedIn data | FAIL |
| InMail frequency | LinkedIn enforces per-member frequency caps (1 per 45 days) | System-enforced |
| Lead Gen Forms | Must link to privacy policy URL | FAIL if missing |
| Content gating | Gated content must deliver what's promised | WARN |

---

## 4. Pre-Flight Validation Logic

### 4.1 Master Validation Function (Pseudocode)

```python
def pre_flight_validate(payload: dict, platform: str) -> ValidationResult:
    """
    Binary PASS/FAIL pre-flight validation for ad payloads.
    Returns: ValidationResult with status, errors[], warnings[]
    """
    errors = []
    warnings = []
    
    # ── Step 1: Platform Detection ──
    assert platform in ["google_ads", "meta_ads", "tiktok_ads", "linkedin_ads"]
    
    # ── Step 2: Character Length Validation ──
    constraints = CONSTRAINT_MATRIX[platform]
    for field_name, field_value in payload.text_fields.items():
        rule = constraints.get(field_name)
        if rule:
            if len(field_value) > rule.hard_max:
                errors.append(f"FAIL: {field_name} exceeds max {rule.hard_max} chars (got {len(field_value)})")
            elif len(field_value) > rule.optimal_max:
                warnings.append(f"WARN: {field_name} exceeds optimal {rule.optimal_max} chars")
            if rule.min_count and len(field_value) < rule.min_count:
                errors.append(f"FAIL: {field_name} below minimum {rule.min_count} chars")
    
    # ── Step 3: Asset Count Validation ──
    for asset_type, count in payload.asset_counts.items():
        rule = constraints.get(asset_type)
        if rule:
            if count < rule.min_count:
                errors.append(f"FAIL: {asset_type} requires min {rule.min_count} (got {count})")
            if count > rule.max_count:
                errors.append(f"FAIL: {asset_type} exceeds max {rule.max_count} (got {count})")
    
    # ── Step 4: URL Validation ──
    for url_field in payload.urls:
        if not url_field.startswith("https://"):
            errors.append(f"FAIL: URL must use HTTPS: {url_field}")
        if not has_utm_parameters(url_field):
            warnings.append(f"WARN: Missing UTM parameters: {url_field}")
        if not is_valid_url_format(url_field):
            errors.append(f"FAIL: Invalid URL format: {url_field}")
    
    # ── Step 5: Policy Compliance Scan ──
    for field_name, field_value in payload.text_fields.items():
        policy_result = scan_forbidden_patterns(field_value, platform)
        if policy_result.violations:
            errors.extend(policy_result.violations)
    
    # ── Step 6: Media Validation (if applicable) ──
    if payload.media_assets:
        for asset in payload.media_assets:
            media_result = validate_media_specs(asset, platform)
            errors.extend(media_result.errors)
            warnings.extend(media_result.warnings)
    
    # ── Step 7: API Token Validation ──
    token_result = validate_api_tokens(platform, payload.credentials)
    if not token_result.valid:
        errors.append(f"FAIL: Invalid API credentials — {token_result.reason}")
    
    # ── Final Verdict ──
    status = "PASS" if len(errors) == 0 else "FAIL"
    return ValidationResult(status=status, errors=errors, warnings=warnings)
```

---

### 4.2 JSON Schema — Google Ads RSA Payload

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Google Ads Responsive Search Ad Payload",
  "type": "object",
  "required": ["campaign_id", "ad_group_id", "final_url", "headlines", "descriptions"],
  "properties": {
    "campaign_id": {
      "type": "string",
      "pattern": "^[0-9]+$"
    },
    "ad_group_id": {
      "type": "string",
      "pattern": "^[0-9]+$"
    },
    "final_url": {
      "type": "string",
      "format": "uri",
      "pattern": "^https://"
    },
    "path1": {
      "type": "string",
      "maxLength": 15
    },
    "path2": {
      "type": "string",
      "maxLength": 15
    },
    "headlines": {
      "type": "array",
      "minItems": 3,
      "maxItems": 15,
      "items": {
        "type": "object",
        "required": ["text"],
        "properties": {
          "text": {
            "type": "string",
            "minLength": 1,
            "maxLength": 30
          },
          "pinned_position": {
            "type": "string",
            "enum": ["HEADLINE_1", "HEADLINE_2", "HEADLINE_3", "UNSPECIFIED"]
          }
        }
      }
    },
    "descriptions": {
      "type": "array",
      "minItems": 2,
      "maxItems": 4,
      "items": {
        "type": "object",
        "required": ["text"],
        "properties": {
          "text": {
            "type": "string",
            "minLength": 1,
            "maxLength": 90
          },
          "pinned_position": {
            "type": "string",
            "enum": ["DESCRIPTION_1", "DESCRIPTION_2", "UNSPECIFIED"]
          }
        }
      }
    }
  }
}
```

---

### 4.3 JSON Schema — Meta Ads Payload

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Meta Ads Creative Payload",
  "type": "object",
  "required": ["ad_account_id", "campaign_id", "adset_id", "creative"],
  "properties": {
    "ad_account_id": {
      "type": "string",
      "pattern": "^act_[0-9]+$"
    },
    "campaign_id": {
      "type": "string"
    },
    "adset_id": {
      "type": "string"
    },
    "creative": {
      "type": "object",
      "required": ["name", "object_story_spec"],
      "properties": {
        "name": {
          "type": "string",
          "maxLength": 255
        },
        "object_story_spec": {
          "type": "object",
          "properties": {
            "page_id": {
              "type": "string"
            },
            "link_data": {
              "type": "object",
              "properties": {
                "message": {
                  "type": "string",
                  "maxLength": 2200,
                  "_optimal_max": 125
                },
                "name": {
                  "type": "string",
                  "maxLength": 255,
                  "_optimal_max": 40
                },
                "description": {
                  "type": "string",
                  "maxLength": 255,
                  "_optimal_max": 30
                },
                "link": {
                  "type": "string",
                  "format": "uri",
                  "pattern": "^https://"
                },
                "call_to_action": {
                  "type": "object",
                  "properties": {
                    "type": {
                      "type": "string",
                      "enum": [
                        "APPLY_NOW", "BOOK_NOW", "CONTACT_US", "DOWNLOAD",
                        "GET_OFFER", "GET_QUOTE", "LEARN_MORE", "ORDER_NOW",
                        "SHOP_NOW", "SIGN_UP", "SUBSCRIBE", "WATCH_MORE",
                        "SEND_WHATSAPP_MESSAGE", "GET_DIRECTIONS", "CALL_NOW"
                      ]
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    "tracking_specs": {
      "type": "array",
      "items": {
        "type": "object"
      }
    }
  }
}
```

---

### 4.4 JSON Schema — TikTok Ads Payload

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "TikTok Ads Creative Payload",
  "type": "object",
  "required": ["advertiser_id", "adgroup_id", "creatives"],
  "properties": {
    "advertiser_id": {
      "type": "string"
    },
    "adgroup_id": {
      "type": "string"
    },
    "creatives": {
      "type": "array",
      "minItems": 1,
      "items": {
        "type": "object",
        "required": ["ad_text", "video_id"],
        "properties": {
          "ad_name": {
            "type": "string",
            "maxLength": 512
          },
          "ad_text": {
            "type": "string",
            "minLength": 1,
            "maxLength": 100,
            "_validation_note": "Latin chars: 1-100; CJK: 12-100"
          },
          "video_id": {
            "type": "string"
          },
          "image_ids": {
            "type": "array",
            "items": { "type": "string" }
          },
          "call_to_action": {
            "type": "string",
            "enum": [
              "DOWNLOAD_NOW", "SHOP_NOW", "SIGN_UP", "LEARN_MORE",
              "CONTACT_US", "APPLY_NOW", "BOOK_NOW", "GET_QUOTE",
              "SUBSCRIBE", "ORDER_NOW", "PLAY_GAME", "INSTALL_NOW",
              "GET_OFFER", "VIEW_NOW", "LISTEN_NOW", "WATCH_NOW"
            ]
          },
          "display_name": {
            "type": "string",
            "minLength": 2,
            "maxLength": 40
          },
          "landing_page_url": {
            "type": "string",
            "format": "uri",
            "pattern": "^https://"
          }
        }
      }
    }
  }
}
```

---

### 4.5 JSON Schema — LinkedIn Ads Payload

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "LinkedIn Ads Sponsored Content Payload",
  "type": "object",
  "required": ["account_id", "campaign_id", "creative"],
  "properties": {
    "account_id": {
      "type": "string",
      "pattern": "^urn:li:sponsoredAccount:[0-9]+$"
    },
    "campaign_id": {
      "type": "string",
      "pattern": "^urn:li:sponsoredCampaign:[0-9]+$"
    },
    "creative": {
      "type": "object",
      "required": ["type", "content"],
      "properties": {
        "type": {
          "type": "string",
          "enum": ["SINGLE_IMAGE", "VIDEO", "CAROUSEL", "MESSAGE", "CONVERSATION", "DOCUMENT"]
        },
        "content": {
          "type": "object",
          "properties": {
            "intro_text": {
              "type": "string",
              "maxLength": 600,
              "_optimal_max": 150
            },
            "headline": {
              "type": "string",
              "maxLength": 200,
              "_optimal_max": 70
            },
            "description": {
              "type": "string",
              "maxLength": 300,
              "_optimal_max": 100
            },
            "destination_url": {
              "type": "string",
              "format": "uri",
              "pattern": "^https://"
            },
            "call_to_action": {
              "type": "string",
              "enum": [
                "APPLY", "DOWNLOAD", "VIEW_QUOTE", "LEARN_MORE",
                "SIGN_UP", "SUBSCRIBE", "REGISTER", "JOIN",
                "ATTEND", "REQUEST_DEMO"
              ]
            }
          }
        },
        "message_content": {
          "type": "object",
          "properties": {
            "subject": {
              "type": "string",
              "maxLength": 60,
              "_optimal_max": 40
            },
            "body": {
              "type": "string",
              "maxLength": 1500,
              "_optimal_max": 1000
            },
            "cta_buttons": {
              "type": "array",
              "maxItems": 5,
              "items": {
                "type": "object",
                "properties": {
                  "label": {
                    "type": "string",
                    "maxLength": 25
                  },
                  "destination_url": {
                    "type": "string",
                    "format": "uri"
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

---

### 4.6 URL & UTM Validation Function

```python
def validate_url(url: str, platform: str) -> ValidationResult:
    """Validate URL format and UTM parameters."""
    errors = []
    warnings = []
    
    # HTTPS enforcement
    if not url.startswith("https://"):
        errors.append("FAIL: URL must use HTTPS protocol")
    
    # URL format check
    from urllib.parse import urlparse, parse_qs
    parsed = urlparse(url)
    
    if not parsed.scheme or not parsed.netloc:
        errors.append("FAIL: Invalid URL structure")
    
    # UTM parameter validation
    params = parse_qs(parsed.query)
    required_utms = ["utm_source", "utm_medium", "utm_campaign"]
    recommended_utms = ["utm_content", "utm_term"]
    
    for utm in required_utms:
        if utm not in params:
            warnings.append(f"WARN: Missing required UTM parameter: {utm}")
    
    for utm in recommended_utms:
        if utm not in params:
            warnings.append(f"INFO: Missing recommended UTM parameter: {utm}")
    
    # Platform-specific click ID parameters
    platform_params = {
        "google_ads": "gclid",
        "meta_ads": "fbclid",
        "tiktok_ads": "ttclid",
        "linkedin_ads": "li_fat_id"
    }
    
    # Auto-append check — these are typically auto-appended by platforms
    expected_param = platform_params.get(platform)
    if expected_param:
        warnings.append(f"INFO: Ensure {expected_param} auto-tagging is enabled in platform settings")
    
    status = "PASS" if len(errors) == 0 else "FAIL"
    return ValidationResult(status=status, errors=errors, warnings=warnings)
```

---

### 4.7 API Token Permission Validator

```python
def validate_api_tokens(platform: str, credentials: dict) -> TokenValidationResult:
    """
    Pre-flight check for API token validity and permissions.
    """
    
    checks = {
        "google_ads": {
            "required_tokens": ["developer_token", "oauth2_client_id", "oauth2_client_secret", "refresh_token"],
            "required_permissions": ["STANDARD_ACCESS"],  # or TEST_ACCOUNT for sandbox
            "validation_endpoint": "GET /v19/customers/{customer_id}",
            "mcc_check": "login_customer_id required if using MCC"
        },
        "meta_ads": {
            "required_tokens": ["system_user_token", "page_access_token"],
            "required_permissions": [
                "ads_management",
                "ads_read",
                "business_management",
                "pages_read_engagement"
            ],
            "validation_endpoint": "GET /me?fields=id,name&access_token={token}",
            "token_type_check": "System User Token (long-lived) preferred over User Token"
        },
        "tiktok_ads": {
            "required_tokens": ["access_token", "app_id", "secret"],
            "required_permissions": [
                "ad.read", "ad.write",
                "campaign.read", "campaign.write",
                "creative.read", "creative.write",
                "report.read"
            ],
            "validation_endpoint": "GET /open_api/v1.3/oauth2/advertiser/get/",
            "sandbox_check": "Use sandbox app_id for testing"
        },
        "linkedin_ads": {
            "required_tokens": ["access_token"],
            "required_permissions": [
                "r_ads", "r_ads_reporting",
                "rw_ads",
                "r_organization_social"
            ],
            "validation_endpoint": "GET /rest/adAccounts?q=search",
            "oauth_version": "OAuth 2.0 Three-Legged"
        }
    }
    
    config = checks[platform]
    errors = []
    
    # Check all required tokens are present
    for token_key in config["required_tokens"]:
        if token_key not in credentials or not credentials[token_key]:
            errors.append(f"FAIL: Missing required credential: {token_key}")
    
    # Check token is not expired (basic format check)
    if "access_token" in credentials:
        token = credentials["access_token"]
        if len(token) < 20:
            errors.append("FAIL: Access token appears invalid (too short)")
    
    if errors:
        return TokenValidationResult(valid=False, errors=errors)
    
    return TokenValidationResult(
        valid=True,
        message=f"Credentials present for {platform}. Validate against: {config['validation_endpoint']}"
    )
```

---

## 5. API Authentication & Token Matrix

| Platform | Auth Method | Token Type | Expiry | Refresh Mechanism |
|---|---|---|---|---|
| **Google Ads** | OAuth 2.0 | Developer Token + OAuth Refresh Token | Refresh token: no expiry (unless revoked) | `POST /token` with refresh_token |
| **Meta Ads** | OAuth 2.0 | System User Token (recommended) | 60 days (user tokens); never (system user) | Exchange for long-lived token |
| **TikTok Ads** | OAuth 2.0 | Access Token + Refresh Token | 24 hours (access); 365 days (refresh) | `POST /oauth2/access_token/` |
| **LinkedIn Ads** | OAuth 2.0 (3-legged) | Access Token | 60 days (access); 365 days (refresh) | `POST /oauth/v2/accessToken` |

### Token Hierarchy

```
Google Ads:
  Manager Account (MCC)
    └── Developer Token (API access)
        └── OAuth 2.0 Client
            └── Refresh Token → Access Token (per request)

Meta Ads:
  Business Manager
    └── System User
        └── System User Access Token
            └── Page Access Token (per page)
    └── App
        └── App Access Token (server-to-server)

TikTok Ads:
  TikTok for Business Center
    └── App (registered)
        └── Auth Code → Access Token + Refresh Token
            └── Advertiser ID (per account)

LinkedIn Ads:
  LinkedIn Developer App
    └── OAuth 2.0 Three-Legged Flow
        └── Access Token (member-context)
            └── Ad Account URN (per account)
```

---

## 6. UTM & Tracking Standards

### Mandatory UTM Template

```
{final_url}?utm_source={platform}&utm_medium={medium}&utm_campaign={campaign_name}&utm_content={ad_name}&utm_term={keyword_or_audience}
```

### Platform-Specific UTM Mapping

| Parameter | Google Ads | Meta Ads | TikTok Ads | LinkedIn Ads |
|---|---|---|---|---|
| `utm_source` | `google` | `facebook` or `instagram` | `tiktok` | `linkedin` |
| `utm_medium` | `cpc` / `cpv` / `display` | `paid_social` | `paid_social` | `paid_social` |
| `utm_campaign` | `{campaign.name}` | `{{campaign.name}}` | `{campaign_name}` | `{campaign_name}` |
| `utm_content` | `{creative.name}` | `{{ad.name}}` | `{ad_name}` | `{creative_name}` |
| `utm_term` | `{keyword}` | `{{adset.name}}` | `{adgroup_name}` | `{audience_name}` |
| Auto-click ID | `gclid` (auto) | `fbclid` (auto) | `ttclid` (auto) | `li_fat_id` (auto) |

---

## 7. Official Reference Sources

### Google Ads
| Resource | URL |
|---|---|
| API Documentation | https://developers.google.com/google-ads/api/docs/start |
| Ad Policies | https://support.google.com/adspolicy/answer/6008942 |
| Consent Mode v2 | https://developers.google.com/tag-platform/security/guides/consent |
| Performance Max Guide | https://developers.google.com/google-ads/api/docs/performance-max/overview |
| Asset Specs | https://support.google.com/google-ads/answer/7005917 |
| Value-Based Bidding | https://developers.google.com/google-ads/api/docs/bidding/value-based |

### Meta Ads
| Resource | URL |
|---|---|
| Marketing API | https://developers.facebook.com/docs/marketing-apis/ |
| Ad Standards | https://transparency.meta.com/policies/ad-standards/ |
| Advantage+ Automation | https://www.facebook.com/business/help/advantage-plus |
| Conversions API | https://developers.facebook.com/docs/marketing-api/conversions-api/ |
| Creative Specs | https://www.facebook.com/business/ads-guide |
| Special Ad Categories | https://www.facebook.com/business/help/298000447747885 |

### TikTok Ads
| Resource | URL |
|---|---|
| Business API | https://business-api.tiktok.com/portal/docs |
| Creative Specs | https://ads.tiktok.com/help/article/video-creative-specifications |
| Smart+ Campaigns | https://ads.tiktok.com/help/article/smart-plus-campaigns |
| Symphony AI | https://ads.tiktok.com/help/article/tiktok-symphony |
| Ad Policy Center | https://ads.tiktok.com/help/article/tiktok-advertising-policies |
| Spark Ads | https://ads.tiktok.com/help/article/spark-ads |

### LinkedIn Ads
| Resource | URL |
|---|---|
| Marketing API | https://learn.microsoft.com/en-us/linkedin/marketing/ |
| Ad Specifications | https://business.linkedin.com/marketing-solutions/ad-specs |
| Advertising Policies | https://www.linkedin.com/legal/ads-policy |
| Lead Gen Forms API | https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads/lead-gen |
| Conversions API | https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api |

---

## Appendix A: Pre-Flight Checklist (Per Campaign)

### Universal Checks

- [ ] All text fields within character limits
- [ ] All URLs use HTTPS
- [ ] All URLs contain UTM parameters
- [ ] No forbidden text patterns detected
- [ ] API tokens validated and not expired
- [ ] Landing page loads in ≤ 3 seconds
- [ ] Landing page mobile-responsive
- [ ] Privacy policy linked (where required)
- [ ] Conversion tracking verified (pixel/tag/CAPI/postback)

### Google Ads

- [ ] Asset Strength ≥ "GOOD"
- [ ] Consent Mode v2 enabled (EEA)
- [ ] Enhanced Conversions configured
- [ ] Customer Match lists uploaded (if applicable)
- [ ] Negative keyword lists applied
- [ ] Ad extensions/assets configured (sitelinks, callouts, snippets)
- [ ] Conversion actions have sufficient data (≥ 30 in 30 days for VBB)

### Meta Ads

- [ ] CAPI configured and Event Match Quality ≥ 6.0
- [ ] Pixel + CAPI deduplication active
- [ ] Special Ad Category flag set (if applicable)
- [ ] No personal attribute call-outs in copy
- [ ] Advantage+ Creative enabled
- [ ] ≥ 5 creative variations per ad set
- [ ] Image text ≤ 20% (recommended)

### TikTok Ads

- [ ] Video resolution ≥ 1080×1920 (9:16)
- [ ] Video duration 9–15 seconds (optimal)
- [ ] 3-second hook rate strategy defined
- [ ] No competitor watermarks
- [ ] Audio from Commercial Music Library
- [ ] Safe zone compliance verified
- [ ] Spark Ads auth code obtained (if UGC)

### LinkedIn Ads

- [ ] Professional tone verified
- [ ] No ALL CAPS (except acronyms)
- [ ] Max 3 emojis per field
- [ ] Lead Gen Form has privacy policy URL
- [ ] ABM company list ≥ 300 matches
- [ ] Predictive Audience seed ≥ 300 contacts
- [ ] Buying committee roles mapped

---

## Appendix B: Error Code Quick Reference

| Error Code | Platform | Meaning | Resolution |
|---|---|---|---|
| `CHAR_LIMIT_EXCEEDED` | All | Text exceeds maximum characters | Shorten text to limit |
| `MISSING_REQUIRED_FIELD` | All | Required field is empty | Populate the field |
| `INVALID_URL` | All | URL format invalid or not HTTPS | Fix URL format |
| `FORBIDDEN_CONTENT` | All | Policy violation detected in text | Rewrite flagged content |
| `ASSET_STRENGTH_LOW` | Google | Asset strength below "GOOD" | Add more/better assets |
| `CONSENT_MODE_MISSING` | Google | Consent Mode v2 not configured | Enable consent signals |
| `PERSONAL_ATTRIBUTE` | Meta | Ad copy calls out personal attributes | Rewrite to solution-focused |
| `SPECIAL_CATEGORY_MISSING` | Meta | Special Ad Category not set | Enable appropriate category |
| `CAPI_NOT_CONFIGURED` | Meta | Conversions API not set up | Configure server-side tracking |
| `WATERMARK_DETECTED` | TikTok | Competitor watermark in video | Remove watermark |
| `SAFE_ZONE_VIOLATION` | TikTok | Text/CTA in blocked UI zones | Reposition creative elements |
| `LOW_RESOLUTION` | TikTok | Video below minimum resolution | Re-export at ≥ 1080×1920 |
| `UNPROFESSIONAL_TONE` | LinkedIn | Informal language detected | Rewrite in B2B professional tone |
| `EMOJI_EXCESS` | LinkedIn | More than 3 emojis in field | Reduce emoji count |
| `TOKEN_EXPIRED` | All | API access token expired | Refresh token |
| `INSUFFICIENT_PERMISSIONS` | All | Token lacks required scopes | Request additional permissions |

---

## 8. MCP (Model Context Protocol) Integration

### 8.1 MCP Server Architecture

```json
{
  "mcp_servers": {
    "ads-automation": {
      "name": "Multi-Platform Ads Automation MCP Server",
      "version": "2026.08",
      "transport": "stdio",
      "description": "Provides tools for planning, validating, and executing ad campaigns across Google, Meta, TikTok, and LinkedIn",
      "capabilities": {
        "tools": true,
        "resources": true,
        "prompts": true
      }
    }
  }
}
```

### 8.2 MCP Tools Registry

#### Campaign Planning Tools

| Tool Name | Description | Input Schema | Output |
|---|---|---|---|
| `plan_campaign` | Generate campaign structure based on objective & platform | `{platform, objective, budget, target_audience, creative_assets}` | Campaign blueprint JSON |
| `select_campaign_type` | Auto-select optimal campaign type using §1 decision trees | `{platform, objective, product_catalog, conversion_data}` | Recommended campaign type + rationale |
| `generate_audience` | Build audience targeting spec per platform rules | `{platform, icp_description, seed_data, expansion_level}` | Audience targeting JSON payload |
| `suggest_bid_strategy` | Recommend bidding strategy using §9 decision trees | `{platform, objective, historical_cpa, historical_roas, budget}` | Bid strategy + parameters |

#### Validation Tools

| Tool Name | Description | Input Schema | Output |
|---|---|---|---|
| `validate_ad_payload` | Run full pre-flight validation (§4) | `{platform, payload}` | `{status: PASS/FAIL, errors[], warnings[]}` |
| `validate_text_compliance` | Scan text against policy guardrails (§3) | `{platform, text_fields}` | `{violations[], suggestions[]}` |
| `validate_media_specs` | Check image/video against platform specs (§2) | `{platform, media_metadata}` | `{status, dimension_check, format_check, size_check}` |
| `validate_url` | Check URL format + UTM completeness (§6) | `{url, platform}` | `{status, utm_present, https_valid}` |
| `validate_tokens` | Verify API credentials and permissions (§4.7) | `{platform, credentials}` | `{valid, missing_permissions[], expiry_status}` |

#### Execution Tools

| Tool Name | Description | Input Schema | Output |
|---|---|---|---|
| `create_campaign` | Create campaign via platform API | `{platform, campaign_payload, credentials}` | `{campaign_id, status, api_response}` |
| `create_ad_group` | Create ad group / ad set | `{platform, adgroup_payload, campaign_id, credentials}` | `{adgroup_id, status}` |
| `create_ad` | Create ad creative | `{platform, ad_payload, adgroup_id, credentials}` | `{ad_id, status, review_status}` |
| `upload_media` | Upload image/video asset to platform | `{platform, file_path, media_type, credentials}` | `{media_id, url, dimensions}` |
| `update_bid` | Modify bidding strategy or target | `{platform, campaign_id, bid_strategy, bid_value, credentials}` | `{status, previous_bid, new_bid}` |
| `pause_campaign` | Pause active campaign | `{platform, campaign_id, credentials}` | `{status, effective_time}` |

#### Reporting Tools

| Tool Name | Description | Input Schema | Output |
|---|---|---|---|
| `get_campaign_metrics` | Fetch performance data | `{platform, campaign_id, date_range, metrics, credentials}` | Metrics JSON per §16 schema |
| `get_creative_performance` | Fetch per-creative metrics | `{platform, campaign_id, date_range, credentials}` | Creative-level metrics |
| `detect_creative_fatigue` | Analyze creative fatigue signals (§1.3) | `{platform, campaign_id, lookback_days, credentials}` | `{fatigue_score, affected_creatives[], recommendations[]}` |
| `generate_cross_platform_report` | Unified report across platforms (§16) | `{platforms[], campaign_ids{}, date_range, credentials{}}` | Unified report JSON |

### 8.3 MCP Resources

```json
{
  "resources": [
    {
      "uri": "ads://constraints/{platform}",
      "name": "Platform Constraint Matrix",
      "description": "Technical limits for the specified platform (§2)",
      "mimeType": "application/json"
    },
    {
      "uri": "ads://policies/{platform}",
      "name": "Platform Policy Rules",
      "description": "Compliance guardrails for the specified platform (§3)",
      "mimeType": "application/json"
    },
    {
      "uri": "ads://schemas/{platform}/{ad_type}",
      "name": "Ad Payload Schema",
      "description": "JSON Schema for ad payload validation (§4)",
      "mimeType": "application/schema+json"
    },
    {
      "uri": "ads://benchmarks/{platform}/{industry}",
      "name": "Performance Benchmarks",
      "description": "KPI thresholds by platform and industry (§12)",
      "mimeType": "application/json"
    },
    {
      "uri": "ads://rate-limits/{platform}",
      "name": "API Rate Limits",
      "description": "Request quotas and throttling rules (§14)",
      "mimeType": "application/json"
    }
  ]
}
```

### 8.4 MCP Prompts

```json
{
  "prompts": [
    {
      "name": "plan_full_campaign",
      "description": "Interactive campaign planning wizard",
      "arguments": [
        {"name": "platform", "description": "Target ad platform", "required": true},
        {"name": "objective", "description": "Campaign objective", "required": true},
        {"name": "monthly_budget", "description": "Total monthly budget in USD", "required": true},
        {"name": "industry", "description": "Business industry vertical", "required": true}
      ]
    },
    {
      "name": "audit_existing_campaign",
      "description": "Audit a running campaign against all guardrails",
      "arguments": [
        {"name": "platform", "description": "Ad platform", "required": true},
        {"name": "campaign_id", "description": "Campaign to audit", "required": true}
      ]
    },
    {
      "name": "fix_rejected_ad",
      "description": "Diagnose and fix a rejected ad creative",
      "arguments": [
        {"name": "platform", "description": "Ad platform", "required": true},
        {"name": "rejection_reason", "description": "Platform rejection message", "required": true},
        {"name": "original_ad_payload", "description": "The rejected ad payload", "required": true}
      ]
    }
  ]
}
```

### 8.5 MCP Workflow — End-to-End Campaign Launch

```
STEP 1: plan_campaign
  → Input: objective, budget, audience description
  → Output: campaign blueprint

STEP 2: select_campaign_type
  → Uses §1 decision trees
  → Output: campaign_type, bidding_strategy

STEP 3: suggest_bid_strategy
  → Uses §9 decision trees
  → Output: bid_strategy, bid_value, rationale

STEP 4: generate_audience
  → Output: targeting payload

STEP 5: validate_ad_payload
  → Runs §2 constraints + §3 policies + §4 schemas
  → IF FAIL → return errors for human review
  → IF PASS → proceed

STEP 6: validate_tokens
  → Check credentials before API calls

STEP 7: upload_media
  → Upload creative assets

STEP 8: create_campaign → create_ad_group → create_ad
  → Sequential API calls with retry logic (§15)

STEP 9: get_campaign_metrics (after 24–48h)
  → Monitor initial performance
  → Run detect_creative_fatigue after 72h

STEP 10: generate_cross_platform_report
  → Unified view if multi-platform
```

---

## 9. Bidding Strategy Decision Trees

### 9.1 Google Ads Bidding Decision Tree

```
START
│
├─ Do you have ≥ 30 conversions in last 30 days?
│   ├─ YES → Do you have conversion value data?
│   │   ├─ YES → Is ROAS the primary KPI?
│   │   │   ├─ YES → USE: Target ROAS (tROAS)
│   │   │   │   SET target_roas = historical_roas × 0.9  # Start conservative
│   │   │   │   MIN target_roas = 100%
│   │   │   │   RAMP: Increase by 10% every 2 weeks if stable
│   │   │   └─ NO  → USE: Maximize Conversion Value
│   │   │           No target cap; let Google optimize freely
│   │   └─ NO  → Is CPA the primary KPI?
│   │       ├─ YES → USE: Target CPA (tCPA)
│   │       │   SET target_cpa = historical_cpa × 1.2  # Start with headroom
│   │       │   MIN target_cpa = 50% of historical
│   │       │   RAMP: Decrease by 10% every 2 weeks if stable
│   │       └─ NO  → USE: Maximize Conversions
│   │               No target cap; maximize volume
│   └─ NO  → Is the campaign new (< 2 weeks)?
│       ├─ YES → USE: Maximize Clicks
│       │   SET daily_budget = 2× target_cpa × 10
│       │   PURPOSE: Build conversion data
│       │   SWITCH to tCPA after 30 conversions
│       └─ NO  → USE: Maximize Conversions
│               Then SWITCH to tCPA after 30 conversions
│
├─ Campaign Type = PERFORMANCE_MAX?
│   └─ REQUIRED: Value-Based Bidding (tROAS or Max Conv Value)
│       IF no conversion values → USE tCPA
│       Asset Strength MUST be ≥ "GOOD"
│
└─ Campaign Type = DEMAND_GEN?
    └─ USE: Maximize Conversions OR Target CPA
        Requires conversion tracking configured
```

### 9.2 Meta Ads Bidding Decision Tree

```
START
│
├─ Campaign Objective?
│   ├─ SALES / CONVERSIONS
│   │   ├─ Have sufficient conversion data (≥ 50 events/week per ad set)?
│   │   │   ├─ YES → Is ROAS the primary KPI?
│   │   │   │   ├─ YES → USE: Minimum ROAS Bid Strategy
│   │   │   │   │   SET roas_floor = historical_roas × 0.8
│   │   │   │   │   PAIR with: Advantage+ Campaign Budget (CBO)
│   │   │   │   └─ NO  → USE: Cost Per Result Goal
│   │   │   │       SET cost_goal = target_cpa
│   │   │   │       ALLOW 20% variance in learning phase
│   │   │   └─ NO  → USE: Highest Volume (no cap)
│   │   │       PURPOSE: Exit learning phase ASAP
│   │   │       NEED: ≥ 50 conversions per ad set per week
│   │   │       BUDGET: ≥ 10× target_cpa per ad set daily
│   │   └─ Advantage+ Shopping?
│   │       └─ USE: Highest Volume OR Highest Value
│   │           Budget at campaign level (CBO mandatory)
│   │
│   ├─ LEADS
│   │   ├─ Lead Gen Form?
│   │   │   └─ USE: Highest Volume → then Cost Per Result
│   │   └─ Website Leads?
│   │       └─ USE: Cost Per Result Goal once ≥ 50 events/week
│   │
│   ├─ TRAFFIC
│   │   └─ USE: Highest Volume of Link Clicks
│   │       OR: Landing Page Views (higher quality)
│   │
│   └─ AWARENESS
│       └─ USE: Reach and Frequency
│           OR: Highest Volume of Impressions
│
├─ Budget Strategy:
│   ├─ CBO (Campaign Budget Optimization) → RECOMMENDED for Advantage+
│   │   SET daily_budget at CAMPAIGN level
│   │   Meta distributes across ad sets
│   └─ ABO (Ad Set Budget Optimization) → For manual control
│       SET daily_budget at AD SET level
│       USE when testing specific audiences
│
└─ Learning Phase Rules:
    ├─ Need ≥ 50 optimization events per ad set per week
    ├─ Do NOT edit during learning phase (first 7 days)
    ├─ If learning_limited → Broaden audience or increase budget
    └─ If stuck > 7 days → Consolidate ad sets
```

### 9.3 TikTok Ads Bidding Decision Tree

```
START
│
├─ Campaign Type = SMART+ ?
│   └─ Bidding is FULLY AUTOMATED
│       Agent provides: budget, optimization_goal, creative assets
│       TikTok AI handles: bid, audience, placement
│       Optimization goals: CONVERSION, VALUE, CLICK, REACH
│
├─ Campaign Type = STANDARD?
│   ├─ Optimization Goal = CONVERSION?
│   │   ├─ Have ≥ 50 conversions in 7 days?
│   │   │   ├─ YES → USE: Cost Cap
│   │   │   │   SET cost_cap = target_cpa
│   │   │   │   ALLOW 20% overshoot in first 3 days
│   │   │   └─ OR → USE: Minimum Cost (no cap)
│   │   │       For maximum volume
│   │   └─ NO  → USE: Minimum Cost (no cap)
│   │       PURPOSE: Accumulate conversion data
│   │       SWITCH to Cost Cap after 50 conversions
│   │
│   ├─ Optimization Goal = CLICK?
│   │   └─ USE: Minimum Cost
│   │       OR: Bid Cap if strict CPC target needed
│   │
│   └─ Optimization Goal = REACH / VIDEO_VIEW?
│       └─ USE: Minimum Cost (Reach)
│           OR: Frequency Cap (max 3 per user per week)
│
└─ Budget Rules:
    ├─ Daily minimum: $20 USD (campaign level)
    ├─ Ad group daily minimum: $20 USD
    ├─ Recommended: ≥ 20× target CPA per ad group daily
    └─ Do NOT change budget by > 30% in 24h (resets learning)
```

### 9.4 LinkedIn Ads Bidding Decision Tree

```
START
│
├─ Campaign Objective?
│   ├─ LEAD GENERATION (Lead Gen Forms)
│   │   ├─ Budget > $100/day?
│   │   │   ├─ YES → USE: Maximum Delivery
│   │   │   │   LinkedIn auto-optimizes for lowest CPL
│   │   │   │   Best for sufficient budget + broad audience
│   │   │   └─ NO  → USE: Manual Bidding
│   │   │       SET bid = estimated_cpl × 1.5
│   │   │       More control with smaller budgets
│   │   └─ Target Cost available?
│   │       └─ USE: Target Cost
│   │           SET target_cost = desired_cpl
│   │           LinkedIn auto-adjusts bids around target
│   │
│   ├─ WEBSITE VISITS
│   │   ├─ USE: Maximum Delivery (CPC-based)
│   │   │   OR: Manual CPC if strict CPC target
│   │   └─ Minimum CPC bid: $2.00 USD (varies by audience)
│   │
│   ├─ BRAND AWARENESS
│   │   └─ USE: Maximum Delivery (CPM-based)
│   │       Optimize for impressions
│   │       SET frequency_cap = 4 per member per week
│   │
│   ├─ ENGAGEMENT
│   │   └─ USE: Maximum Delivery
│   │       Optimize for engagement actions
│   │
│   └─ VIDEO VIEWS
│       └─ USE: Maximum Delivery (CPV-based)
│           Optimize for video views (2+ sec)
│
└─ Budget Rules:
    ├─ Daily minimum: $10 USD
    ├─ Lifetime minimum: $100 USD
    ├─ Recommended: ≥ $50/day for meaningful data
    └─ Message Ads: Charged per send ($0.20–$0.80 per send)
```

---

## 10. Budget Allocation Logic

### 10.1 Cross-Platform Budget Distribution

```python
def allocate_budget_cross_platform(
    total_monthly_budget: float,
    platforms: list,
    objective: str,
    historical_data: dict = None
) -> dict:
    """
    Distribute budget across platforms based on objective and performance.
    Returns: {platform: monthly_budget}
    """
    
    # ── Default Allocation by Objective (no historical data) ──
    DEFAULT_SPLITS = {
        "ecommerce_sales": {
            "google_ads": 0.40,    # Search intent capture
            "meta_ads": 0.35,      # Prospecting + retargeting
            "tiktok_ads": 0.20,    # Awareness + viral reach
            "linkedin_ads": 0.05   # Usually not for B2C ecommerce
        },
        "b2b_lead_gen": {
            "google_ads": 0.30,    # High-intent search
            "meta_ads": 0.20,      # Retargeting + lookalikes
            "tiktok_ads": 0.05,    # Limited B2B use case
            "linkedin_ads": 0.45   # Primary B2B channel
        },
        "app_install": {
            "google_ads": 0.30,    # UAC / App campaigns
            "meta_ads": 0.35,      # App installs + deep linking
            "tiktok_ads": 0.30,    # High engagement for apps
            "linkedin_ads": 0.05   # B2B apps only
        },
        "brand_awareness": {
            "google_ads": 0.20,    # YouTube + Display
            "meta_ads": 0.35,      # Reach + frequency
            "tiktok_ads": 0.35,    # Viral potential
            "linkedin_ads": 0.10   # Thought leadership
        },
        "local_business": {
            "google_ads": 0.50,    # Local search + Maps
            "meta_ads": 0.35,      # Local awareness
            "tiktok_ads": 0.10,    # Local discovery
            "linkedin_ads": 0.05   # B2B local services
        }
    }
    
    # ── Performance-Based Reallocation (with historical data) ──
    if historical_data and all(p in historical_data for p in platforms):
        # Calculate efficiency score per platform
        scores = {}
        for platform in platforms:
            data = historical_data[platform]
            if objective in ["ecommerce_sales"]:
                scores[platform] = data.get("roas", 1.0)
            elif objective in ["b2b_lead_gen", "app_install"]:
                # Inverse CPA — lower CPA = higher score
                cpa = data.get("cpa", 100)
                scores[platform] = 1.0 / max(cpa, 0.01)
            else:
                # CPM efficiency for awareness
                cpm = data.get("cpm", 10)
                scores[platform] = 1.0 / max(cpm, 0.01)
        
        # Normalize scores to percentages
        total_score = sum(scores.values())
        allocation = {
            p: round((scores[p] / total_score) * total_monthly_budget, 2)
            for p in platforms
        }
    else:
        # Use default splits
        splits = DEFAULT_SPLITS.get(objective, DEFAULT_SPLITS["ecommerce_sales"])
        allocation = {
            p: round(splits.get(p, 0.25) * total_monthly_budget, 2)
            for p in platforms
        }
    
    # ── Minimum Budget Enforcement ──
    PLATFORM_MINIMUMS = {
        "google_ads": 300,     # $10/day minimum
        "meta_ads": 300,       # $10/day minimum effective
        "tiktok_ads": 600,     # $20/day minimum
        "linkedin_ads": 300    # $10/day minimum
    }
    
    for platform in platforms:
        minimum = PLATFORM_MINIMUMS.get(platform, 300)
        if allocation[platform] < minimum:
            allocation[platform] = 0  # Below minimum → don't run
            # Redistribute to remaining platforms
    
    return allocation
```

### 10.2 Intra-Campaign Budget Rules

| Platform | Budget Level | Minimum | Optimization |
|---|---|---|---|
| **Google Ads** | Campaign | $1/day (Search), no minimum (PMax) | Budget shared across ad groups |
| **Meta Ads (CBO)** | Campaign | $1/day per ad set × ad set count | Advantage Campaign Budget distributes |
| **Meta Ads (ABO)** | Ad Set | $1/day per ad set | Manual distribution |
| **TikTok Ads** | Campaign | $50/day (campaign), $20/day (ad group) | Auto-distribution in Smart+ |
| **LinkedIn Ads** | Campaign | $10/day | Manual; no auto-distribution |

### 10.3 Budget Scaling Rules

```
SCALING RULES (to avoid resetting algorithm learning):

Google Ads:
  - Increase budget: ≤ 20% per change, wait 3–5 days between changes
  - Decrease budget: ≤ 20% per change
  - PMax: Budget changes take 1–2 weeks to stabilize

Meta Ads:
  - Increase budget: ≤ 20% every 48–72 hours
  - Decrease budget: Any decrease resets learning phase
  - Rule: NEVER change budget during learning phase (first 7 days)

TikTok Ads:
  - Increase budget: ≤ 30% per 24 hours
  - Decrease budget: ≤ 30% per 24 hours
  - >50% change = full learning reset

LinkedIn Ads:
  - No strict scaling rules
  - Recommended: Adjust weekly based on pacing
  - Monitor daily spend vs daily budget ratio
```

---

## 11. A/B Testing Framework

### 11.1 Testing Hierarchy (Priority Order)

```
TEST PRIORITY (highest impact first):

1. OFFER / VALUE PROPOSITION
   - What you're selling / the deal
   - Impact: 🔴🔴🔴🔴🔴 (Highest)
   - Example: "Free trial" vs "50% off" vs "Free consultation"

2. CREATIVE FORMAT
   - Video vs Image vs Carousel
   - Impact: 🔴🔴🔴🔴
   - Example: UGC video vs polished brand video

3. HOOK / HEADLINE
   - First 3 seconds (video) or headline (static)
   - Impact: 🔴🔴🔴🔴
   - Example: Question hook vs Bold claim vs Statistic

4. AUDIENCE / TARGETING
   - Who sees the ad
   - Impact: 🔴🔴🔴
   - Example: Broad vs Lookalike vs Interest-based

5. LANDING PAGE
   - Where they go after click
   - Impact: 🔴🔴🔴
   - Example: Long-form vs Short-form vs Video landing page

6. AD COPY BODY
   - Supporting text
   - Impact: 🔴🔴
   - Example: Benefit-led vs Feature-led vs Social proof

7. CTA BUTTON
   - Call to action
   - Impact: 🔴
   - Example: "Shop Now" vs "Learn More" vs "Get Started"
```

### 11.2 Statistical Significance Calculator

```python
import math

def calculate_sample_size(
    baseline_conversion_rate: float,
    minimum_detectable_effect: float,  # e.g., 0.10 for 10% lift
    significance_level: float = 0.05,  # 95% confidence
    power: float = 0.80               # 80% power
) -> int:
    """
    Calculate required sample size per variant for A/B test.
    """
    p1 = baseline_conversion_rate
    p2 = p1 * (1 + minimum_detectable_effect)
    
    # Z-scores
    z_alpha = 1.96   # 95% confidence (two-tailed)
    z_beta = 0.84    # 80% power
    
    p_avg = (p1 + p2) / 2
    
    numerator = (z_alpha * math.sqrt(2 * p_avg * (1 - p_avg)) + 
                 z_beta * math.sqrt(p1 * (1 - p1) + p2 * (1 - p2))) ** 2
    denominator = (p2 - p1) ** 2
    
    return math.ceil(numerator / denominator)


def is_statistically_significant(
    visitors_a: int, conversions_a: int,
    visitors_b: int, conversions_b: int,
    confidence: float = 0.95
) -> dict:
    """
    Check if A/B test result is statistically significant.
    Returns: {significant: bool, p_value: float, lift: float, winner: str}
    """
    rate_a = conversions_a / max(visitors_a, 1)
    rate_b = conversions_b / max(visitors_b, 1)
    
    # Pooled standard error
    p_pool = (conversions_a + conversions_b) / (visitors_a + visitors_b)
    se = math.sqrt(p_pool * (1 - p_pool) * (1/visitors_a + 1/visitors_b))
    
    if se == 0:
        return {"significant": False, "p_value": 1.0, "lift": 0, "winner": "none"}
    
    z_score = (rate_b - rate_a) / se
    
    # Two-tailed p-value approximation
    p_value = 2 * (1 - 0.5 * (1 + math.erf(abs(z_score) / math.sqrt(2))))
    
    lift = ((rate_b - rate_a) / max(rate_a, 0.0001)) * 100
    winner = "B" if rate_b > rate_a else "A"
    significant = p_value < (1 - confidence)
    
    return {
        "significant": significant,
        "p_value": round(p_value, 4),
        "lift_percent": round(lift, 2),
        "winner": winner,
        "rate_a": round(rate_a, 4),
        "rate_b": round(rate_b, 4)
    }
```

### 11.3 Platform-Specific Testing Methods

| Platform | Built-in A/B Test | Setup | Duration Rule |
|---|---|---|---|
| **Google Ads** | Campaign Experiments | Drafts & Experiments → set traffic split (50/50) | Min 2 weeks, or stat sig reached |
| **Meta Ads** | A/B Test Tool | Experiments → select variable → auto-split | Min 7 days, Meta auto-calculates |
| **TikTok Ads** | Split Test | Campaign → Enable Split Test → select variable | Min 7 days, auto-winner selection |
| **LinkedIn Ads** | Manual (duplicate campaigns) | Create parallel campaigns with one variable changed | Min 2 weeks, manual analysis |

### 11.4 Testing Rules

- [ ] Test ONLY one variable at a time
- [ ] Minimum 2 variants, maximum 5 variants per test
- [ ] Run test for minimum 7 days (full business week cycle)
- [ ] Do NOT declare winner before statistical significance (p < 0.05)
- [ ] Minimum 100 conversions per variant for reliable results
- [ ] Document every test: hypothesis, variable, result, learning
- [ ] After winner declared: scale winner, create new test hypothesis

---

## 12. Performance Benchmarks & KPI Thresholds

### 12.1 Google Ads Benchmarks (2026)

| Industry | Avg CTR (Search) | Avg CPC | Avg Conv Rate | Avg CPA |
|---|---|---|---|---|
| E-commerce | 2.5–4.0% | $0.80–$2.50 | 2.5–4.5% | $25–$65 |
| SaaS / B2B Tech | 2.0–3.5% | $3.00–$8.00 | 2.0–4.0% | $80–$200 |
| Finance / Insurance | 2.5–4.0% | $3.50–$12.00 | 3.0–6.0% | $50–$150 |
| Healthcare | 3.0–4.5% | $2.00–$6.00 | 2.5–5.0% | $40–$120 |
| Real Estate | 3.0–5.0% | $1.50–$4.00 | 2.0–4.5% | $35–$100 |
| Education | 3.5–5.0% | $1.00–$4.00 | 3.0–6.0% | $30–$80 |
| Legal | 2.0–3.5% | $5.00–$15.00 | 3.0–7.0% | $70–$200 |
| Travel | 4.0–6.0% | $0.50–$2.00 | 2.0–4.0% | $20–$60 |

### 12.2 Meta Ads Benchmarks (2026)

| Industry | Avg CTR (Feed) | Avg CPM | Avg CPC | Avg Conv Rate |
|---|---|---|---|---|
| E-commerce | 1.0–2.0% | $8–$18 | $0.50–$2.00 | 1.5–3.5% |
| SaaS / B2B | 0.8–1.5% | $15–$35 | $2.00–$5.00 | 1.0–2.5% |
| Finance | 0.6–1.2% | $12–$30 | $2.50–$6.00 | 1.5–4.0% |
| Healthcare | 0.8–1.5% | $10–$25 | $1.50–$4.00 | 1.0–3.0% |
| Education | 0.9–1.8% | $8–$20 | $1.00–$3.00 | 2.0–5.0% |
| Gaming | 1.0–2.5% | $5–$15 | $0.30–$1.50 | 2.0–5.0% |
| CPG / Retail | 1.0–2.0% | $6–$15 | $0.40–$1.50 | 1.5–3.0% |

### 12.3 TikTok Ads Benchmarks (2026)

| Metric | Good | Average | Poor |
|---|---|---|---|
| **3-sec Hook Rate** | ≥ 35% | 25–35% | < 25% |
| **CTR (In-Feed)** | ≥ 1.5% | 0.8–1.5% | < 0.8% |
| **Video Completion Rate** | ≥ 15% | 8–15% | < 8% |
| **CPM** | < $6 | $6–$12 | > $12 |
| **CPC** | < $0.80 | $0.80–$2.00 | > $2.00 |
| **CPA (E-commerce)** | < $20 | $20–$50 | > $50 |
| **CPA (App Install)** | < $3 | $3–$8 | > $8 |
| **ROAS (E-commerce)** | > 4.0x | 2.0–4.0x | < 2.0x |
| **Creative Lifespan** | > 14 days | 7–14 days | < 7 days |

### 12.4 LinkedIn Ads Benchmarks (2026)

| Metric | Good | Average | Poor |
|---|---|---|---|
| **CTR (Sponsored Content)** | ≥ 0.8% | 0.4–0.8% | < 0.4% |
| **CTR (Message Ads)** | ≥ 35% (open rate) | 25–35% | < 25% |
| **CPC** | < $5 | $5–$12 | > $12 |
| **CPM** | < $30 | $30–$60 | > $60 |
| **CPL (Lead Gen Forms)** | < $50 | $50–$150 | > $150 |
| **Lead Gen Form Fill Rate** | ≥ 15% | 10–15% | < 10% |
| **Engagement Rate** | ≥ 2.0% | 1.0–2.0% | < 1.0% |
| **Video View Rate** | ≥ 30% | 15–30% | < 15% |
| **InMail Response Rate** | ≥ 10% | 5–10% | < 5% |

### 12.5 Automated Alert Thresholds

```python
ALERT_THRESHOLDS = {
    "universal": {
        "ctr_drop": {
            "trigger": "CTR drops > 25% vs 7-day avg",
            "severity": "HIGH",
            "action": "Check ad fatigue, audience saturation, or bid competitiveness"
        },
        "cpa_spike": {
            "trigger": "CPA increases > 30% vs 7-day avg",
            "severity": "HIGH",
            "action": "Review targeting, landing page, conversion tracking"
        },
        "budget_underspend": {
            "trigger": "Daily spend < 70% of daily budget for 3 consecutive days",
            "severity": "MEDIUM",
            "action": "Broaden targeting, increase bids, or reduce budget"
        },
        "zero_conversions": {
            "trigger": "0 conversions for 48 hours with > $100 spend",
            "severity": "CRITICAL",
            "action": "Check conversion tracking, landing page, ad approval status"
        },
        "frequency_cap": {
            "trigger": "Frequency > 4.0 (Meta/TikTok) or > 6.0 (Google Display)",
            "severity": "MEDIUM",
            "action": "Refresh creatives, expand audience, or cap frequency"
        },
        "roas_below_floor": {
            "trigger": "ROAS < 1.0x for 72 hours",
            "severity": "CRITICAL",
            "action": "Pause non-performing ad sets, review attribution window"
        }
    }
}
```

---

## 13. Retargeting & Remarketing Funnel Logic

### 13.1 Full-Funnel Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    TOFU — TOP OF FUNNEL                     │
│                   (Awareness & Discovery)                   │
│─────────────────────────────────────────────────────────────│
│ AUDIENCE: Cold — no prior interaction                       │
│ PLATFORMS: TikTok (primary), Meta, Google Display, YouTube  │
│ FORMATS: Video (6–15 sec), Carousel, Spark Ads             │
│ OBJECTIVE: Reach, Video Views, Brand Awareness              │
│ BUDGET ALLOCATION: 30–40% of total                          │
│ KPI: CPM, Video View Rate, 3-sec Hook Rate, Reach           │
│ CONTENT: Educational, entertaining, problem-aware            │
│                                                             │
│ EXIT CRITERIA → User: watches 50%+ video, visits site,      │
│                 engages with content                         │
└─────────────┬───────────────────────────────────────────────┘
              │ PIXEL/CAPI fires → adds to MOFU audience
              ▼
┌─────────────────────────────────────────────────────────────┐
│                   MOFU — MIDDLE OF FUNNEL                    │
│                  (Consideration & Intent)                    │
│─────────────────────────────────────────────────────────────│
│ AUDIENCE: Warm — site visitors, video viewers, engagers     │
│ PLATFORMS: Meta (primary), Google Search, LinkedIn           │
│ FORMATS: Carousel, Single Image, Lead Gen Forms              │
│ OBJECTIVE: Traffic, Lead Gen, Engagement                     │
│ BUDGET ALLOCATION: 30–40% of total                          │
│ KPI: CTR, CPC, CPL, Landing Page View Rate                  │
│ CONTENT: Case studies, comparisons, demos, free resources    │
│                                                             │
│ RETARGETING WINDOWS:                                        │
│   - Website visitors: 1–14 days                             │
│   - Video viewers (50%+): 1–30 days                         │
│   - Social engagers: 1–30 days                              │
│   - Email subscribers (non-converted): 1–60 days            │
│                                                             │
│ EXCLUSIONS: Already converted users                         │
│                                                             │
│ EXIT CRITERIA → User: adds to cart, starts checkout,         │
│                 downloads lead magnet, submits form          │
└─────────────┬───────────────────────────────────────────────┘
              │ Conversion event fires → adds to BOFU audience
              ▼
┌─────────────────────────────────────────────────────────────┐
│                   BOFU — BOTTOM OF FUNNEL                    │
│                   (Conversion & Action)                      │
│─────────────────────────────────────────────────────────────│
│ AUDIENCE: Hot — cart abandoners, form starters, demo viewers │
│ PLATFORMS: Google Search (branded), Meta, LinkedIn           │
│ FORMATS: Dynamic Product Ads (DPA), Single Image, Carousel  │
│ OBJECTIVE: Conversions, Sales, App Installs                  │
│ BUDGET ALLOCATION: 20–30% of total                          │
│ KPI: CPA, ROAS, Conversion Rate, Revenue                    │
│ CONTENT: Urgency, social proof, testimonials, offers         │
│                                                             │
│ RETARGETING WINDOWS:                                        │
│   - Cart abandoners: 1–7 days (aggressive)                  │
│   - Product viewers: 1–14 days                              │
│   - Checkout starters: 1–3 days (highest priority)          │
│   - Lead form abandoners: 1–7 days                          │
│                                                             │
│ EXCLUSIONS: Converted users (last 7–30 days)                │
│                                                             │
│ EXIT CRITERIA → User: completes purchase / conversion        │
└─────────────┬───────────────────────────────────────────────┘
              │ Purchase/conversion event fires
              ▼
┌─────────────────────────────────────────────────────────────┐
│                 POST-PURCHASE — RETENTION                    │
│                (Upsell, Cross-sell, Loyalty)                 │
│─────────────────────────────────────────────────────────────│
│ AUDIENCE: Existing customers                                │
│ PLATFORMS: Meta (Custom Audiences), Google (Customer Match)  │
│ FORMATS: DPA (cross-sell), Carousel, Video                   │
│ OBJECTIVE: Repeat purchase, LTV increase                     │
│ BUDGET ALLOCATION: 10% of total                              │
│ KPI: Repeat purchase rate, LTV, ROAS on retention            │
│ CONTENT: New arrivals, complementary products, loyalty offers│
│                                                             │
│ RETARGETING WINDOWS:                                        │
│   - Recent buyers: 7–30 days (cross-sell)                   │
│   - Lapsed buyers: 30–90 days (win-back)                    │
│   - VIP customers: Ongoing (loyalty)                        │
│                                                             │
│ EXCLUSIONS: Recent buyers (< 7 days) to avoid annoyance     │
└─────────────────────────────────────────────────────────────┘
```

### 13.2 Retargeting Audience Builder

```python
RETARGETING_AUDIENCES = {
    "google_ads": {
        "remarketing_lists": [
            {"name": "All Website Visitors - 30d", "window": 30, "source": "GA4"},
            {"name": "Product Viewers - 14d", "window": 14, "source": "GA4", "event": "view_item"},
            {"name": "Cart Abandoners - 7d", "window": 7, "source": "GA4", "event": "add_to_cart", "exclude_event": "purchase"},
            {"name": "Checkout Starters - 3d", "window": 3, "source": "GA4", "event": "begin_checkout", "exclude_event": "purchase"},
            {"name": "Past Purchasers - 90d", "window": 90, "source": "GA4", "event": "purchase"},
            {"name": "YouTube Viewers - 30d", "window": 30, "source": "YouTube", "action": "viewed_video"},
            {"name": "Customer Match - Email", "source": "CRM", "match_type": "email"}
        ]
    },
    "meta_ads": {
        "custom_audiences": [
            {"name": "Website Visitors - 30d", "source": "pixel", "window": 30},
            {"name": "Product Page Viewers - 14d", "source": "pixel", "event": "ViewContent", "window": 14},
            {"name": "Add to Cart - 7d", "source": "pixel", "event": "AddToCart", "window": 7, "exclude": "Purchase"},
            {"name": "Initiate Checkout - 3d", "source": "pixel", "event": "InitiateCheckout", "window": 3, "exclude": "Purchase"},
            {"name": "Video Viewers 50%+ - 30d", "source": "engagement", "action": "video_watched_50_pct", "window": 30},
            {"name": "IG/FB Engagers - 30d", "source": "engagement", "action": "page_or_profile_engagement", "window": 30},
            {"name": "Lead Form Openers - 14d", "source": "lead_form", "action": "opened_not_submitted", "window": 14},
            {"name": "Customer List", "source": "file_upload", "match_keys": ["email", "phone"]}
        ]
    },
    "tiktok_ads": {
        "custom_audiences": [
            {"name": "Website Visitors - 30d", "source": "pixel", "window": 30},
            {"name": "Video Viewers 50%+ - 30d", "source": "engagement", "window": 30},
            {"name": "Profile Visitors - 30d", "source": "engagement", "action": "profile_visit", "window": 30},
            {"name": "App Activity Users - 14d", "source": "app_events", "window": 14},
            {"name": "Customer List", "source": "file_upload"}
        ]
    },
    "linkedin_ads": {
        "matched_audiences": [
            {"name": "Website Visitors - 90d", "source": "insight_tag", "window": 90},
            {"name": "Lead Form Openers - 30d", "source": "lead_gen_form", "action": "opened", "window": 30},
            {"name": "Video Viewers 50%+ - 30d", "source": "engagement", "window": 30},
            {"name": "Company Page Engagers - 30d", "source": "engagement", "window": 30},
            {"name": "Contact List Upload", "source": "file_upload", "match_keys": ["email", "company"]},
            {"name": "Account List (ABM)", "source": "company_upload", "match_keys": ["company_name", "domain"]}
        ]
    }
}
```

---

## 14. API Rate Limits

### 14.1 Rate Limit Matrix

| Platform | Rate Limit | Scope | Throttle Response | Retry Header |
|---|---|---|---|---|
| **Google Ads** | 1,500 requests/day (basic), 15,000/day (standard) | Per Developer Token | HTTP 429 | `Retry-After` |
| Google Ads (mutate) | 5,000 operations/request | Per mutate call | HTTP 429 | `Retry-After` |
| Google Ads (reports) | 100 concurrent requests | Per account | HTTP 429 | `Retry-After` |
| **Meta Ads** | 200 calls/hour/ad account (estimated) | Per Ad Account + Token | HTTP 429, Error Code 17 | `X-Business-Use-Case-Usage` |
| Meta Ads (batch) | 50 requests per batch | Per batch call | — | — |
| Meta Ads (Marketing API) | Tier-based (dev/standard/advanced) | Per App | Error Code 4, 17, 32 | `x-app-usage` header |
| **TikTok Ads** | 10 requests/second, 600/minute | Per App | HTTP 429, Code 40100 | `X-RateLimit-Reset` |
| TikTok Ads (reporting) | 600 requests/minute | Per App | HTTP 429 | — |
| TikTok Ads (creative) | 100 uploads/day | Per Advertiser | HTTP 429 | — |
| **LinkedIn Ads** | 100 requests/day (per member token) | Per Member | HTTP 429 | `X-RateLimit-Limit`, `X-RateLimit-Remaining` |
| LinkedIn Ads (reporting) | 30 requests/minute | Per App | HTTP 429 | `X-RateLimit-Reset` |

### 14.2 Rate Limit Handling Logic

```python
import time
import random

class RateLimiter:
    """
    Platform-aware rate limiter with token bucket algorithm.
    """
    
    PLATFORM_LIMITS = {
        "google_ads": {"requests_per_second": 10, "daily_limit": 15000},
        "meta_ads": {"requests_per_second": 3, "hourly_limit": 200},
        "tiktok_ads": {"requests_per_second": 10, "minute_limit": 600},
        "linkedin_ads": {"requests_per_second": 1, "daily_limit": 100}
    }
    
    def __init__(self, platform: str):
        self.platform = platform
        self.limits = self.PLATFORM_LIMITS[platform]
        self.request_count = 0
        self.window_start = time.time()
    
    def wait_if_needed(self):
        """Block if approaching rate limit."""
        rps = self.limits["requests_per_second"]
        elapsed = time.time() - self.window_start
        
        if elapsed < 1.0 and self.request_count >= rps:
            sleep_time = 1.0 - elapsed + random.uniform(0.05, 0.2)  # Jitter
            time.sleep(sleep_time)
            self.request_count = 0
            self.window_start = time.time()
        elif elapsed >= 1.0:
            self.request_count = 0
            self.window_start = time.time()
        
        self.request_count += 1
    
    def handle_429(self, response_headers: dict) -> float:
        """Calculate backoff time from 429 response."""
        retry_after = response_headers.get("Retry-After")
        if retry_after:
            return float(retry_after)
        
        # Platform-specific header parsing
        if self.platform == "tiktok_ads":
            reset_time = response_headers.get("X-RateLimit-Reset")
            if reset_time:
                return max(float(reset_time) - time.time(), 1.0)
        
        if self.platform == "linkedin_ads":
            remaining = response_headers.get("X-RateLimit-Remaining", "0")
            if int(remaining) == 0:
                reset_time = response_headers.get("X-RateLimit-Reset")
                if reset_time:
                    return max(float(reset_time) - time.time(), 1.0)
        
        # Default backoff: 60 seconds
        return 60.0
```

---

## 15. Error Handling & Retry Logic

### 15.1 Retry Strategy Matrix

| Error Type | HTTP Code | Retryable? | Max Retries | Backoff Strategy | Initial Wait |
|---|---|---|---|---|---|
| Rate Limited | 429 | ✅ YES | 5 | Exponential + Jitter | `Retry-After` header or 60s |
| Server Error | 500, 502, 503 | ✅ YES | 3 | Exponential + Jitter | 5s |
| Gateway Timeout | 504 | ✅ YES | 3 | Exponential | 10s |
| Auth Expired | 401 | ✅ YES (after refresh) | 1 | Refresh token, then retry | 0s (immediate) |
| Bad Request | 400 | ❌ NO | 0 | — | — |
| Forbidden | 403 | ❌ NO | 0 | — | — |
| Not Found | 404 | ❌ NO | 0 | — | — |
| Conflict | 409 | ⚠️ CONDITIONAL | 1 | Wait + retry | 5s |
| Unprocessable | 422 | ❌ NO | 0 | — | — |
| Network Error | — | ✅ YES | 3 | Exponential + Jitter | 2s |
| Connection Timeout | — | ✅ YES | 3 | Linear | 5s |

### 15.2 Exponential Backoff with Jitter Implementation

```python
import time
import random
import logging

logger = logging.getLogger("ads_automation")

def retry_with_backoff(
    func,
    max_retries: int = 3,
    initial_wait: float = 1.0,
    max_wait: float = 300.0,
    backoff_factor: float = 2.0,
    jitter: bool = True,
    retryable_status_codes: set = {429, 500, 502, 503, 504},
    on_retry_callback=None
):
    """
    Execute function with exponential backoff retry logic.
    
    Args:
        func: Callable that returns (status_code, response_headers, response_body)
        max_retries: Maximum number of retry attempts
        initial_wait: Initial wait time in seconds
        max_wait: Maximum wait time cap in seconds
        backoff_factor: Multiplier for each retry (2.0 = double each time)
        jitter: Add random jitter to prevent thundering herd
        retryable_status_codes: HTTP status codes that trigger retry
        on_retry_callback: Optional callback(attempt, wait_time, error) called before each retry
    """
    last_exception = None
    
    for attempt in range(max_retries + 1):
        try:
            status_code, headers, body = func()
            
            # Success
            if 200 <= status_code < 300:
                return {"success": True, "status": status_code, "data": body, "attempts": attempt + 1}
            
            # Auth expired — special handling
            if status_code == 401:
                logger.warning(f"Auth expired on attempt {attempt + 1}. Refreshing token...")
                return {
                    "success": False,
                    "status": 401,
                    "action": "REFRESH_TOKEN_AND_RETRY",
                    "data": body,
                    "attempts": attempt + 1
                }
            
            # Non-retryable error
            if status_code not in retryable_status_codes:
                return {
                    "success": False,
                    "status": status_code,
                    "action": "DO_NOT_RETRY",
                    "data": body,
                    "attempts": attempt + 1
                }
            
            # Retryable error
            if attempt < max_retries:
                # Calculate wait time
                if status_code == 429 and "Retry-After" in headers:
                    wait_time = float(headers["Retry-After"])
                else:
                    wait_time = min(initial_wait * (backoff_factor ** attempt), max_wait)
                
                if jitter:
                    wait_time = wait_time * (0.5 + random.random())  # 50–150% of calculated wait
                
                logger.warning(
                    f"Attempt {attempt + 1}/{max_retries + 1} failed with {status_code}. "
                    f"Retrying in {wait_time:.1f}s..."
                )
                
                if on_retry_callback:
                    on_retry_callback(attempt, wait_time, body)
                
                time.sleep(wait_time)
            else:
                return {
                    "success": False,
                    "status": status_code,
                    "action": "MAX_RETRIES_EXCEEDED",
                    "data": body,
                    "attempts": attempt + 1
                }
        
        except (ConnectionError, TimeoutError) as e:
            last_exception = e
            if attempt < max_retries:
                wait_time = initial_wait * (backoff_factor ** attempt)
                if jitter:
                    wait_time = wait_time * (0.5 + random.random())
                
                logger.warning(f"Network error on attempt {attempt + 1}: {e}. Retrying in {wait_time:.1f}s...")
                time.sleep(wait_time)
            else:
                return {
                    "success": False,
                    "status": None,
                    "action": "NETWORK_ERROR_MAX_RETRIES",
                    "error": str(last_exception),
                    "attempts": attempt + 1
                }
    
    return {"success": False, "action": "UNKNOWN_ERROR", "attempts": max_retries + 1}
```

### 15.3 Platform-Specific Error Handling

```python
PLATFORM_ERROR_MAP = {
    "google_ads": {
        "QUOTA_ERROR": {"retryable": True, "wait": 60, "description": "Rate limit exceeded"},
        "INTERNAL_ERROR": {"retryable": True, "wait": 30, "description": "Google internal error"},
        "AUTHENTICATION_ERROR": {"retryable": False, "action": "REFRESH_TOKEN"},
        "POLICY_VIOLATION": {"retryable": False, "action": "FIX_CONTENT"},
        "RESOURCE_EXHAUSTED": {"retryable": True, "wait": 120, "description": "Daily quota exceeded"},
        "MUTATE_ERROR": {"retryable": False, "action": "FIX_PAYLOAD"},
        "REQUEST_ERROR": {"retryable": False, "action": "FIX_REQUEST"}
    },
    "meta_ads": {
        "OAuthException (Code 4)": {"retryable": True, "wait": 60, "description": "App-level rate limit"},
        "OAuthException (Code 17)": {"retryable": True, "wait": 300, "description": "Account-level rate limit"},
        "OAuthException (Code 32)": {"retryable": True, "wait": 600, "description": "Page-level rate limit"},
        "OAuthException (Code 190)": {"retryable": False, "action": "REFRESH_TOKEN"},
        "ValidationError (Code 100)": {"retryable": False, "action": "FIX_PAYLOAD"},
        "PolicyViolation (Code 1487851)": {"retryable": False, "action": "FIX_CONTENT"}
    },
    "tiktok_ads": {
        "40100": {"retryable": True, "wait": 60, "description": "Rate limit exceeded"},
        "40001": {"retryable": False, "action": "FIX_PARAMS", "description": "Invalid parameters"},
        "40002": {"retryable": False, "action": "REFRESH_TOKEN", "description": "Auth failed"},
        "40101": {"retryable": True, "wait": 120, "description": "Service busy"},
        "50001": {"retryable": True, "wait": 30, "description": "Internal server error"}
    },
    "linkedin_ads": {
        "UNAUTHORIZED": {"retryable": False, "action": "REFRESH_TOKEN"},
        "THROTTLED": {"retryable": True, "wait": 60, "description": "Rate limited"},
        "SERVICE_UNAVAILABLE": {"retryable": True, "wait": 30, "description": "LinkedIn down"},
        "VALIDATION_ERROR": {"retryable": False, "action": "FIX_PAYLOAD"},
        "QUOTA_EXCEEDED": {"retryable": True, "wait": 3600, "description": "Daily quota hit"}
    }
}
```

---

## 16. Cross-Platform Reporting Schema

### 16.1 Unified Metrics Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Cross-Platform Campaign Report",
  "type": "object",
  "required": ["report_metadata", "platform_data", "aggregated_metrics"],
  "properties": {
    "report_metadata": {
      "type": "object",
      "properties": {
        "report_id": {"type": "string"},
        "generated_at": {"type": "string", "format": "date-time"},
        "date_range": {
          "type": "object",
          "properties": {
            "start_date": {"type": "string", "format": "date"},
            "end_date": {"type": "string", "format": "date"}
          }
        },
        "currency": {"type": "string", "default": "USD"},
        "timezone": {"type": "string"}
      }
    },
    "platform_data": {
      "type": "object",
      "properties": {
        "google_ads": {"$ref": "#/definitions/platform_metrics"},
        "meta_ads": {"$ref": "#/definitions/platform_metrics"},
        "tiktok_ads": {"$ref": "#/definitions/platform_metrics"},
        "linkedin_ads": {"$ref": "#/definitions/platform_metrics"}
      }
    },
    "aggregated_metrics": {"$ref": "#/definitions/aggregated_totals"}
  },
  "definitions": {
    "platform_metrics": {
      "type": "object",
      "properties": {
        "spend": {"type": "number", "description": "Total spend in report currency"},
        "impressions": {"type": "integer"},
        "clicks": {"type": "integer"},
        "ctr": {"type": "number", "description": "Click-through rate (percentage)"},
        "cpc": {"type": "number", "description": "Cost per click"},
        "cpm": {"type": "number", "description": "Cost per thousand impressions"},
        "conversions": {"type": "integer"},
        "conversion_rate": {"type": "number", "description": "Conversions / clicks (percentage)"},
        "cpa": {"type": "number", "description": "Cost per acquisition"},
        "conversion_value": {"type": "number", "description": "Total conversion value (revenue)"},
        "roas": {"type": "number", "description": "Return on ad spend (value / spend)"},
        "reach": {"type": "integer", "description": "Unique users reached"},
        "frequency": {"type": "number", "description": "Average impressions per user"},
        "video_views": {"type": "integer"},
        "video_view_rate": {"type": "number"},
        "engagements": {"type": "integer"},
        "engagement_rate": {"type": "number"},
        "campaigns": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "campaign_id": {"type": "string"},
              "campaign_name": {"type": "string"},
              "status": {"type": "string", "enum": ["ACTIVE", "PAUSED", "ENDED", "LEARNING"]},
              "spend": {"type": "number"},
              "impressions": {"type": "integer"},
              "clicks": {"type": "integer"},
              "conversions": {"type": "integer"},
              "cpa": {"type": "number"},
              "roas": {"type": "number"},
              "creatives": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "creative_id": {"type": "string"},
                    "creative_name": {"type": "string"},
                    "format": {"type": "string", "enum": ["IMAGE", "VIDEO", "CAROUSEL", "TEXT", "DOCUMENT"]},
                    "spend": {"type": "number"},
                    "impressions": {"type": "integer"},
                    "clicks": {"type": "integer"},
                    "ctr": {"type": "number"},
                    "conversions": {"type": "integer"},
                    "fatigue_score": {"type": "number", "description": "0-100, higher = more fatigued"}
                  }
                }
              }
            }
          }
        }
      }
    },
    "aggregated_totals": {
      "type": "object",
      "properties": {
        "total_spend": {"type": "number"},
        "total_impressions": {"type": "integer"},
        "total_clicks": {"type": "integer"},
        "total_conversions": {"type": "integer"},
        "total_conversion_value": {"type": "number"},
        "blended_ctr": {"type": "number"},
        "blended_cpc": {"type": "number"},
        "blended_cpa": {"type": "number"},
        "blended_roas": {"type": "number"},
        "total_reach": {"type": "integer", "description": "Sum of platform reach (not deduplicated)"},
        "platform_contribution": {
          "type": "object",
          "description": "Percentage of total metrics per platform",
          "properties": {
            "google_ads": {"$ref": "#/definitions/contribution_pct"},
            "meta_ads": {"$ref": "#/definitions/contribution_pct"},
            "tiktok_ads": {"$ref": "#/definitions/contribution_pct"},
            "linkedin_ads": {"$ref": "#/definitions/contribution_pct"}
          }
        }
      }
    },
    "contribution_pct": {
      "type": "object",
      "properties": {
        "spend_pct": {"type": "number"},
        "conversion_pct": {"type": "number"},
        "revenue_pct": {"type": "number"}
      }
    }
  }
}
```

### 16.2 Metric Normalization Rules

| Metric | Google Ads | Meta Ads | TikTok Ads | LinkedIn Ads | Unified Name |
|---|---|---|---|---|---|
| Cost | `cost_micros / 1,000,000` | `spend` | `spend` | `costInLocalCurrency` | `spend` |
| Impressions | `impressions` | `impressions` | `impressions` | `impressions` | `impressions` |
| Clicks | `clicks` | `clicks` | `clicks` | `clicks` | `clicks` |
| CTR | `ctr` (already %) | `ctr` (needs ×100) | `ctr` (already %) | `clickRate` (needs ×100) | `ctr` (%) |
| Conversions | `conversions` | `actions[type=purchase]` | `conversions` | `externalWebsiteConversions` | `conversions` |
| Revenue | `conversion_value` | `action_values[type=purchase]` | `complete_payment_value` | `conversionValueInLocalCurrency` | `conversion_value` |
| Reach | `N/A (use impressions)` | `reach` | `reach` | `approximateUniqueImpressions` | `reach` |
| Video Views | `video_views` | `video_views` (3-sec) | `video_play_actions` | `videoViews` | `video_views` |
| Engagement | `interactions` | `post_engagements` | `engagements` | `totalEngagements` | `engagements` |

### 16.3 Cross-Platform Attribution Considerations

```
ATTRIBUTION WINDOWS (defaults):

  Google Ads:
    - Click-through: 30 days
    - View-through: 1 day (Display/Video)
    - Model: Data-driven (default since 2023)

  Meta Ads:
    - Click-through: 7 days (default), configurable 1/7/28 days
    - View-through: 1 day (default)
    - Model: Last-touch within window

  TikTok Ads:
    - Click-through: 7 days (default), configurable 1/7/14/28 days
    - View-through: 1 day (default)
    - Model: Last-touch within window

  LinkedIn Ads:
    - Click-through: 30 days (default), configurable 1/7/30/90 days
    - View-through: 7 days (default), configurable 1/7/30 days
    - Model: Last-touch / each campaign

CROSS-PLATFORM DEDUPLICATION:
  PROBLEM: Same conversion may be claimed by multiple platforms
  SOLUTION:
    1. Use UTM parameters to identify traffic source
    2. Use a central analytics tool (GA4) as source of truth
    3. Compare platform-reported vs GA4-reported conversions
    4. Apply fractional attribution if using data-driven model
    5. Never sum conversions across platforms (will over-count)

RECOMMENDATION:
  - Use GA4 as unified attribution source
  - Set consistent attribution windows across platforms where possible
  - Report "platform-reported" metrics alongside "GA4-attributed" metrics
  - Blended ROAS = Total Revenue (GA4) / Total Ad Spend (all platforms)
```

---

## Appendix C: Campaign Naming Convention

```
FORMAT:
  {platform}_{objective}_{audience}_{geo}_{format}_{date}

EXAMPLES:
  gads_search_brand_us_rsa_202608
  gads_pmax_prospecting_global_mixed_202608
  meta_conversions_lookalike_id_video_202608
  meta_awareness_broad_sea_carousel_202608
  tiktok_traffic_interest_us_video_202608
  tiktok_smartplus_broad_global_video_202608
  li_leadgen_abm_us_singleimage_202608
  li_awareness_predictive_apac_video_202608

RULES:
  - All lowercase, underscore separated
  - No spaces, no special characters
  - Platform prefix: gads, meta, tiktok, li
  - Date format: YYYYMM
  - Max 80 characters
```

---

## Appendix D: Glossary

| Term | Definition |
|---|---|
| **ABM** | Account-Based Marketing — targeting specific companies |
| **ABO** | Ad Set Budget Optimization — budget set at ad set level (Meta) |
| **CAPI** | Conversions API — server-side event tracking (Meta) |
| **CBO** | Campaign Budget Optimization — budget set at campaign level (Meta) |
| **CPA** | Cost Per Acquisition — total spend / conversions |
| **CPL** | Cost Per Lead — total spend / leads generated |
| **CPM** | Cost Per Mille — cost per 1,000 impressions |
| **CTR** | Click-Through Rate — clicks / impressions × 100 |
| **DPA** | Dynamic Product Ads — auto-generated from product catalog |
| **EEA** | European Economic Area — GDPR jurisdiction |
| **ICP** | Ideal Customer Profile — description of best-fit customer |
| **LTV** | Lifetime Value — total revenue from a customer over time |
| **MCP** | Model Context Protocol — standardized AI tool integration |
| **PMax** | Performance Max — Google's AI-driven campaign type |
| **ROAS** | Return On Ad Spend — conversion value / spend |
| **RSA** | Responsive Search Ad — Google's AI-assembled text ads |
| **tCPA** | Target CPA — bidding strategy targeting specific CPA |
| **tROAS** | Target ROAS — bidding strategy targeting specific ROAS |
| **UGC** | User-Generated Content — content created by real users |
| **UTM** | Urchin Tracking Module — URL parameters for attribution |
| **VBB** | Value-Based Bidding — bidding optimized for conversion value |

---

*End of SKILL.md — Multi-Platform Ad Campaign Automation v2026.08.1*
