# SKILLS: Бизнес-агенты — CRM, Proposal, Scout, Coordinator
# Содержит: ar-business-growth/contract-and-proposal-writer, revenue-operations, customer-success-manager, marketing-skills/cold-email, customer-research, ar-project-management/senior-pm, ar-c-level-advisor/ceo-advisor, meeting-insights-analyzer

---
## SKILL: ar-business-growth/contract-and-proposal-writer

---
name: "contract-and-proposal-writer"
description: "Contract & Proposal Writer"
---

# Contract & Proposal Writer

**Tier:** POWERFUL  
**Category:** Business Growth  
**Domain:** Legal Documents, Business Development, Client Relations

---

## Overview

Generate professional, jurisdiction-aware business documents: freelance contracts, project proposals, SOWs, NDAs, and MSAs. Outputs structured Markdown with docx conversion instructions. Covers US (Delaware), EU (GDPR), UK, and DACH (German law) jurisdictions.

**Not a substitute for legal counsel.** Use these templates as strong starting points; review with an attorney for high-value or complex engagements.

---

## Core Capabilities

- Freelance development contracts (fixed-price & hourly)
- Project proposals with timeline/budget breakdown
- Statements of Work (SOW) with deliverables matrix
- NDAs (mutual & one-way)
- Master Service Agreements (MSA)
- Jurisdiction-specific clauses (US/EU/UK/DACH)
- GDPR Data Processing Addenda (EU/DACH)

---

## Key Clauses Reference

| Clause | Options |
|--------|---------|
| Payment terms | Net-30, milestone-based, monthly retainer |
| IP ownership | Work-for-hire (US), assignment (EU/UK), license-back |
| Liability cap | 1x contract value (standard), 3x (high-risk) |
| Termination | For cause (14-day cure), convenience (30/60/90-day notice) |
| Confidentiality | 2-5 year term, perpetual for trade secrets |
| Warranty | "As-is" disclaimer, limited 30/90-day fix warranty |
| Dispute resolution | Arbitration (AAA/ICC), courts (jurisdiction-specific) |

---

## When to Use

- Starting a new client engagement and need a contract fast
- Client asks for a proposal with pricing and timeline
- Partnership or vendor relationship requiring an MSA
- Protecting IP or confidential information with an NDA
- EU/DACH project requiring GDPR-compliant data clauses

---

## Workflow

### 1. Gather Requirements

Ask the user:

    1. Document type? (contract / proposal / SOW / NDA / MSA)
    2. Jurisdiction? (US-Delaware / EU / UK / DACH)
    3. Engagement type? (fixed-price / hourly / retainer)
    4. Parties? (names, roles, business addresses)
    5. Scope summary? (1-3 sentences)
    6. Total value or hourly rate?
    7. Start date / end date or duration?
    8. Special requirements? (IP assignment, white-label, subcontractors)

### 2. Select Template

| Type | Jurisdiction | Template |
|------|-------------|----------|
| Dev contract fixed | Any | Template A |
| Consulting retainer | Any | Template B |
| SaaS partnership | Any | Template C |
| NDA mutual | US/EU/UK/DACH | NDA-M |
| NDA one-way | US/EU/UK/DACH | NDA-OW |
| SOW | Any | SOW base |

### 3. Generate & Fill

Fill all [BRACKETED] placeholders. Flag missing data as "REQUIRED".

### 4. Convert to DOCX

```bash
# Install pandoc
brew install pandoc        # macOS
apt install pandoc         # Ubuntu

# Basic conversion
pandoc contract.md -o contract.docx \
  --reference-doc=reference.docx \
  -V geometry:margin=1in

# With numbered sections (legal style)
pandoc contract.md -o contract.docx \
  --number-sections \
  -V documentclass=article \
  -V fontsize=11pt

# With custom company template
pandoc contract.md -o contract.docx \
  --reference-doc=company-template.docx
```

---

## Jurisdiction Notes

### US (Delaware)
- Governing law: State of Delaware
- Work-for-hire doctrine applies (Copyright Act 101)
- Arbitration: AAA Commercial Rules
- Non-compete: enforceable with reasonable scope/time

### EU (GDPR)
- Must include Data Processing Addendum if handling personal data
- IP assignment requires separate written deed in some member states
- Arbitration: ICC or local chamber

### UK (post-Brexit)
- Governed by English law
- IP: Patents Act 1977 / CDPA 1988
- Arbitration: LCIA Rules
- Data: UK GDPR (post-Brexit equivalent)

### DACH (Germany / Austria / Switzerland)
- BGB (Buergerliches Gesetzbuch) governs contracts
- Written form requirement for certain clauses (para 126 BGB)
- IP: Author always retains moral rights; must explicitly transfer Nutzungsrechte
- Non-competes: max 2 years, compensation required (para 74 HGB)
- Jurisdiction: German courts (Landgericht) or DIS arbitration
- DSGVO (GDPR implementation) mandatory for personal data processing
- Kuendigungsfristen: statutory notice periods apply

---

## Template A: Web Dev Fixed-Price Contract

```markdown
# SOFTWARE DEVELOPMENT AGREEMENT

**Effective Date:** [DATE]
**Client:** [CLIENT LEGAL NAME], [ADDRESS] ("Client")
**Developer:** [YOUR LEGAL NAME / COMPANY], [ADDRESS] ("Developer")

---

## 1. SERVICES

Developer agrees to design, develop, and deliver:

**Project:** [PROJECT NAME]
**Description:** [1-3 sentence scope]

**Deliverables:**
- [Deliverable 1] due [DATE]
- [Deliverable 2] due [DATE]
- [Deliverable 3] due [DATE]

## 2. PAYMENT

**Total Fee:** [CURRENCY] [AMOUNT]

| Milestone | Amount | Due |
|-----------|--------|-----|
| Contract signing | 50% | Upon execution |
| Beta delivery | 25% | [DATE] |
| Final acceptance | 25% | Within 5 days of acceptance |

Late payments accrue interest at 1.5% per month.
Client has [10] business days to accept or reject deliverables in writing.

## 3. INTELLECTUAL PROPERTY

Upon receipt of full payment, Developer assigns all right, title, and interest in the
Work Product to Client as a work made for hire (US) / by assignment of future copyright (EU/UK).

Developer retains the right to display Work Product in portfolio unless Client
requests confidentiality in writing within [30] days of delivery.

Pre-existing IP (tools, libraries, frameworks) remains Developer's property.
Developer grants Client a perpetual, royalty-free license to use pre-existing IP
as embedded in the Work Product.

## 4. CONFIDENTIALITY

Each party keeps confidential all non-public information received from the other.
This obligation survives termination for [3] years.

## 5. WARRANTIES

Developer warrants Work Product will substantially conform to specifications for
[90] days post-delivery. Developer will fix material defects at no charge during
this period. EXCEPT AS STATED, WORK PRODUCT IS PROVIDED "AS IS."

## 6. LIABILITY

Developer's total liability shall not exceed total fees paid under this Agreement.
Neither party liable for indirect, incidental, or consequential damages.

## 7. TERMINATION

For Cause: Either party may terminate if the other materially breaches and fails
to cure within [14] days of written notice.

For Convenience: Client may terminate with [30] days written notice and pay for
all work completed plus [10%] of remaining contract value.

## 8. DISPUTE RESOLUTION

US: Binding arbitration under AAA Commercial Rules, [CITY], Delaware law.
EU/DACH: ICC / DIS arbitration, [CITY]. German / English law.
UK: LCIA Rules, London. English law.

## 9. GENERAL

- Entire Agreement: Supersedes all prior discussions.
- Amendments: Must be in writing, signed by both parties.
- Independent Contractor: Developer is not an employee of Client.

---

CLIENT: _________________________ Date: _________
[CLIENT NAME], [TITLE]

DEVELOPER: _________________________ Date: _________
[YOUR NAME], [TITLE]
```

---

## Template B: Monthly Consulting Retainer

```markdown
# CONSULTING RETAINER AGREEMENT

**Effective Date:** [DATE]
**Client:** [CLIENT LEGAL NAME] ("Client")
**Consultant:** [YOUR NAME / COMPANY] ("Consultant")

---

## 1. SERVICES

Consultant provides [DOMAIN, e.g., "CTO advisory and technical architecture"] services.

**Monthly Hours:** Up to [X] hours/month
**Rollover:** Unused hours [do / do not] roll over (max [X] hours banked)
**Overflow Rate:** [CURRENCY] [RATE]/hr for hours exceeding retainer

## 2. FEES

**Monthly Retainer:** [CURRENCY] [AMOUNT], due on the 1st of each month.
**Payment Method:** Bank transfer / Stripe / SEPA direct debit
**Late Payment:** 2% monthly interest after [10]-day grace period.

## 3. TERM AND TERMINATION

**Initial Term:** [3] months starting [DATE]
**Renewal:** Auto-renews monthly unless either party gives [30] days written notice.
**Immediate termination:** For material breach uncured after [7] days notice.

On termination, Consultant delivers all work in progress within [5] business days.

## 4. INTELLECTUAL PROPERTY

Work product created under this Agreement belongs to [Client / Consultant / jointly].
Advisory output (recommendations, analyses) are Client property upon full payment.

## 5. EXCLUSIVITY

[OPTION A - Non-exclusive:]
This Agreement is non-exclusive. Consultant may work with other clients.

[OPTION B - Partial exclusivity:]
Consultant will not work with direct competitors of Client during the term
and [90] days thereafter.

## 6. CONFIDENTIALITY AND DATA PROTECTION

EU/DACH: If Consultant processes personal data on behalf of Client, the parties
shall execute a Data Processing Agreement (DPA) per Art. 28 GDPR.

## 7. LIABILITY

Consultant's aggregate liability is capped at [3x] the fees paid in the [3] months
preceding the claim.

---

Signatures as above.
```

---

## Template C: SaaS Partnership Agreement

```markdown
# SAAS PARTNERSHIP AGREEMENT

**Effective Date:** [DATE]
**Provider:** [NAME], [ADDRESS]
**Partner:** [NAME], [ADDRESS]

---

## 1. PURPOSE

Provider grants Partner [reseller / referral / white-label / integration] rights to
Provider's [PRODUCT NAME] ("Software") subject to this Agreement.

## 2. PARTNERSHIP TYPE

[ ] Referral: Partner refers customers; earns [X%] of first-year ARR per referral.
[ ] Reseller: Partner resells licenses; earns [X%] discount off list price.
[ ] White-label: Partner rebrands Software; pays [AMOUNT]/month platform fee.
[ ] Integration: Partner integrates Software via API; terms in Exhibit A.

## 3. REVENUE SHARE

| Tier | Monthly ARR Referred | Commission |
|------|---------------------|------------|
| Bronze | < $10,000 | [X]% |
| Silver | $10,000-$50,000 | [X]% |
| Gold | > $50,000 | [X]% |

Payout: Net-30 after month close, minimum $[500] threshold.

## 4. INTELLECTUAL PROPERTY

Each party retains all IP in its own products. No implied licenses.
Partner may use Provider's marks per Provider's Brand Guidelines (Exhibit B).

## 5. DATA AND PRIVACY

Each party is an independent data controller for its own customers.
Joint processing requires a separate DPA (Exhibit C - EU/DACH projects).

## 6. TERM

Initial: [12] months. Renews annually unless [90]-day written notice given.
Termination for Cause: [30]-day cure period for material breach.

## 7. LIMITATION OF LIABILITY

Each party's liability capped at [1x] fees paid/received in prior [12] months.
Mutual indemnification for IP infringement claims from own products.

---

Signatures, exhibits, and governing law per applicable jurisdiction.
```

---

## GDPR Data Processing Addendum (EU/DACH Clause Block)

```markdown
## DATA PROCESSING ADDENDUM (Art. 28 GDPR)

Controller: [CLIENT NAME]
Processor: [CONTRACTOR NAME]

### Subject Matter
Processor processes personal data on behalf of Controller solely to perform services
under the main Agreement.

### Categories of Data Subjects
[e.g., end users, employees, customers]

### Categories of Personal Data
[e.g., names, email addresses, usage data]

### Processing Duration
For the term of the main Agreement; deletion within [30] days of termination.

### Processor Obligations
- Process data only on Controller's documented instructions
- Ensure persons authorized to process have committed to confidentiality
- Implement technical and organizational measures per Art. 32 GDPR
- Assist Controller with data subject rights requests
- Not engage sub-processors without prior written consent
- Delete or return all personal data upon termination

### Sub-processors (current as of Effective Date)
| Sub-processor | Location | Purpose |
|--------------|----------|---------|
| [AWS / GCP / Azure] | [Region] | Cloud hosting |
| [Other] | [Location] | [Purpose] |

### Cross-border Transfers
Data transfers outside EEA covered by: [ ] SCCs  [ ] Adequacy Decision  [ ] BCRs
```

---

## Common Pitfalls

1. **Missing IP assignment language** - "work for hire" alone is insufficient in EU; need explicit assignment of Nutzungsrechte in DACH
2. **Vague acceptance criteria** - Always define what "accepted" means (written sign-off, X days to reject)
3. **No change order process** - Scope creep kills fixed-price projects; add a clause for out-of-scope work
4. **Jurisdiction mismatch** - Choosing Delaware law for a German-only project creates enforcement problems
5. **Missing limitation of liability** - Without a cap, one bug could mean unlimited damages
6. **Oral amendments** - Contracts modified verbally are hard to enforce; always require written amendments

---

## Best Practices

- Use **milestone payments** over net-30 for projects >$10K - reduces cash flow risk
- For EU/DACH: always check if a DPA is needed (any personal data = yes)
- For DACH: include a **Schriftformklausel** (written form clause) explicitly
- Add a **force majeure** clause for anything over 3 months
- For retainers: define response time SLAs (e.g., 4h urgent / 24h normal)
- Keep templates in version control; track changes with `git diff`
- Review annually - laws change, especially GDPR enforcement interpretations
- For NDAs: always specify the return/destruction of confidential materials on termination

---
## SKILL: ar-business-growth/revenue-operations

---
name: "revenue-operations"
description: Analyzes sales pipeline health, revenue forecasting accuracy, and go-to-market efficiency metrics for SaaS revenue optimization. Use when analyzing sales pipeline coverage, forecasting revenue, evaluating go-to-market performance, reviewing sales metrics, assessing pipeline analysis, tracking forecast accuracy with MAPE, calculating GTM efficiency, or measuring sales efficiency and unit economics for SaaS teams.
---

# Revenue Operations

Pipeline analysis, forecast accuracy tracking, and GTM efficiency measurement for SaaS revenue teams.

> **Output formats:** All scripts support `--format text` (human-readable) and `--format json` (dashboards/integrations).

---

## Quick Start

```bash
# Analyze pipeline health and coverage
python scripts/pipeline_analyzer.py --input assets/sample_pipeline_data.json --format text

# Track forecast accuracy over multiple periods
python scripts/forecast_accuracy_tracker.py assets/sample_forecast_data.json --format text

# Calculate GTM efficiency metrics
python scripts/gtm_efficiency_calculator.py assets/sample_gtm_data.json --format text
```

---

## Tools Overview

### 1. Pipeline Analyzer

Analyzes sales pipeline health including coverage ratios, stage conversion rates, deal velocity, aging risks, and concentration risks.

**Input:** JSON file with deals, quota, and stage configuration
**Output:** Coverage ratios, conversion rates, velocity metrics, aging flags, risk assessment

**Usage:**

```bash
python scripts/pipeline_analyzer.py --input pipeline.json --format text
```

**Key Metrics Calculated:**
- **Pipeline Coverage Ratio** -- Total pipeline value / quota target (healthy: 3-4x)
- **Stage Conversion Rates** -- Stage-to-stage progression rates
- **Sales Velocity** -- (Opportunities x Avg Deal Size x Win Rate) / Avg Sales Cycle
- **Deal Aging** -- Flags deals exceeding 2x average cycle time per stage
- **Concentration Risk** -- Warns when >40% of pipeline is in a single deal
- **Coverage Gap Analysis** -- Identifies quarters with insufficient pipeline

**Input Schema:**

```json
{
  "quota": 500000,
  "stages": ["Discovery", "Qualification", "Proposal", "Negotiation", "Closed Won"],
  "average_cycle_days": 45,
  "deals": [
    {
      "id": "D001",
      "name": "Acme Corp",
      "stage": "Proposal",
      "value": 85000,
      "age_days": 32,
      "close_date": "2025-03-15",
      "owner": "rep_1"
    }
  ]
}
```

### 2. Forecast Accuracy Tracker

Tracks forecast accuracy over time using MAPE, detects systematic bias, analyzes trends, and provides category-level breakdowns.

**Input:** JSON file with forecast periods and optional category breakdowns
**Output:** MAPE score, bias analysis, trends, category breakdown, accuracy rating

**Usage:**

```bash
python scripts/forecast_accuracy_tracker.py forecast_data.json --format text
```

**Key Metrics Calculated:**
- **MAPE** -- mean(|actual - forecast| / |actual|) x 100
- **Forecast Bias** -- Over-forecasting (positive) vs under-forecasting (negative) tendency
- **Weighted Accuracy** -- MAPE weighted by deal value for materiality
- **Period Trends** -- Improving, stable, or declining accuracy over time
- **Category Breakdown** -- Accuracy by rep, product, segment, or any custom dimension

**Accuracy Ratings:**
| Rating | MAPE Range | Interpretation |
|--------|-----------|----------------|
| Excellent | <10% | Highly predictable, data-driven process |
| Good | 10-15% | Reliable forecasting with minor variance |
| Fair | 15-25% | Needs process improvement |
| Poor | >25% | Significant forecasting methodology gaps |

**Input Schema:**

```json
{
  "forecast_periods": [
    {"period": "2025-Q1", "forecast": 480000, "actual": 520000},
    {"period": "2025-Q2", "forecast": 550000, "actual": 510000}
  ],
  "category_breakdowns": {
    "by_rep": [
      {"category": "Rep A", "forecast": 200000, "actual": 210000},
      {"category": "Rep B", "forecast": 280000, "actual": 310000}
    ]
  }
}
```

### 3. GTM Efficiency Calculator

Calculates core SaaS GTM efficiency metrics with industry benchmarking, ratings, and improvement recommendations.

**Input:** JSON file with revenue, cost, and customer metrics
**Output:** Magic Number, LTV:CAC, CAC Payback, Burn Multiple, Rule of 40, NDR with ratings

**Usage:**

```bash
python scripts/gtm_efficiency_calculator.py gtm_data.json --format text
```

**Key Metrics Calculated:**

| Metric | Formula | Target |
|--------|---------|--------|
| Magic Number | Net New ARR / Prior Period S&M Spend | >0.75 |
| LTV:CAC | (ARPA x Gross Margin / Churn Rate) / CAC | >3:1 |
| CAC Payback | CAC / (ARPA x Gross Margin) months | <18 months |
| Burn Multiple | Net Burn / Net New ARR | <2x |
| Rule of 40 | Revenue Growth % + FCF Margin % | >40% |
| Net Dollar Retention | (Begin ARR + Expansion - Contraction - Churn) / Begin ARR | >110% |

**Input Schema:**

```json
{
  "revenue": {
    "current_arr": 5000000,
    "prior_arr": 3800000,
    "net_new_arr": 1200000,
    "arpa_monthly": 2500,
    "revenue_growth_pct": 31.6
  },
  "costs": {
    "sales_marketing_spend": 1800000,
    "cac": 18000,
    "gross_margin_pct": 78,
    "total_operating_expense": 6500000,
    "net_burn": 1500000,
    "fcf_margin_pct": 8.4
  },
  "customers": {
    "beginning_arr": 3800000,
    "expansion_arr": 600000,
    "contraction_arr": 100000,
    "churned_arr": 300000,
    "annual_churn_rate_pct": 8
  }
}
```

---

## Revenue Operations Workflows

### Weekly Pipeline Review

Use this workflow for your weekly pipeline inspection cadence.

1. **Verify input data:** Confirm pipeline export is current and all required fields (stage, value, close_date, owner) are populated before proceeding.

2. **Generate pipeline report:**
   ```bash
   python scripts/pipeline_analyzer.py --input current_pipeline.json --format text
   ```

3. **Cross-check output totals** against your CRM source system to confirm data integrity.

4. **Review key indicators:**
   - Pipeline coverage ratio (is it above 3x quota?)
   - Deals aging beyond threshold (which deals need intervention?)
   - Concentration risk (are we over-reliant on a few large deals?)
   - Stage distribution (is there a healthy funnel shape?)

5. **Document using template:** Use `assets/pipeline_review_template.md`

6. **Action items:** Address aging deals, redistribute pipeline concentration, fill coverage gaps

### Forecast Accuracy Review

Use monthly or quarterly to evaluate and improve forecasting discipline.

1. **Verify input data:** Confirm all forecast periods have corresponding actuals and no periods are missing before running.

2. **Generate accuracy report:**
   ```bash
   python scripts/forecast_accuracy_tracker.py forecast_history.json --format text
   ```

3. **Cross-check actuals** against closed-won records in your CRM before drawing conclusions.

4. **Analyze patterns:**
   - Is MAPE trending down (improving)?
   - Which reps or segments have the highest error rates?
   - Is there systematic over- or under-forecasting?

5. **Document using template:** Use `assets/forecast_report_template.md`

6. **Improvement actions:** Coach high-bias reps, adjust methodology, improve data hygiene

### GTM Efficiency Audit

Use quarterly or during board prep to evaluate go-to-market efficiency.

1. **Verify input data:** Confirm revenue, cost, and customer figures reconcile with finance records before running.

2. **Calculate efficiency metrics:**
   ```bash
   python scripts/gtm_efficiency_calculator.py quarterly_data.json --format text
   ```

3. **Cross-check computed ARR and spend totals** against your finance system before sharing results.

4. **Benchmark against targets:**
   - Magic Number (>0.75)
   - LTV:CAC (>3:1)
   - CAC Payback (<18 months)
   - Rule of 40 (>40%)

5. **Document using template:** Use `assets/gtm_dashboard_template.md`

6. **Strategic decisions:** Adjust spend allocation, optimize channels, improve retention

### Quarterly Business Review

Combine all three tools for a comprehensive QBR analysis.

1. Run pipeline analyzer for forward-looking coverage
2. Run forecast tracker for backward-looking accuracy
3. Run GTM calculator for efficiency benchmarks
4. Cross-reference pipeline health with forecast accuracy
5. Align GTM efficiency metrics with growth targets

---

## Reference Documentation

| Reference | Description |
|-----------|-------------|
| [RevOps Metrics Guide](references/revops-metrics-guide.md) | Complete metrics hierarchy, definitions, formulas, and interpretation |
| [Pipeline Management Framework](references/pipeline-management-framework.md) | Pipeline best practices, stage definitions, conversion benchmarks |
| [GTM Efficiency Benchmarks](references/gtm-efficiency-benchmarks.md) | SaaS benchmarks by stage, industry standards, improvement strategies |

---

## Templates

| Template | Use Case |
|----------|----------|
| [Pipeline Review Template](assets/pipeline_review_template.md) | Weekly/monthly pipeline inspection documentation |
| [Forecast Report Template](assets/forecast_report_template.md) | Forecast accuracy reporting and trend analysis |
| [GTM Dashboard Template](assets/gtm_dashboard_template.md) | GTM efficiency dashboard for leadership review |
| [Sample Pipeline Data](assets/sample_pipeline_data.json) | Example input for pipeline_analyzer.py |
| [Expected Output](assets/expected_output.json) | Reference output from pipeline_analyzer.py |

---
## SKILL: ar-business-growth/customer-success-manager

---
name: "customer-success-manager"
description: Monitors customer health, predicts churn risk, and identifies expansion opportunities using weighted scoring models for SaaS customer success. Use when analyzing customer accounts, reviewing retention metrics, scoring at-risk customers, or when the user mentions churn, customer health scores, upsell opportunities, expansion revenue, retention analysis, or customer analytics. Runs three Python CLI tools to produce deterministic health scores, churn risk tiers, and prioritized expansion recommendations across Enterprise, Mid-Market, and SMB segments.
license: MIT
metadata:
  version: 1.0.0
  author: Alireza Rezvani
  category: business-growth
  domain: customer-success
  updated: 2026-02-06
  python-tools: health_score_calculator.py, churn_risk_analyzer.py, expansion_opportunity_scorer.py
  tech-stack: customer-success, saas-metrics, health-scoring
---

# Customer Success Manager

Production-grade customer success analytics with multi-dimensional health scoring, churn risk prediction, and expansion opportunity identification. Three Python CLI tools provide deterministic, repeatable analysis using standard library only -- no external dependencies, no API calls, no ML models.

---

## Table of Contents

- [Input Requirements](#input-requirements)
- [Output Formats](#output-formats)
- [How to Use](#how-to-use)
- [Scripts](#scripts)
- [Reference Guides](#reference-guides)
- [Templates](#templates)
- [Best Practices](#best-practices)
- [Limitations](#limitations)

---

## Input Requirements

All scripts accept a JSON file as positional input argument. See `assets/sample_customer_data.json` for complete schema examples and sample data.

### Health Score Calculator

Required fields per customer object: `customer_id`, `name`, `segment`, `arr`, and nested objects `usage` (login_frequency, feature_adoption, dau_mau_ratio), `engagement` (support_ticket_volume, meeting_attendance, nps_score, csat_score), `support` (open_tickets, escalation_rate, avg_resolution_hours), `relationship` (executive_sponsor_engagement, multi_threading_depth, renewal_sentiment), and `previous_period` scores for trend analysis.

### Churn Risk Analyzer

Required fields per customer object: `customer_id`, `name`, `segment`, `arr`, `contract_end_date`, and nested objects `usage_decline`, `engagement_drop`, `support_issues`, `relationship_signals`, and `commercial_factors`.

### Expansion Opportunity Scorer

Required fields per customer object: `customer_id`, `name`, `segment`, `arr`, and nested objects `contract` (licensed_seats, active_seats, plan_tier, available_tiers), `product_usage` (per-module adoption flags and usage percentages), and `departments` (current and potential).

---

## Output Formats

All scripts support two output formats via the `--format` flag:

- **`text`** (default): Human-readable formatted output for terminal viewing
- **`json`**: Machine-readable JSON output for integrations and pipelines

---

## How to Use

### Quick Start

```bash
# Health scoring
python scripts/health_score_calculator.py assets/sample_customer_data.json
python scripts/health_score_calculator.py assets/sample_customer_data.json --format json

# Churn risk analysis
python scripts/churn_risk_analyzer.py assets/sample_customer_data.json
python scripts/churn_risk_analyzer.py assets/sample_customer_data.json --format json

# Expansion opportunity scoring
python scripts/expansion_opportunity_scorer.py assets/sample_customer_data.json
python scripts/expansion_opportunity_scorer.py assets/sample_customer_data.json --format json
```

### Workflow Integration

```bash
# 1. Score customer health across portfolio
python scripts/health_score_calculator.py customer_portfolio.json --format json > health_results.json
# Verify: confirm health_results.json contains the expected number of customer records before continuing

# 2. Identify at-risk accounts
python scripts/churn_risk_analyzer.py customer_portfolio.json --format json > risk_results.json
# Verify: confirm risk_results.json is non-empty and risk tiers are present for each customer

# 3. Find expansion opportunities in healthy accounts
python scripts/expansion_opportunity_scorer.py customer_portfolio.json --format json > expansion_results.json
# Verify: confirm expansion_results.json lists opportunities ranked by priority

# 4. Prepare QBR using templates
# Reference: assets/qbr_template.md
```

**Error handling:** If a script exits with an error, check that:
- The input JSON matches the required schema for that script (see Input Requirements above)
- All required fields are present and correctly typed
- Python 3.7+ is being used (`python --version`)
- Output files from prior steps are non-empty before piping into subsequent steps

---

## Scripts

### 1. health_score_calculator.py

**Purpose:** Multi-dimensional customer health scoring with trend analysis and segment-aware benchmarking.

**Dimensions and Weights:**
| Dimension | Weight | Metrics |
|-----------|--------|---------|
| Usage | 30% | Login frequency, feature adoption, DAU/MAU ratio |
| Engagement | 25% | Support ticket volume, meeting attendance, NPS/CSAT |
| Support | 20% | Open tickets, escalation rate, avg resolution time |
| Relationship | 25% | Executive sponsor engagement, multi-threading depth, renewal sentiment |

**Classification:**
- Green (75-100): Healthy -- customer achieving value
- Yellow (50-74): Needs attention -- monitor closely
- Red (0-49): At risk -- immediate intervention required

**Usage:**
```bash
python scripts/health_score_calculator.py customer_data.json
python scripts/health_score_calculator.py customer_data.json --format json
```

### 2. churn_risk_analyzer.py

**Purpose:** Identify at-risk accounts with behavioral signal detection and tier-based intervention recommendations.

**Risk Signal Weights:**
| Signal Category | Weight | Indicators |
|----------------|--------|------------|
| Usage Decline | 30% | Login trend, feature adoption change, DAU/MAU change |
| Engagement Drop | 25% | Meeting cancellations, response time, NPS change |
| Support Issues | 20% | Open escalations, unresolved critical, satisfaction trend |
| Relationship Signals | 15% | Champion left, sponsor change, competitor mentions |
| Commercial Factors | 10% | Contract type, pricing complaints, budget cuts |

**Risk Tiers:**
- Critical (80-100): Immediate executive escalation
- High (60-79): Urgent CSM intervention
- Medium (40-59): Proactive outreach
- Low (0-39): Standard monitoring

**Usage:**
```bash
python scripts/churn_risk_analyzer.py customer_data.json
python scripts/churn_risk_analyzer.py customer_data.json --format json
```

### 3. expansion_opportunity_scorer.py

**Purpose:** Identify upsell, cross-sell, and expansion opportunities with revenue estimation and priority ranking.

**Expansion Types:**
- **Upsell**: Upgrade to higher tier or more of existing product
- **Cross-sell**: Add new product modules
- **Expansion**: Additional seats or departments

**Usage:**
```bash
python scripts/expansion_opportunity_scorer.py customer_data.json
python scripts/expansion_opportunity_scorer.py customer_data.json --format json
```

---

## Reference Guides

| Reference | Description |
|-----------|-------------|
| `references/health-scoring-framework.md` | Complete health scoring methodology, dimension definitions, weighting rationale, threshold calibration |
| `references/cs-playbooks.md` | Intervention playbooks for each risk tier, onboarding, renewal, expansion, and escalation procedures |
| `references/cs-metrics-benchmarks.md` | Industry benchmarks for NRR, GRR, churn rates, health scores, expansion rates by segment and industry |

---

## Templates

| Template | Purpose |
|----------|---------|
| `assets/qbr_template.md` | Quarterly Business Review presentation structure |
| `assets/success_plan_template.md` | Customer success plan with goals, milestones, and metrics |
| `assets/onboarding_checklist_template.md` | 90-day onboarding checklist with phase gates |
| `assets/executive_business_review_template.md` | Executive stakeholder review for strategic accounts |

---

## Best Practices

1. **Combine signals**: Use all three scripts together for a complete customer picture
2. **Act on trends, not snapshots**: A declining Green is more urgent than a stable Yellow
3. **Calibrate thresholds**: Adjust segment benchmarks based on your product and industry per `references/health-scoring-framework.md`
4. **Prepare with data**: Run scripts before every QBR and executive meeting; reference `references/cs-playbooks.md` for intervention guidance

---

## Limitations

- **No real-time data**: Scripts analyze point-in-time snapshots from JSON input files
- **No CRM integration**: Data must be exported manually from your CRM/CS platform
- **Deterministic only**: No predictive ML -- scoring is algorithmic based on weighted signals
- **Threshold tuning**: Default thresholds are industry-standard but may need calibration for your business
- **Revenue estimates**: Expansion revenue estimates are approximations based on usage patterns

---

**Last Updated:** February 2026
**Tools:** 3 Python CLI tools
**Dependencies:** Python 3.7+ standard library only

---
## SKILL: marketing-skills/cold-email

---
name: cold-email
description: Write B2B cold emails and follow-up sequences that get replies. Use when the user wants to write cold outreach emails, prospecting emails, cold email campaigns, sales development emails, or SDR emails. Also use when the user mentions "cold outreach," "prospecting email," "outbound email," "email to leads," "reach out to prospects," "sales email," "follow-up email sequence," "nobody's replying to my emails," or "how do I write a cold email." Covers subject lines, opening lines, body copy, CTAs, personalization, and multi-touch follow-up sequences. For warm/lifecycle email sequences, see email-sequence. For sales collateral beyond emails, see sales-enablement.
metadata:
  version: 1.1.0
---

# Cold Email Writing

You are an expert cold email writer. Your goal is to write emails that sound like they came from a sharp, thoughtful human — not a sales machine following a template.

## Before Writing

**Check for product marketing context first:**
If `.agents/product-marketing-context.md` exists (or `.claude/product-marketing-context.md` in older setups), read it before asking questions. Use that context and only ask for information not already covered or specific to this task.

Understand the situation (ask if not provided):

1. **Who are you writing to?** — Role, company, why them specifically
2. **What do you want?** — The outcome (meeting, reply, intro, demo)
3. **What's the value?** — The specific problem you solve for people like them
4. **What's your proof?** — A result, case study, or credibility signal
5. **Any research signals?** — Funding, hiring, LinkedIn posts, company news, tech stack changes

Work with whatever the user gives you. If they have a strong signal and a clear value prop, that's enough to write. Don't block on missing inputs — use what you have and note what would make it stronger.

---

## Writing Principles

### Write like a peer, not a vendor

The email should read like it came from someone who understands their world — not someone trying to sell them something. Use contractions. Read it aloud. If it sounds like marketing copy, rewrite it.

### Every sentence must earn its place

Cold email is ruthlessly short. If a sentence doesn't move the reader toward replying, cut it. The best cold emails feel like they could have been shorter, not longer.

### Personalization must connect to the problem

If you remove the personalized opening and the email still makes sense, the personalization isn't working. The observation should naturally lead into why you're reaching out.

See [personalization.md](references/personalization.md) for the 4-level system and research signals.

### Lead with their world, not yours

The reader should see their own situation reflected back. "You/your" should dominate over "I/we." Don't open with who you are or what your company does.

### One ask, low friction

Interest-based CTAs ("Worth exploring?" / "Would this be useful?") beat meeting requests. One CTA per email. Make it easy to say yes with a one-line reply.

---

## Voice & Tone

**The target voice:** A smart colleague who noticed something relevant and is sharing it. Conversational but not sloppy. Confident but not pushy.

**Calibrate to the audience:**

- C-suite: ultra-brief, peer-level, understated
- Mid-level: more specific value, slightly more detail
- Technical: precise, no fluff, respect their intelligence

**What it should NOT sound like:**

- A template with fields swapped in
- A pitch deck compressed into paragraph form
- A LinkedIn DM from someone you've never met
- An AI-generated email (avoid the telltale patterns: "I hope this email finds you well," "I came across your profile," "leverage," "synergy," "best-in-class")

---

## Structure

There's no single right structure. Choose a framework that fits the situation, or write freeform if the email flows naturally without one.

**Common shapes that work:**

- **Observation → Problem → Proof → Ask** — You noticed X, which usually means Y challenge. We helped Z with that. Interested?
- **Question → Value → Ask** — Struggling with X? We do Y. Company Z saw [result]. Worth a look?
- **Trigger → Insight → Ask** — Congrats on X. That usually creates Y challenge. We've helped similar companies with that. Curious?
- **Story → Bridge → Ask** — [Similar company] had [problem]. They [solved it this way]. Relevant to you?

For the full catalog of frameworks with examples, see [frameworks.md](references/frameworks.md).

---

## Subject Lines

Short, boring, internal-looking. The subject line's only job is to get the email opened — not to sell.

- 2-4 words, lowercase, no punctuation tricks
- Should look like it came from a colleague ("reply rates," "hiring ops," "Q2 forecast")
- No product pitches, no urgency, no emojis, no prospect's first name

See [subject-lines.md](references/subject-lines.md) for the full data.

---

## Follow-Up Sequences

Each follow-up should add something new — a different angle, fresh proof, a useful resource. "Just checking in" gives the reader no reason to respond.

- 3-5 total emails, increasing gaps between them
- Each email should stand alone (they may not have read the previous ones)
- The breakup email is your last touch — honor it

See [follow-up-sequences.md](references/follow-up-sequences.md) for cadence, angle rotation, and breakup email templates.

---

## Quality Check

Before presenting, gut-check:

- Does it sound like a human wrote it? (Read it aloud)
- Would YOU reply to this if you received it?
- Does every sentence serve the reader, not the sender?
- Is the personalization connected to the problem?
- Is there one clear, low-friction ask?

---

## What to Avoid

- Opening with "I hope this email finds you well" or "My name is X and I work at Y"
- Jargon: "synergy," "leverage," "circle back," "best-in-class," "leading provider"
- Feature dumps — one proof point beats ten features
- HTML, images, or multiple links
- Fake "Re:" or "Fwd:" subject lines
- Identical templates with only {{FirstName}} swapped
- Asking for 30-minute calls in first touch
- "Just checking in" follow-ups

---

## Data & Benchmarks

The references contain performance data if you need to make informed choices:

- [benchmarks.md](references/benchmarks.md) — Reply rates, conversion funnels, expert methods, common mistakes
- [personalization.md](references/personalization.md) — 4-level personalization system, research signals
- [subject-lines.md](references/subject-lines.md) — Subject line data and optimization
- [follow-up-sequences.md](references/follow-up-sequences.md) — Cadence, angles, breakup emails
- [frameworks.md](references/frameworks.md) — All copywriting frameworks with examples

Use this data to inform your writing — not as a checklist to satisfy.

---

## Related Skills

- **copywriting**: For landing pages and web copy
- **email-sequence**: For lifecycle/nurture email sequences (not cold outreach)
- **social-content**: For LinkedIn and social posts
- **product-marketing-context**: For establishing foundational positioning
- **revops**: For lead scoring, routing, and pipeline management

---
## SKILL: marketing-skills/customer-research

---
name: customer-research
description: When the user wants to conduct, analyze, or synthesize customer research. Use when the user mentions "customer research," "ICP research," "talk to customers," "analyze transcripts," "customer interviews," "survey analysis," "support ticket analysis," "voice of customer," "VOC," "build personas," "customer personas," "jobs to be done," "JTBD," "what do customers say," "what are customers struggling with," "Reddit mining," "G2 reviews," "review mining," "digital watering holes," "community research," "forum research," "competitor reviews," "customer sentiment," or "find out why customers churn/convert/buy." Use for both analyzing existing research assets AND gathering new research from online sources. For writing copy informed by research, see copywriting. For acting on research to improve pages, see page-cro.
metadata:
  version: 1.0.0
---

# Customer Research

You are an expert customer researcher. Your goal is to help uncover what customers actually think, feel, say, and struggle with — so that everything from positioning to product to copy is grounded in reality rather than assumption.

## Before Starting

**Check for product marketing context first:**
If `.agents/product-marketing-context.md` exists (or `.claude/product-marketing-context.md` in older setups), read it before asking questions. Use that context to skip questions already answered.

---

## Two Modes of Research

### Mode 1: Analyze Existing Assets
You have raw research material (transcripts, surveys, reviews, tickets). Your job is to extract signal.

### Mode 2: Go Find Research
You need to gather intel from online sources (Reddit, G2, forums, communities, review sites). Your job is to know where to look and what to extract.

Most engagements combine both. Establish which mode applies before proceeding.

---

## Mode 1: Analyzing Existing Research Assets

### Asset Types

**Customer interview / sales call transcripts**
- Extract: pains, triggers, desired outcomes, language used, objections, alternatives considered
- Look for: the moment they decided to look for a solution, what they tried before, what success looks like to them

**Survey results**
- Segment responses by customer tier, use case, or tenure before drawing conclusions
- Flag: what open-ended answers say vs. what multiple-choice answers say (they often conflict)
- Identify: the 20% of responses that contain the most useful signal

**Customer support conversations**
- Mine for: recurring complaints, confusion points, feature requests, and "I wish it could…" language
- Categorize tickets before analyzing — don't treat all tickets as equal signal
- Separate bugs from confusion from missing features from expectation mismatches

**Win/loss interviews and churned customer notes**
- Wins: what tipped the decision? What almost made them choose a competitor?
- Losses and churn: was it price, features, fit, timing, or something else?
- Segment by reason — don't average across different churn causes

**NPS responses**
- Passives and detractors are higher signal than promoters for improvement work
- Pair scores with verbatims — a 9 with a specific complaint beats a 10 with no comment

### Extraction Framework

For each asset, extract:

1. **Jobs to Be Done** — what outcome is the customer trying to achieve?
   - Functional job: the task itself
   - Emotional job: how they want to feel
   - Social job: how they want to be perceived

2. **Pain Points** — what's frustrating, broken, or inadequate about their current situation?
   - Prioritize pains mentioned unprompted and with emotional language

3. **Trigger Events** — what changed that made them seek a solution?
   - Common triggers: team growth, new hire, missed target, embarrassing incident, competitor doing something

4. **Desired Outcomes** — what does success look like in their words?
   - Capture exact quotes, not paraphrases

5. **Language and Vocabulary** — exact words and phrases customers use
   - This is gold for copy. "We were drowning in spreadsheets" > "manual process inefficiency"

6. **Alternatives Considered** — what else did they look at or try?
   - Includes doing nothing, hiring someone, or building internally

### Synthesis Steps

After extracting from individual assets:

1. **Cluster by theme** — group similar pains, outcomes, and triggers across assets
2. **Frequency + intensity scoring** — how often does a theme appear, and how strongly is it felt?
3. **Segment by customer profile** — do patterns differ by company size, role, use case, or tenure?
4. **Identify the "money quotes"** — 5-10 verbatim quotes that best represent each theme
5. **Flag contradictions** — where do customers say one thing but do another?

### Research Quality Guardrails

Label every insight with a confidence level before presenting it:

| Confidence | Criteria |
|------------|----------|
| **High** | Theme appears in 3+ independent sources; mentioned unprompted; consistent across segments |
| **Medium** | Theme appears in 2 sources, or only prompted, or limited to one segment |
| **Low** | Single source; could be an outlier; needs validation |

**Recency window**: Weight sources from the last 12 months more heavily. Markets shift — a 3-year-old transcript may reflect a different product and buyer.

**Sample bias checks**:
- Online reviewers skew toward power users and people with strong opinions
- Support tickets skew toward problems, not value
- Reddit skews technical and skeptical vs. mainstream buyers
- Factor this in when drawing conclusions about "all customers"

**Minimum viable sample**: Don't build personas or draw messaging conclusions from fewer than 5 independent data points per segment.

---

## Mode 2: Digital Watering Hole Research

Online communities are where customers speak without a filter. The goal is to find authentic, unmoderated language about the problem space.

### Where to Look

Choose sources based on your ICP type — then read `references/source-guides.md` for detailed playbooks, search operators, and per-platform extraction tips.

| ICP Type | Primary Sources |
|----------|----------------|
| B2B SaaS / technical buyers | Reddit (role-specific subs), G2/Capterra, Hacker News, LinkedIn, Indie Hackers, SparkToro |
| SMB / founders | Reddit (r/entrepreneur, r/smallbusiness), Indie Hackers, Product Hunt, Facebook Groups, SparkToro |
| Developer / DevOps | r/devops, r/programming, Hacker News, Stack Overflow, Discord servers |
| B2C / consumer | App store reviews (1-3 star), Reddit hobby/lifestyle subs, YouTube comments, TikTok/Instagram comments |
| Enterprise | LinkedIn, industry analyst reports, G2 Enterprise filter, job postings, SparkToro |

**Quick decision guide:**
- Have a product category? → Start with G2/Capterra reviews (yours + competitors)
- Need to know where your audience spends time? → SparkToro (reveals podcasts, YouTube, subreddits, websites, social accounts)
- Need raw language? → Reddit and YouTube comments
- Need trigger events? → LinkedIn posts, job postings, Hacker News "Ask HN" threads
- Need competitive intel? → Competitor 4-star reviews on G2; Product Hunt discussions; SparkToro competitor audience analysis

### What to Extract from Each Source

For every piece of content you find:

| Field | What to Capture |
|-------|----------------|
| Source | Platform, thread URL, date |
| Verbatim quote | Exact words — don't paraphrase |
| Context | What prompted the comment? |
| Sentiment | Positive / negative / neutral / frustrated |
| Theme tag | Pain / trigger / outcome / alternative / language |
| Customer profile signals | Role, company size, industry hints from the post |

### Research Synthesis Template

After gathering from multiple sources, synthesize into:

```
## Top Themes (ranked by frequency × intensity)

### Theme 1: [Name]
**Summary**: [1-2 sentences]
**Frequency**: Appeared in X of Y sources
**Intensity**: High / Medium / Low (based on emotional language used)
**Representative quotes**:
- "[exact quote]" — [source, date]
- "[exact quote]" — [source, date]
**Implications**: What this means for messaging / product / positioning

### Theme 2: ...
```

---

## Persona Generation

Personas should be built from research, not invented. Don't create a persona until you have at least 5-10 data points (interviews, reviews, or community posts) from a consistent segment.

### Persona Structure

```
## [Persona Name] — [Role/Title]

**Profile**
- Title range: [e.g., "Marketing Manager to VP of Marketing"]
- Company size: [e.g., "50–500 employees, Series A–C SaaS"]
- Industry: [if narrow]
- Reports to: [who]
- Team size managed: [if relevant]

**Primary Job to Be Done**
[One sentence: what outcome are they trying to achieve in their role?]

**Trigger Events**
What causes them to start looking for a solution like yours?
- [trigger 1]
- [trigger 2]

**Top Pains**
1. [Pain — in their words if possible]
2. [Pain]
3. [Pain]

**Desired Outcomes**
- [What success looks like to them]
- [How they measure it]
- [How it makes them look to their boss/team]

**Objections and Fears**
- [What makes them hesitate to buy or switch]

**Alternatives They Consider**
- [Competitor, DIY, do nothing, hire someone]

**Key Vocabulary**
Words and phrases they actually use (sourced from research):
- "[phrase]"
- "[phrase]"

**How to Reach Them**
- Channels: [where they spend time]
- Content they consume: [formats, topics]
- Influencers/communities they trust: [specific names if known]
```

### Persona Anti-Patterns

- **Don't name them cutely** ("Marketing Mary") unless your team finds it helpful — it's often a distraction
- **Don't average across segments** — a persona that represents everyone represents no one
- **Don't invent details** — if you don't have data on something, leave it blank rather than filling it in
- **Revisit quarterly** — personas decay as your market and product evolve

---

## Deliverable Formats

Depending on what the user needs, offer:

1. **Research synthesis report** — themes, quotes, patterns, and implications
2. **VOC quote bank** — organized verbatim quotes by theme, for use in copy
3. **Persona document** — 1-3 personas built from the research
4. **Jobs-to-be-done map** — functional, emotional, and social jobs by segment
5. **Competitive intelligence summary** — what customers say about competitors vs. you
6. **Research gap analysis** — what you still don't know and how to find it

Ask the user which deliverable(s) they need before generating output.

---

## Questions to Ask Before Proceeding

If context is unclear:

1. **What's the goal?** Improve messaging? Build personas? Find product gaps? Understand churn?
2. **What do you already have?** (transcripts, surveys, tickets, G2 reviews, nothing)
3. **Who is the target segment?** (all customers, a specific tier, churned users, prospects who didn't buy)
4. **What's your product?** (if not in the product marketing context file)
5. **What do you want delivered?** (synthesis report, persona, quote bank, competitive intel)

Don't ask all five at once — lead with #1 and #2, then follow up as needed.

---

## Related Skills

| When to hand off | Skill |
|-----------------|-------|
| Writing copy informed by the research | `copywriting` |
| Optimizing a page using VOC insights | `page-cro` |
| Building a competitor comparison page | `competitor-alternatives` |
| Creating a churn prevention strategy from churn research | `churn-prevention` |
| Planning paid ads informed by research | `paid-ads` |
| Writing cold email using research on pain/trigger | `cold-email` |
| Planning content based on discovered topics | `content-strategy` |

---
## SKILL: ar-project-management/senior-pm

---
name: "senior-pm"
description: Senior Project Manager for enterprise software, SaaS, and digital transformation projects. Specializes in portfolio management, quantitative risk analysis, resource optimization, stakeholder alignment, and executive reporting. Uses advanced methodologies including EMV analysis, Monte Carlo simulation, WSJF prioritization, and multi-dimensional health scoring. Use when a user needs help with project plans, project status reports, risk assessments, resource allocation, project roadmaps, milestone tracking, team capacity planning, portfolio health reviews, program management, or executive-level project reporting — especially for enterprise-scale initiatives with multiple workstreams, complex dependencies, or multi-million dollar budgets.
---

# Senior Project Management Expert

## Overview

Strategic project management for enterprise software, SaaS, and digital transformation initiatives. Provides portfolio management capabilities, quantitative analysis tools, and executive-level reporting frameworks for complex, multi-project portfolios.

### Core Expertise Areas

**Portfolio Management & Strategic Alignment**
- Multi-project portfolio optimization using advanced prioritization models (WSJF, RICE, ICE, MoSCoW)
- Strategic roadmap development aligned with business objectives and market conditions
- Resource capacity planning and allocation optimization across portfolio
- Portfolio health monitoring with multi-dimensional scoring frameworks

**Quantitative Risk Management**
- Expected Monetary Value (EMV) analysis for financial risk quantification
- Monte Carlo simulation for schedule risk modeling and confidence intervals
- Risk appetite framework implementation with enterprise-level thresholds
- Portfolio risk correlation analysis and diversification strategies

**Executive Communication & Governance**
- Board-ready executive reports with RAG status and strategic recommendations
- Stakeholder alignment through sophisticated RACI matrices and escalation paths
- Financial performance tracking with risk-adjusted ROI and NPV calculations
- Change management strategies for large-scale digital transformations

## Methodology & Frameworks

### Three-Tier Analysis Approach

**Tier 1: Portfolio Health Assessment**
Uses `project_health_dashboard.py` to provide comprehensive multi-dimensional scoring:

```bash
python3 scripts/project_health_dashboard.py assets/sample_project_data.json
```

**Health Dimensions (Weighted Scoring):**
- **Timeline Performance** (25% weight): Schedule adherence, milestone achievement, critical path analysis
- **Budget Management** (25% weight): Spend variance, forecast accuracy, cost efficiency metrics
- **Scope Delivery** (20% weight): Feature completion rates, requirement satisfaction, change control
- **Quality Metrics** (20% weight): Code coverage, defect density, technical debt, security posture
- **Risk Exposure** (10% weight): Risk score, mitigation effectiveness, exposure trends

**RAG Status Calculation:**
- 🟢 Green: Composite score >80, all dimensions >60
- 🟡 Amber: Composite score 60-80, or any dimension 40-60
- 🔴 Red: Composite score <60, or any dimension <40

**Tier 2: Risk Matrix & Mitigation Strategy**
Leverages `risk_matrix_analyzer.py` for quantitative risk assessment:

```bash
python3 scripts/risk_matrix_analyzer.py assets/sample_project_data.json
```

**Risk Quantification Process:**
1. **Probability Assessment** (1-5 scale): Historical data, expert judgment, Monte Carlo inputs
2. **Impact Analysis** (1-5 scale): Financial, schedule, quality, and strategic impact vectors
3. **Category Weighting**: Technical (1.2x), Resource (1.1x), Financial (1.4x), Schedule (1.0x)
4. **EMV Calculation**:

```python
# EMV and risk-adjusted budget calculation
def calculate_emv(risks):
    category_weights = {"Technical": 1.2, "Resource": 1.1, "Financial": 1.4, "Schedule": 1.0}
    total_emv = 0
    for risk in risks:
        score = risk["probability"] * risk["impact"] * category_weights[risk["category"]]
        emv = risk["probability"] * risk["financial_impact"]
        total_emv += emv
        risk["score"] = score
    return total_emv

def risk_adjusted_budget(base_budget, portfolio_risk_score, risk_tolerance_factor):
    risk_premium = portfolio_risk_score * risk_tolerance_factor
    return base_budget * (1 + risk_premium)
```

**Risk Response Strategies (by score threshold):**
- **Avoid** (>18): Eliminate through scope/approach changes
- **Mitigate** (12-18): Reduce probability or impact through active intervention
- **Transfer** (8-12): Insurance, contracts, partnerships
- **Accept** (<8): Monitor with contingency planning

**Tier 3: Resource Capacity Optimization**
Employs `resource_capacity_planner.py` for portfolio resource analysis:

```bash
python3 scripts/resource_capacity_planner.py assets/sample_project_data.json
```

**Capacity Analysis Framework:**
- **Utilization Optimization**: Target 70-85% for sustainable productivity
- **Skill Matching**: Algorithm-based resource allocation to maximize efficiency
- **Bottleneck Identification**: Critical path resource constraints across portfolio
- **Scenario Planning**: What-if analysis for resource reallocation strategies

### Advanced Prioritization Models

Apply each model in the specific context where it provides the most signal:

**Weighted Shortest Job First (WSJF)** — Resource-constrained agile portfolios with quantifiable cost-of-delay
```python
def wsjf(user_value, time_criticality, risk_reduction, job_size):
    return (user_value + time_criticality + risk_reduction) / job_size
```

**RICE** — Customer-facing initiatives where reach metrics are quantifiable
```python
def rice(reach, impact, confidence_pct, effort_person_months):
    return (reach * impact * (confidence_pct / 100)) / effort_person_months
```

**ICE** — Rapid prioritization during brainstorming or when analysis time is limited
```python
def ice(impact, confidence, ease):
    return (impact + confidence + ease) / 3
```

**Model Selection — Use this decision logic:**
```
if resource_constrained and agile_methodology and cost_of_delay_quantifiable:
    → WSJF
elif customer_facing and reach_metrics_available:
    → RICE
elif quick_prioritization_needed or ideation_phase:
    → ICE
elif multiple_stakeholder_groups_with_differing_priorities:
    → MoSCoW
elif complex_tradeoffs_across_incommensurable_criteria:
    → Multi-Criteria Decision Analysis (MCDA)
```

Reference: `references/portfolio-prioritization-models.md`

### Risk Management Framework

Reference: `references/risk-management-framework.md`

**Step 1: Risk Classification by Category**
- Technical: Architecture, integration, performance
- Resource: Availability, skills, retention
- Schedule: Dependencies, critical path, external factors
- Financial: Budget overruns, currency, economic factors
- Business: Market changes, competitive pressure, strategic shifts

**Step 2: Three-Point Estimation for Monte Carlo Inputs**
```python
def three_point_estimate(optimistic, most_likely, pessimistic):
    expected = (optimistic + 4 * most_likely + pessimistic) / 6
    std_dev = (pessimistic - optimistic) / 6
    return expected, std_dev
```

**Step 3: Portfolio Risk Correlation**
```python
import math

def portfolio_risk(individual_risks, correlations):
    # individual_risks: list of risk EMV values
    # correlations: list of (i, j, corr_coefficient) tuples
    sum_sq = sum(r**2 for r in individual_risks)
    sum_corr = sum(2 * c * individual_risks[i] * individual_risks[j]
                   for i, j, c in correlations)
    return math.sqrt(sum_sq + sum_corr)
```

**Risk Appetite Framework:**
- **Conservative**: Risk scores 0-8, 25-30% contingency reserves
- **Moderate**: Risk scores 8-15, 15-20% contingency reserves
- **Aggressive**: Risk scores 15+, 10-15% contingency reserves

## Assets & Templates

### Project Charter Template
Reference: `assets/project_charter_template.md`

**Comprehensive 12-section charter including:**
- Executive summary with strategic alignment
- Success criteria with KPIs and quality gates
- RACI matrix with decision authority levels
- Risk assessment with mitigation strategies
- Budget breakdown with contingency analysis
- Timeline with critical path dependencies

### Executive Report Template
Reference: `assets/executive_report_template.md`

**Board-level portfolio reporting with:**
- RAG status dashboard with trend analysis
- Financial performance vs. strategic objectives
- Risk heat map with mitigation status
- Resource utilization and capacity analysis
- Forward-looking recommendations with ROI projections

### RACI Matrix Template
Reference: `assets/raci_matrix_template.md`

**Enterprise-grade responsibility assignment featuring:**
- Detailed stakeholder roster with decision authority
- Phase-based RACI assignments (initiation through deployment)
- Escalation paths with timeline and authority levels
- Communication protocols and meeting frameworks
- Conflict resolution processes with governance integration

### Sample Portfolio Data
Reference: `assets/sample_project_data.json`

**Realistic multi-project portfolio including:**
- 4 projects across different phases and priorities
- Complete financial data (budgets, actuals, forecasts)
- Resource allocation with utilization metrics
- Risk register with probability/impact scoring
- Quality metrics and stakeholder satisfaction data
- Dependencies and milestone tracking

### Expected Output Examples
Reference: `assets/expected_output.json`

**Demonstrates script capabilities with:**
- Portfolio health scores and RAG status
- Risk matrix visualization and mitigation priorities
- Resource capacity analysis with optimization recommendations
- Integration examples showing how outputs complement each other

## Implementation Workflows

### Portfolio Health Review (Weekly)

1. **Data Collection & Validation**
   ```bash
   python3 scripts/project_health_dashboard.py current_portfolio.json
   ```
   ⚠️ If any project composite score <60 or a critical data field is missing, STOP and resolve data integrity issues before proceeding.

2. **Risk Assessment Update**
   ```bash
   python3 scripts/risk_matrix_analyzer.py current_portfolio.json
   ```
   ⚠️ If any risk score >18 (Avoid threshold), STOP and initiate escalation to project sponsor before proceeding.

3. **Capacity Analysis**
   ```bash
   python3 scripts/resource_capacity_planner.py current_portfolio.json
   ```
   ⚠️ If any team utilization >90% or <60%, flag for immediate reallocation discussion before step 4.

4. **Executive Summary Generation**
   - Synthesize outputs into executive report format
   - Highlight critical issues and recommendations
   - Prepare stakeholder communications

### Monthly Strategic Review

1. **Portfolio Prioritization Review**
   - Apply WSJF/RICE/ICE models to evaluate current priorities
   - Assess strategic alignment with business objectives
   - Identify optimization opportunities

2. **Risk Portfolio Analysis**
   - Update risk appetite and tolerance levels
   - Review portfolio risk correlation and concentration
   - Adjust risk mitigation investments

3. **Resource Optimization Planning**
   - Analyze capacity constraints across upcoming quarter
   - Plan resource reallocation and hiring strategies
   - Identify skill gaps and training needs

4. **Stakeholder Alignment Session**
   - Present portfolio health and strategic recommendations
   - Gather feedback on prioritization and resource allocation
   - Align on upcoming quarter priorities and investments

### Quarterly Portfolio Optimization

1. **Strategic Alignment Assessment**
   - Evaluate portfolio contribution to business objectives
   - Assess market and competitive position changes
   - Update strategic priorities and success criteria

2. **Financial Performance Review**
   - Analyze risk-adjusted ROI across portfolio
   - Review budget performance and forecast accuracy
   - Optimize investment allocation for maximum value

3. **Capability Gap Analysis**
   - Identify emerging technology and skill requirements
   - Plan capability building investments
   - Assess make vs. buy vs. partner decisions

4. **Portfolio Rebalancing**
   - Apply three horizons model for innovation balance
   - Optimize risk-return profile using efficient frontier
   - Plan new initiatives and sunset decisions

## Integration Strategies

### Atlassian Integration
- **Jira**: Portfolio dashboards, cross-project metrics, risk tracking
- **Confluence**: Strategic documentation, executive reports, knowledge management
- Use MCP integrations to automate data collection and report generation

### Financial Systems Integration
- **Budget Tracking**: Real-time spend data for variance analysis
- **Resource Costing**: Hourly rates and utilization for capacity planning
- **ROI Measurement**: Value realization tracking against projections

### Stakeholder Management
- **Executive Dashboards**: Real-time portfolio health visualization
- **Team Scorecards**: Individual project performance metrics
- **Risk Registers**: Collaborative risk management with automated escalation

## Handoff Protocols

### TO Scrum Master
**Context Transfer:**
- Strategic priorities and success criteria
- Resource allocation and team composition
- Risk factors requiring sprint-level attention
- Quality standards and acceptance criteria

**Ongoing Collaboration:**
- Weekly velocity and health metrics review
- Sprint retrospective insights for portfolio learning
- Impediment escalation and resolution support
- Team capacity and utilization feedback

### TO Product Owner
**Strategic Context:**
- Market prioritization and competitive analysis
- User value frameworks and measurement criteria
- Feature prioritization aligned with portfolio objectives
- Resource and timeline constraints

**Decision Support:**
- ROI analysis for feature investments
- Risk assessment for product decisions
- Market intelligence and customer feedback integration
- Strategic roadmap alignment and dependencies

### FROM Executive Team
**Strategic Direction:**
- Business objective updates and priority changes
- Budget allocation and resource approval decisions
- Risk appetite and tolerance level adjustments
- Market strategy and competitive response decisions

**Performance Expectations:**
- Portfolio health and value delivery targets
- Timeline and milestone commitment expectations
- Quality standards and compliance requirements
- Stakeholder satisfaction and communication standards

## Success Metrics & KPIs

Reference: `references/portfolio-kpis.md` for full definitions and measurement guidance.

### Portfolio Performance
- On-time Delivery Rate: >80% within 10% of planned timeline
- Budget Variance: <5% average across portfolio
- Quality Score: >85 composite rating
- Risk Mitigation Coverage: >90% risks with active plans
- Resource Utilization: 75-85% average

### Strategic Value
- ROI Achievement: >90% projects meeting projections within 12 months
- Strategic Alignment: >95% investment aligned with business priorities
- Innovation Balance: 70% operational / 20% growth / 10% transformational
- Stakeholder Satisfaction: >8.5/10 executive average
- Time-to-Value: <6 months average post-completion

### Risk Management
- Risk Exposure: Maintain within approved appetite ranges
- Resolution Time: <30 days (medium), <7 days (high)
- Mitigation Cost Efficiency: <20% of total portfolio risk EMV
- Risk Prediction Accuracy: >70% probability assessment accuracy

## Continuous Improvement Framework

### Portfolio Learning Integration
- Capture lessons learned from completed projects
- Update risk probability assessments based on historical data
- Refine estimation accuracy through retrospective analysis
- Share best practices across project teams

### Methodology Evolution
- Regular review of prioritization model effectiveness
- Update risk frameworks based on industry best practices
- Integrate new tools and technologies for analysis efficiency
- Benchmark against industry portfolio performance standards

### Stakeholder Feedback Integration
- Quarterly stakeholder satisfaction surveys
- Executive interview feedback on decision support quality
- Team feedback on process efficiency and effectiveness
- Customer impact assessment of portfolio decisions

## Related Skills

- **Product Strategist** (`product-team/product-strategist/`) — Product OKRs align with portfolio objectives
- **Scrum Master** (`project-management/scrum-master/`) — Sprint velocity data feeds project health dashboards

---
## SKILL: ar-c-level-advisor/ceo-advisor

---
name: "ceo-advisor"
description: "Executive leadership guidance for strategic decision-making, organizational development, and stakeholder management. Use when planning strategy, preparing board presentations, managing investors, developing organizational culture, making executive decisions, fundraising, or when user mentions CEO, strategic planning, board meetings, investor updates, organizational leadership, or executive strategy."
license: MIT
metadata:
  version: 2.0.0
  author: Alireza Rezvani
  category: c-level
  domain: ceo-leadership
  updated: 2026-03-05
  python-tools: strategy_analyzer.py, financial_scenario_analyzer.py
  frameworks: executive-decisions, board-governance, leadership-culture
---

# CEO Advisor

Strategic leadership frameworks for vision, fundraising, board management, culture, and stakeholder alignment.

## Keywords
CEO, chief executive officer, strategy, strategic planning, fundraising, board management, investor relations, culture, organizational leadership, vision, mission, stakeholder management, capital allocation, crisis management, succession planning

## Quick Start

```bash
python scripts/strategy_analyzer.py          # Analyze strategic options with weighted scoring
python scripts/financial_scenario_analyzer.py # Model financial scenarios (base/bull/bear)
```

## Core Responsibilities

### 1. Vision & Strategy
Set the direction. Not a 50-page document — a clear, compelling answer to "Where are we going and why?"

**Strategic planning cycle:**
- Annual: 3-year vision refresh + 1-year strategic plan
- Quarterly: OKR setting with C-suite (COO drives execution)
- Monthly: strategy health check — are we still on track?

**Stage-adaptive time horizons:**
- Seed/Pre-PMF: 3-month / 6-month / 12-month
- Series A: 6-month / 1-year / 2-year
- Series B+: 1-year / 3-year / 5-year

See `references/executive_decision_framework.md` for the full Go/No-Go framework, crisis playbook, and capital allocation model.

### 2. Capital & Resource Management
You're the chief allocator. Every dollar, every person, every hour of engineering time is a bet.

**Capital allocation priorities:**
1. Keep the lights on (operations, must-haves)
2. Protect the core (retention, quality, security)
3. Grow the core (expansion of what works)
4. Fund new bets (innovation, new products/markets)

**Fundraising:** Know your numbers cold. Timing matters more than valuation. See `references/board_governance_investor_relations.md`.

### 3. Stakeholder Leadership
You serve multiple masters. Priority order:
1. Customers (they pay the bills)
2. Team (they build the product)
3. Board/Investors (they fund the mission)
4. Partners (they extend your reach)

### 4. Organizational Culture
Culture is what people do when you're not in the room. It's your job to define it, model it, and enforce it.

See `references/leadership_organizational_culture.md` for culture development frameworks and the CEO learning agenda. Also see `culture-architect/` for the operational culture toolkit.

### 5. Board & Investor Management
Your board can be your greatest asset or your biggest liability. The difference is how you manage them.

See `references/board_governance_investor_relations.md` for board meeting prep, investor communication cadence, and managing difficult directors. Also see `board-deck-builder/` for assembling the actual board deck.

## Key Questions a CEO Asks

- "Can every person in this company explain our strategy in one sentence?"
- "What's the one thing that, if it goes wrong, kills us?"
- "Am I spending my time on the highest-leverage activity right now?"
- "What decision am I avoiding? Why?"
- "If we could only do one thing this quarter, what would it be?"
- "Do our investors and our team hear the same story from me?"
- "Who would replace me if I got hit by a bus tomorrow?"

## CEO Metrics Dashboard

| Category | Metric | Target | Frequency |
|----------|--------|--------|-----------|
| **Strategy** | Annual goals hit rate | > 70% | Quarterly |
| **Revenue** | ARR growth rate | Stage-dependent | Monthly |
| **Capital** | Months of runway | > 12 months | Monthly |
| **Capital** | Burn multiple | < 2x | Monthly |
| **Product** | NPS / PMF score | > 40 NPS | Quarterly |
| **People** | Regrettable attrition | < 10% | Monthly |
| **People** | Employee engagement | > 7/10 | Quarterly |
| **Board** | Board NPS (your relationship) | Positive trend | Quarterly |
| **Personal** | % time on strategic work | > 40% | Weekly |

## Red Flags

- You're the bottleneck for more than 3 decisions per week
- The board surprises you with questions you can't answer
- Your calendar is 80%+ meetings with no strategic blocks
- Key people are leaving and you didn't see it coming
- You're fundraising reactively (runway < 6 months, no plan)
- Your team can't articulate the strategy without you in the room
- You're avoiding a hard conversation (co-founder, investor, underperformer)

## Integration with C-Suite Roles

| When... | CEO works with... | To... |
|---------|-------------------|-------|
| Setting direction | COO | Translate vision into OKRs and execution plan |
| Fundraising | CFO | Model scenarios, prep financials, negotiate terms |
| Board meetings | All C-suite | Each role contributes their section |
| Culture issues | CHRO | Diagnose and address people/culture problems |
| Product vision | CPO | Align product strategy with company direction |
| Market positioning | CMO | Ensure brand and messaging reflect strategy |
| Revenue targets | CRO | Set realistic targets backed by pipeline data |
| Security/compliance | CISO | Understand risk posture for board reporting |
| Technical strategy | CTO | Align tech investments with business priorities |
| Hard decisions | Executive Mentor | Stress-test before committing |

## Proactive Triggers

Surface these without being asked when you detect them in company context:
- Runway < 12 months with no fundraising plan → flag immediately
- Strategy hasn't been reviewed in 2+ quarters → prompt refresh
- Board meeting approaching with no prep → initiate board-prep flow
- Founder spending < 20% time on strategic work → raise it
- Key exec departure risk visible → escalate to CHRO

## Output Artifacts

| Request | You Produce |
|---------|-------------|
| "Help me think about strategy" | Strategic options matrix with risk-adjusted scoring |
| "Prep me for the board" | Board narrative + anticipated questions + data gaps |
| "Should we raise?" | Fundraising readiness assessment with timeline |
| "We need to decide on X" | Decision framework with options, trade-offs, recommendation |
| "How are we doing?" | CEO scorecard with traffic-light metrics |

## Reasoning Technique: Tree of Thought

Explore multiple futures. For every strategic decision, generate at least 3 paths. Evaluate each path for upside, downside, reversibility, and second-order effects. Pick the path with the best risk-adjusted outcome.

**Stage-adaptive horizons:**
- Seed: project 3m/6m/12m
- Series A: project 6m/1y/2y
- Series B+: project 1y/3y/5y

## Communication

All output passes the Internal Quality Loop before reaching the founder (see `agent-protocol/SKILL.md`).
- Self-verify: source attribution, assumption audit, confidence scoring
- Peer-verify: cross-functional claims validated by the owning role
- Critic pre-screen: high-stakes decisions reviewed by Executive Mentor
- Output format: Bottom Line → What (with confidence) → Why → How to Act → Your Decision
- Results only. Every finding tagged: 🟢 verified, 🟡 medium, 🔴 assumed.

## Context Integration

- **Always** read `company-context.md` before responding (if it exists)
- **During board meetings:** Use only your own analysis in Phase 2 (no cross-pollination)
- **Invocation:** You can request input from other roles: `[INVOKE:role|question]`

## Resources
- `references/executive_decision_framework.md` — Go/No-Go framework, crisis playbook, capital allocation
- `references/board_governance_investor_relations.md` — Board management, investor communication, fundraising
- `references/leadership_organizational_culture.md` — Culture development, CEO routines, succession planning

---
## SKILL: meeting-insights-analyzer

---
name: meeting-insights-analyzer
description: Analyzes meeting transcripts and recordings to uncover behavioral patterns, communication insights, and actionable feedback. Identifies when you avoid conflict, use filler words, dominate conversations, or miss opportunities to listen. Perfect for professionals seeking to improve their communication and leadership skills.
---

# Meeting Insights Analyzer

This skill transforms your meeting transcripts into actionable insights about your communication patterns, helping you become a more effective communicator and leader.

## When to Use This Skill

- Analyzing your communication patterns across multiple meetings
- Getting feedback on your leadership and facilitation style
- Identifying when you avoid difficult conversations
- Understanding your speaking habits and filler words
- Tracking improvement in communication skills over time
- Preparing for performance reviews with concrete examples
- Coaching team members on their communication style

## What This Skill Does

1. **Pattern Recognition**: Identifies recurring behaviors across meetings like:
   - Conflict avoidance or indirect communication
   - Speaking ratios and turn-taking
   - Question-asking vs. statement-making patterns
   - Active listening indicators
   - Decision-making approaches

2. **Communication Analysis**: Evaluates communication effectiveness:
   - Clarity and directness
   - Use of filler words and hedging language
   - Tone and sentiment patterns
   - Meeting control and facilitation

3. **Actionable Feedback**: Provides specific, timestamped examples with:
   - What happened
   - Why it matters
   - How to improve

4. **Trend Tracking**: Compares patterns over time when analyzing multiple meetings

## How to Use

### Basic Setup

1. Download your meeting transcripts to a folder (e.g., `~/meetings/`)
2. Navigate to that folder in Claude Code
3. Ask for the analysis you want

### Quick Start Examples

```
Analyze all meetings in this folder and tell me when I avoided conflict.
```

```
Look at my meetings from the past month and identify my communication patterns.
```

```
Compare my facilitation style between these two meeting folders.
```

### Advanced Analysis

```
Analyze all transcripts in this folder and:
1. Identify when I interrupted others
2. Calculate my speaking ratio
3. Find moments I avoided giving direct feedback
4. Track my use of filler words
5. Show examples of good active listening
```

## Instructions

When a user requests meeting analysis:

1. **Discover Available Data**
   - Scan the folder for transcript files (.txt, .md, .vtt, .srt, .docx)
   - Check if files contain speaker labels and timestamps
   - Confirm the date range of meetings
   - Identify the user's name/identifier in transcripts

2. **Clarify Analysis Goals**
   
   If not specified, ask what they want to learn:
   - Specific behaviors (conflict avoidance, interruptions, filler words)
   - Communication effectiveness (clarity, directness, listening)
   - Meeting facilitation skills
   - Speaking patterns and ratios
   - Growth areas for improvement
   
3. **Analyze Patterns**

   For each requested insight:
   
   **Conflict Avoidance**:
   - Look for hedging language ("maybe", "kind of", "I think")
   - Indirect phrasing instead of direct requests
   - Changing subject when tension arises
   - Agreeing without commitment ("yeah, but...")
   - Not addressing obvious problems
   
   **Speaking Ratios**:
   - Calculate percentage of meeting spent speaking
   - Count interruptions (by and of the user)
   - Measure average speaking turn length
   - Track question vs. statement ratios
   
   **Filler Words**:
   - Count "um", "uh", "like", "you know", "actually", etc.
   - Note frequency per minute or per speaking turn
   - Identify situations where they increase (nervous, uncertain)
   
   **Active Listening**:
   - Questions that reference others' previous points
   - Paraphrasing or summarizing others' ideas
   - Building on others' contributions
   - Asking clarifying questions
   
   **Leadership & Facilitation**:
   - Decision-making approach (directive vs. collaborative)
   - How disagreements are handled
   - Inclusion of quieter participants
   - Time management and agenda control
   - Follow-up and action item clarity

4. **Provide Specific Examples**

   For each pattern found, include:
   
   ```markdown
   ### [Pattern Name]
   
   **Finding**: [One-sentence summary of the pattern]
   
   **Frequency**: [X times across Y meetings]
   
   **Examples**:
   
   1. **[Meeting Name/Date]** - [Timestamp]
      
      **What Happened**:
      > [Actual quote from transcript]
      
      **Why This Matters**:
      [Explanation of the impact or missed opportunity]
      
      **Better Approach**:
      [Specific alternative phrasing or behavior]
   
   [Repeat for 2-3 strongest examples]
   ```

5. **Synthesize Insights**

   After analyzing all patterns, provide:
   
   ```markdown
   # Meeting Insights Summary
   
   **Analysis Period**: [Date range]
   **Meetings Analyzed**: [X meetings]
   **Total Duration**: [X hours]
   
   ## Key Patterns Identified
   
   ### 1. [Primary Pattern]
   - **Observed**: [What you saw]
   - **Impact**: [Why it matters]
   - **Recommendation**: [How to improve]
   
   ### 2. [Second Pattern]
   [Same structure]
   
   ## Communication Strengths
   
   1. [Strength 1 with example]
   2. [Strength 2 with example]
   3. [Strength 3 with example]
   
   ## Growth Opportunities
   
   1. **[Area 1]**: [Specific, actionable advice]
   2. **[Area 2]**: [Specific, actionable advice]
   3. **[Area 3]**: [Specific, actionable advice]
   
   ## Speaking Statistics
   
   - Average speaking time: [X% of meeting]
   - Questions asked: [X per meeting average]
   - Filler words: [X per minute]
   - Interruptions: [X given / Y received per meeting]
   
   ## Next Steps
   
   [3-5 concrete actions to improve communication]
   ```

6. **Offer Follow-Up Options**
   - Track these same metrics in future meetings
   - Deep dive into specific meetings or patterns
   - Compare to industry benchmarks
   - Create a personal communication development plan
   - Generate a summary for performance reviews

## Examples

### Example 1: Conflict Avoidance Analysis (Inspired by Dan Shipper)

**User**: "I download all of my meeting recordings and put them in a folder. Tell me all the times I've subtly avoided conflict."

**Output**: 
```markdown
# Conflict Avoidance Patterns

Found 23 instances across 15 meetings where you used indirect 
communication or avoided addressing tensions directly.

## Pattern: Hedging on Critical Feedback

**Frequency**: 8 times across 7 meetings

**Example 1: 1:1 with Sarah** - 00:14:32

**What Happened**:
> "So, I was thinking... maybe we could, like, potentially 
> consider looking at the timeline again? I mean, if you 
> think that makes sense. But whatever you think is best!"

**Why This Matters**:
You needed to address that Sarah's project was behind schedule, 
but the hedging language ("maybe", "potentially", "if you think") 
and the deflection at the end ("whatever you think") made it easy 
for her to miss the urgency.

**Better Approach**:
"Sarah, the project is two weeks behind schedule. We need to 
discuss what's blocking progress and create a new timeline 
today."

[Additional examples...]

## Recommendations

1. **Name the issue directly** in the first sentence
2. **Remove hedging words** like "maybe," "kind of," "sort of"
3. **Ask specific questions** instead of hinting
4. **Schedule difficult conversations** instead of raising them casually
```

### Example 2: Leadership Facilitation

**User**: "Analyze my team meetings and tell me about my facilitation style."

**Output**: Provides insights on:
- How much you speak vs. team members (60% vs. 40%)
- Whether you ask questions or make statements (3:1 ratio)
- How you handle disagreements (tendency to resolve too quickly)
- Who speaks least and whether you draw them in
- Examples of good and missed facilitation moments

### Example 3: Personal Development Tracking

**User**: "Compare my meetings from Q1 vs. Q2 to see if I've improved my listening skills."

**Output**: Creates a comparative analysis showing:
- Decrease in interruptions (8 per meeting → 3 per meeting)
- Increase in clarifying questions (2 → 7 per meeting)
- Improvement in building on others' ideas
- Specific examples showing the difference
- Remaining areas for growth

## Setup Tips

### Getting Meeting Transcripts

**From Granola** (free with Lenny's newsletter subscription):
- Granola auto-transcribes your meetings
- Export transcripts to a folder: [Instructions on how]
- Point Claude Code to that folder

**From Zoom**:
- Enable cloud recording with transcription
- Download VTT or SRT files after meetings
- Store in a dedicated folder

**From Google Meet**:
- Use Google Docs auto-transcription
- Save transcript docs to a folder
- Download as .txt files or give Claude Code access

**From Fireflies.ai, Otter.ai, etc.**:
- Export transcripts in bulk
- Store in a local folder
- Run analysis on the folder

### Best Practices

1. **Consistent naming**: Use `YYYY-MM-DD - Meeting Name.txt` format
2. **Regular analysis**: Review monthly or quarterly for trends
3. **Specific queries**: Ask about one behavior at a time for depth
4. **Privacy**: Keep sensitive meeting data local
5. **Action-oriented**: Focus on one improvement area at a time

## Common Analysis Requests

- "When do I avoid difficult conversations?"
- "How often do I interrupt others?"
- "What's my speaking vs. listening ratio?"
- "Do I ask good questions?"
- "How do I handle disagreement?"
- "Am I inclusive of all voices?"
- "Do I use too many filler words?"
- "How clear are my action items?"
- "Do I stay on agenda or get sidetracked?"
- "How has my communication changed over time?"

## Related Use Cases

- Creating a personal development plan from insights
- Preparing performance review materials with examples
- Coaching direct reports on their communication
- Analyzing customer calls for sales or support patterns
- Studying negotiation tactics and outcomes


