# SKILLS: Финансы, аналитика, KPI
# Содержит: ar-finance, ar-finance/financial-analyst, ar-finance/saas-metrics-coach, ar-c-level-advisor/cfo-advisor, gb-tufte-report

---
## SKILL: ar-finance

---
name: "finance-skills"
description: "Financial analyst agent skill and plugin for Claude Code, Codex, Gemini CLI, Cursor, OpenClaw. Ratio analysis, DCF valuation, budget variance, rolling forecasts. 4 Python tools (stdlib-only)."
version: 1.0.0
author: Alireza Rezvani
license: MIT
tags:
  - finance
  - financial-analysis
  - dcf
  - valuation
  - budgeting
agents:
  - claude-code
  - codex-cli
  - openclaw
---

# Finance Skills

Production-ready financial analysis skill for strategic decision-making.

## Quick Start

### Claude Code
```
/read finance/financial-analyst/SKILL.md
```

### Codex CLI
```bash
npx agent-skills-cli add alirezarezvani/claude-skills/finance
```

## Skills Overview

| Skill | Folder | Focus |
|-------|--------|-------|
| Financial Analyst | `financial-analyst/` | Ratio analysis, DCF, budget variance, forecasting |

## Python Tools

4 scripts, all stdlib-only:

```bash
python3 financial-analyst/scripts/ratio_calculator.py --help
python3 financial-analyst/scripts/dcf_valuation.py --help
python3 financial-analyst/scripts/budget_variance_analyzer.py --help
python3 financial-analyst/scripts/forecast_builder.py --help
```

## Rules

- Load only the specific skill SKILL.md you need
- Always validate financial outputs against source data

---
## SKILL: ar-finance/financial-analyst

---
name: "financial-analyst"
description: Performs financial ratio analysis, DCF valuation, budget variance analysis, and rolling forecast construction for strategic decision-making. Use when analyzing financial statements, building valuation models, assessing budget variances, or constructing financial projections and forecasts. Also applicable when users mention financial modeling, cash flow analysis, company valuation, financial projections, or spreadsheet analysis.
---

# Financial Analyst Skill

## Overview

Production-ready financial analysis toolkit providing ratio analysis, DCF valuation, budget variance analysis, and rolling forecast construction. Designed for financial modeling, forecasting & budgeting, management reporting, business performance analysis, and investment analysis.

## 5-Phase Workflow

### Phase 1: Scoping
- Define analysis objectives and stakeholder requirements
- Identify data sources and time periods
- Establish materiality thresholds and accuracy targets
- Select appropriate analytical frameworks

### Phase 2: Data Analysis & Modeling
- Collect and validate financial data (income statement, balance sheet, cash flow)
- **Validate input data completeness** before running ratio calculations (check for missing fields, nulls, or implausible values)
- Calculate financial ratios across 5 categories (profitability, liquidity, leverage, efficiency, valuation)
- Build DCF models with WACC and terminal value calculations; **cross-check DCF outputs against sanity bounds** (e.g., implied multiples vs. comparables)
- Construct budget variance analyses with favorable/unfavorable classification
- Develop driver-based forecasts with scenario modeling

### Phase 3: Insight Generation
- Interpret ratio trends and benchmark against industry standards
- Identify material variances and root causes
- Assess valuation ranges through sensitivity analysis
- Evaluate forecast scenarios (base/bull/bear) for decision support

### Phase 4: Reporting
- Generate executive summaries with key findings
- Produce detailed variance reports by department and category
- Deliver DCF valuation reports with sensitivity tables
- Present rolling forecasts with trend analysis

### Phase 5: Follow-up
- Track forecast accuracy (target: +/-5% revenue, +/-3% expenses)
- Monitor report delivery timeliness (target: 100% on time)
- Update models with actuals as they become available
- Refine assumptions based on variance analysis

## Tools

### 1. Ratio Calculator (`scripts/ratio_calculator.py`)

Calculate and interpret financial ratios from financial statement data.

**Ratio Categories:**
- **Profitability:** ROE, ROA, Gross Margin, Operating Margin, Net Margin
- **Liquidity:** Current Ratio, Quick Ratio, Cash Ratio
- **Leverage:** Debt-to-Equity, Interest Coverage, DSCR
- **Efficiency:** Asset Turnover, Inventory Turnover, Receivables Turnover, DSO
- **Valuation:** P/E, P/B, P/S, EV/EBITDA, PEG Ratio

```bash
python scripts/ratio_calculator.py sample_financial_data.json
python scripts/ratio_calculator.py sample_financial_data.json --format json
python scripts/ratio_calculator.py sample_financial_data.json --category profitability
```

### 2. DCF Valuation (`scripts/dcf_valuation.py`)

Discounted Cash Flow enterprise and equity valuation with sensitivity analysis.

**Features:**
- WACC calculation via CAPM
- Revenue and free cash flow projections (5-year default)
- Terminal value via perpetuity growth and exit multiple methods
- Enterprise value and equity value derivation
- Two-way sensitivity analysis (discount rate vs growth rate)

```bash
python scripts/dcf_valuation.py valuation_data.json
python scripts/dcf_valuation.py valuation_data.json --format json
python scripts/dcf_valuation.py valuation_data.json --projection-years 7
```

### 3. Budget Variance Analyzer (`scripts/budget_variance_analyzer.py`)

Analyze actual vs budget vs prior year performance with materiality filtering.

**Features:**
- Dollar and percentage variance calculation
- Materiality threshold filtering (default: 10% or $50K)
- Favorable/unfavorable classification with revenue/expense logic
- Department and category breakdown
- Executive summary generation

```bash
python scripts/budget_variance_analyzer.py budget_data.json
python scripts/budget_variance_analyzer.py budget_data.json --format json
python scripts/budget_variance_analyzer.py budget_data.json --threshold-pct 5 --threshold-amt 25000
```

### 4. Forecast Builder (`scripts/forecast_builder.py`)

Driver-based revenue forecasting with rolling cash flow projection and scenario modeling.

**Features:**
- Driver-based revenue forecast model
- 13-week rolling cash flow projection
- Scenario modeling (base/bull/bear cases)
- Trend analysis using simple linear regression (standard library)

```bash
python scripts/forecast_builder.py forecast_data.json
python scripts/forecast_builder.py forecast_data.json --format json
python scripts/forecast_builder.py forecast_data.json --scenarios base,bull,bear
```

## Knowledge Bases

| Reference | Purpose |
|-----------|---------|
| `references/financial-ratios-guide.md` | Ratio formulas, interpretation, industry benchmarks |
| `references/valuation-methodology.md` | DCF methodology, WACC, terminal value, comps |
| `references/forecasting-best-practices.md` | Driver-based forecasting, rolling forecasts, accuracy |
| `references/industry-adaptations.md` | Sector-specific metrics and considerations (SaaS, Retail, Manufacturing, Financial Services, Healthcare) |

## Templates

| Template | Purpose |
|----------|---------|
| `assets/variance_report_template.md` | Budget variance report template |
| `assets/dcf_analysis_template.md` | DCF valuation analysis template |
| `assets/forecast_report_template.md` | Revenue forecast report template |

## Key Metrics & Targets

| Metric | Target |
|--------|--------|
| Forecast accuracy (revenue) | +/-5% |
| Forecast accuracy (expenses) | +/-3% |
| Report delivery | 100% on time |
| Model documentation | Complete for all assumptions |
| Variance explanation | 100% of material variances |

## Input Data Format

All scripts accept JSON input files. See `assets/sample_financial_data.json` for the complete input schema covering all four tools.

## Dependencies

**None** - All scripts use Python standard library only (`math`, `statistics`, `json`, `argparse`, `datetime`). No numpy, pandas, or scipy required.

---
## SKILL: ar-finance/saas-metrics-coach

---
name: saas-metrics-coach
description: SaaS financial health advisor. Use when a user shares revenue or customer numbers, or mentions ARR, MRR, churn, LTV, CAC, NRR, or asks how their SaaS business is doing.
license: MIT
metadata:
  version: 1.0.0
  author: Abbas Mir
  category: finance
  updated: 2026-03-08
---

# SaaS Metrics Coach

Act as a senior SaaS CFO advisor. Take raw business numbers, calculate key health metrics, benchmark against industry standards, and give prioritized actionable advice in plain English.

## Step 1 — Collect Inputs

If not already provided, ask for these in a single grouped request:

- Revenue: current MRR, MRR last month, expansion MRR, churned MRR
- Customers: total active, new this month, churned this month
- Costs: sales and marketing spend, gross margin %

Work with partial data. Be explicit about what is missing and what assumptions are being made.

## Step 2 — Calculate Metrics

Run `scripts/metrics_calculator.py` with the user's inputs. If the script is unavailable, use the formulas in `references/formulas.md`.

Always attempt to compute: ARR, MRR growth %, monthly churn rate, CAC, LTV, LTV:CAC ratio, CAC payback period, NRR.

**Additional Analysis Tools:**
- Use `scripts/quick_ratio_calculator.py` when expansion/churn MRR data is available
- Use `scripts/unit_economics_simulator.py` for forward-looking projections

## Step 3 — Benchmark Each Metric

Load `references/benchmarks.md`. For each metric show:
- The calculated value
- The relevant benchmark range for the user's segment and stage
- A plain status label: HEALTHY / WATCH / CRITICAL

Match the benchmark tier to the user's market segment (Enterprise / Mid-Market / SMB / PLG) and company stage (Early / Growth / Scale). Ask if unclear.

## Step 4 — Prioritize and Recommend

Identify the top 2-3 metrics at WATCH or CRITICAL status. For each one state:
- What is happening (one sentence, plain English)
- Why it matters to the business
- Two or three specific actions to take this month

Order by impact — address the most damaging problem first.

## Step 5 — Output Format

Always use this exact structure:

```
# SaaS Health Report — [Month Year]

## Metrics at a Glance
| Metric | Your Value | Benchmark | Status |
|--------|------------|-----------|--------|

## Overall Picture
[2-3 sentences, plain English summary]

## Priority Issues

### 1. [Metric Name]
What is happening: ...
Why it matters: ...
Fix it this month: ...

### 2. [Metric Name]
...

## What is Working
[1-2 genuine strengths, no padding]

## 90-Day Focus
[Single metric to move + specific numeric target]
```

## Examples

**Example 1 — Partial data**

Input: "MRR is $80k, we have 200 customers, about 3 cancel each month."

Expected output: Calculates ARPA ($400), monthly churn (1.5%), ARR ($960k), LTV estimate. Flags CAC and growth rate as missing. Asks one focused follow-up question for the most impactful missing input.

**Example 2 — Critical scenario**

Input: "MRR $22k (was $23.5k), 80 customers, lost 9, gained 6, spent $15k on ads, 65% gross margin."

Expected output: Flags negative MoM growth (-6.4%), critical churn (11.25%), and LTV:CAC of 0.64:1 as CRITICAL. Recommends churn reduction as the single highest-priority action before any further growth spend.

## Key Principles

- Be direct. If a metric is bad, say it is bad.
- Explain every metric in one sentence before showing the number.
- Cap priority issues at three. More than three paralyzes action.
- Context changes benchmarks. Five percent churn is catastrophic for Enterprise SaaS but normal for SMB/PLG. Always confirm the user's target market before scoring.

## Reference Files

- `references/formulas.md` — All metric formulas with worked examples
- `references/benchmarks.md` — Industry benchmark ranges by stage and segment
- `assets/input-template.md` — Blank input form to share with users
- `scripts/metrics_calculator.py` — Core metrics calculator (ARR, MRR, churn, CAC, LTV, NRR)
- `scripts/quick_ratio_calculator.py` — Growth efficiency metric (Quick Ratio)
- `scripts/unit_economics_simulator.py` — 12-month forward projection

## Tools

### 1. Metrics Calculator (`scripts/metrics_calculator.py`)
Core SaaS metrics from raw business numbers.

```bash
# Interactive mode
python scripts/metrics_calculator.py

# CLI mode
python scripts/metrics_calculator.py --mrr 50000 --customers 100 --churned 5 --json
```

### 2. Quick Ratio Calculator (`scripts/quick_ratio_calculator.py`)
Growth efficiency metric: (New MRR + Expansion) / (Churned + Contraction)

```bash
python scripts/quick_ratio_calculator.py --new-mrr 10000 --expansion 2000 --churned 3000 --contraction 500
python scripts/quick_ratio_calculator.py --new-mrr 10000 --expansion 2000 --churned 3000 --json
```

**Benchmarks:**
- < 1.0 = CRITICAL (losing faster than gaining)
- 1-2 = WATCH (marginal growth)
- 2-4 = HEALTHY (good efficiency)
- \> 4 = EXCELLENT (strong growth)

### 3. Unit Economics Simulator (`scripts/unit_economics_simulator.py`)
Project metrics forward 12 months based on growth/churn assumptions.

```bash
python scripts/unit_economics_simulator.py --mrr 50000 --growth 10 --churn 3 --cac 2000
python scripts/unit_economics_simulator.py --mrr 50000 --growth 10 --churn 3 --cac 2000 --json
```

**Use for:**
- "What if we grow at X% per month?"
- Runway projections
- Scenario planning (best/base/worst case)

## Related Skills

- **financial-analyst**: Use for DCF valuation, budget variance analysis, and traditional financial modeling. NOT for SaaS-specific metrics like CAC, LTV, or churn.
- **business-growth/customer-success**: Use for retention strategies and customer health scoring. Complements this skill when churn is flagged as CRITICAL.

---
## SKILL: ar-c-level-advisor/cfo-advisor

---
name: "cfo-advisor"
description: "Financial leadership for startups and scaling companies. Financial modeling, unit economics, fundraising strategy, cash management, and board financial packages. Use when building financial models, analyzing unit economics, planning fundraising, managing cash runway, preparing board materials, or when user mentions CFO, burn rate, runway, fundraising, unit economics, LTV, CAC, term sheets, or financial strategy."
license: MIT
metadata:
  version: 1.0.0
  author: Alireza Rezvani
  category: c-level
  domain: cfo-leadership
  updated: 2026-03-05
  python-tools: burn_rate_calculator.py, unit_economics_analyzer.py, fundraising_model.py
  frameworks: financial-planning, fundraising-playbook, cash-management
---

# CFO Advisor

Strategic financial frameworks for startup CFOs and finance leaders. Numbers-driven, decisions-focused.

This is **not** a financial analyst skill. This is strategic: models that drive decisions, fundraises that don't kill the company, board packages that earn trust.

## Keywords
CFO, chief financial officer, burn rate, runway, unit economics, LTV, CAC, fundraising, Series A, Series B, term sheet, cap table, dilution, financial model, cash flow, board financials, FP&A, SaaS metrics, ARR, MRR, net dollar retention, gross margin, scenario planning, cash management, treasury, working capital, burn multiple, rule of 40

## Quick Start

```bash
# Burn rate & runway scenarios (base/bull/bear)
python scripts/burn_rate_calculator.py

# Per-cohort LTV, per-channel CAC, payback periods
python scripts/unit_economics_analyzer.py

# Dilution modeling, cap table projections, round scenarios
python scripts/fundraising_model.py
```

## Key Questions (ask these first)

- **What's your burn multiple?** (Net burn ÷ Net new ARR. > 2x is a problem.)
- **If fundraising takes 6 months instead of 3, do you survive?** (If not, you're already behind.)
- **Show me unit economics per cohort, not blended.** (Blended hides deterioration.)
- **What's your NDR?** (> 100% means you grow without signing a single new customer.)
- **What are your decision triggers?** (At what runway do you start cutting? Define now, not in a crisis.)

## Core Responsibilities

| Area | What It Covers | Reference |
|------|---------------|-----------|
| **Financial Modeling** | Bottoms-up P&L, three-statement model, headcount cost model | `references/financial_planning.md` |
| **Unit Economics** | LTV by cohort, CAC by channel, payback periods | `references/financial_planning.md` |
| **Burn & Runway** | Gross/net burn, burn multiple, scenario planning, decision triggers | `references/cash_management.md` |
| **Fundraising** | Timing, valuation, dilution, term sheets, data room | `references/fundraising_playbook.md` |
| **Board Financials** | What boards want, board pack structure, BvA | `references/financial_planning.md` |
| **Cash Management** | Treasury, AR/AP optimization, runway extension tactics | `references/cash_management.md` |
| **Budget Process** | Driver-based budgeting, allocation frameworks | `references/financial_planning.md` |

## CFO Metrics Dashboard

| Category | Metric | Target | Frequency |
|----------|--------|--------|-----------|
| **Efficiency** | Burn Multiple | < 1.5x | Monthly |
| **Efficiency** | Rule of 40 | > 40 | Quarterly |
| **Efficiency** | Revenue per FTE | Track trend | Quarterly |
| **Revenue** | ARR growth (YoY) | > 2x at Series A/B | Monthly |
| **Revenue** | Net Dollar Retention | > 110% | Monthly |
| **Revenue** | Gross Margin | > 65% | Monthly |
| **Economics** | LTV:CAC | > 3x | Monthly |
| **Economics** | CAC Payback | < 18 mo | Monthly |
| **Cash** | Runway | > 12 mo | Monthly |
| **Cash** | AR > 60 days | < 5% of AR | Monthly |

## Red Flags

- Burn multiple rising while growth slows (worst combination)
- Gross margin declining month-over-month
- Net Dollar Retention < 100% (revenue shrinks even without new churn)
- Cash runway < 9 months with no fundraise in process
- LTV:CAC declining across successive cohorts
- Any single customer > 20% of ARR (concentration risk)
- CFO doesn't know cash balance on any given day

## Integration with Other C-Suite Roles

| When... | CFO works with... | To... |
|---------|-------------------|-------|
| Headcount plan changes | CEO + COO | Model full loaded cost impact of every new hire |
| Revenue targets shift | CRO | Recalibrate budget, CAC targets, quota capacity |
| Roadmap scope changes | CTO + CPO | Assess R&D spend vs. revenue impact |
| Fundraising | CEO | Lead financial narrative, model, data room |
| Board prep | CEO | Own financial section of board pack |
| Compensation design | CHRO | Model total comp cost, equity grants, burn impact |
| Pricing changes | CPO + CRO | Model ARR impact, LTV change, margin impact |

## Resources

- `references/financial_planning.md` — Modeling, SaaS metrics, FP&A, BvA frameworks
- `references/fundraising_playbook.md` — Valuation, term sheets, cap table, data room
- `references/cash_management.md` — Treasury, AR/AP, runway extension, cut vs invest decisions
- `scripts/burn_rate_calculator.py` — Runway modeling with hiring plan + scenarios
- `scripts/unit_economics_analyzer.py` — Per-cohort LTV, per-channel CAC
- `scripts/fundraising_model.py` — Dilution, cap table, multi-round projections


## Proactive Triggers

Surface these without being asked when you detect them in company context:
- Runway < 18 months with no fundraising plan → raise the alarm early
- Burn multiple > 2x for 2+ consecutive months → spending outpacing growth
- Unit economics deteriorating by cohort → acquisition strategy needs review
- No scenario planning done → build base/bull/bear before you need them
- Budget vs actual variance > 20% in any category → investigate immediately

## Output Artifacts

| Request | You Produce |
|---------|-------------|
| "How much runway do we have?" | Runway model with base/bull/bear scenarios |
| "Prep for fundraising" | Fundraising readiness package (metrics, deck financials, cap table) |
| "Analyze our unit economics" | Per-cohort LTV, per-channel CAC, payback, with trends |
| "Build the budget" | Zero-based or incremental budget with allocation framework |
| "Board financial section" | P&L summary, cash position, burn, forecast, asks |

## Reasoning Technique: Chain of Thought

Work through financial logic step by step. Show all math. Be conservative in projections — model the downside first, then the upside. Never round in your favor.

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

---
## SKILL: gb-tufte-report

---
name: tufte-report
description: Create Tufte-inspired data reports and infographic dashboards as standalone HTML files. Uses EB Garamond for text, Monaspace Argon for numbers, Chart.js for interactive charts, and inline SVG sparklines. Produces publication-quality reports with 2-column narrative+data layouts, status dashboards, scroll animations, and responsive mobile support. Use this skill whenever the user wants to create a data report, activity dashboard, infographic, personal analytics page, health tracker visualization, or any document that combines narrative text with interactive charts and tables. Also triggers for "make a report like Tufte", "create an infographic", "build a dashboard", "visualize my data", or requests for beautiful data-driven documents.
---

# Tufte Report — Data-Driven Infographic Skill

Create standalone HTML reports that combine editorial narrative with interactive data visualization in Edward Tufte's style: high information density, minimal chart junk, typography-first design.

## Design Philosophy

Tufte's core principles drive every decision:
- **Data-ink ratio**: every pixel of ink should represent data, not decoration
- **Small multiples**: repeat a design to show comparison, not animation
- **Sparklines**: word-sized graphics that live inside prose
- **Layering**: overview first, then detail on demand
- **Integration**: text and graphics share the same visual space (sidenotes, not footnotes)

The report should feel like a well-edited magazine feature — you read it top to bottom, narrative carries you through the data, and every chart earns its space by answering a specific question.

## Onboarding — Ask Before Building

Before writing ANY code, ask these questions. Do not proceed until all are answered:

1. **What data sources do you have?** (CSV, JSON, SQLite, API endpoint, or raw numbers)
2. **What is the primary question this report should answer?** (one sentence — this becomes the title and drives all design decisions)
3. **How many sections do you need?** (cap at 8 — push back if more are requested; each section should answer one sub-question)
4. **What's the output format?** (standalone HTML file, or embedded component)
5. **Time budget?** Provide an estimate:
   - 1-2 sections with tables only: ~200 LOC, ~5 min bypass / ~10 min manual
   - 3-4 sections with 2-3 charts: ~500 LOC, ~15 min bypass / ~25 min manual
   - 5-8 sections with charts + health data + sparklines: ~1200 LOC, ~30 min bypass / ~50 min manual

## Scope Protection

This skill enforces hard limits to prevent scope creep:

- **Max 8 sections** — if the user asks for more, suggest combining related topics
- **Max 2 chart types per section** — a section gets one primary chart and optionally one supporting chart or table. More than that means the section should split
- **Max 3 colors per chart** — beyond that, use small multiples instead of rainbow legends
- **No 3D charts, no pie charts, no donut charts** — these violate Tufte principles
- **No gratuitous animation** — scroll-reveal on enter is fine; spinning, bouncing, or pulsing is not
- **Every chart must have a caption** — if you can't write a one-sentence caption explaining what the chart shows, the chart shouldn't exist

When the user asks for something outside these limits, respond with: "That would take the report from [current LOC estimate] to [new estimate]. The extra complexity adds [X] but risks [Y]. Shall I proceed, or can we [simpler alternative]?"

## Architecture

```
report.html (standalone, no build step)
├── Google Fonts CDN (EB Garamond)
├── jsDelivr CDN (Monaspace Argon woff2)
├── jsDelivr CDN (Chart.js 4.x UMD)
├── Inline <style> (design system CSS)
├── Inline HTML (semantic structure)
└── Inline <script> (data + Chart.js configs + sparklines + scroll-reveal)
```

No build tools, no frameworks, no npm. One file, opens in any browser.

## Design System

Read `references/design-tokens.md` for the complete CSS variables, typography scale, and color palette.

Read `references/components.md` for the HTML+CSS snippet of every reusable component.

Read `references/charts.md` for Chart.js configuration patterns and inline SVG sparkline code.

## Report Structure Template

Every report follows this skeleton:

```
1. Title + subtitle + data source tags (monospace, subtle)
2. [Optional] Status dashboard (4-column KPI strip)
3. Overview narrative with inline sparklines + TOC sidebar
4. Summary cards (2-4 KPI tiles with sparklines)
5. Sections (each: state-line → chart+narrative aside → table+narrative aside)
6. [Optional] Decision register (threshold table with status colors)
7. Footer (generation date, sources)
```

### Section Pattern

Each section follows this rhythm:
```
<h2> with ↑ back-to-top link
<p class="state-line"> — one italic sentence, the takeaway
<div class="aside-container"> — chart on left, narrative on right
<div class="aside-container"> — table on left, interpretation on right
```

The alternation of chart→narrative→table→narrative creates visual breathing room and prevents "wall of data" fatigue.

### Rules for Narrative Text

- **State-lines** (the italic intro under each heading): one sentence, max 20 words, states the conclusion not the topic. "HRV down 13%, steps down 42%" not "This section covers health metrics"
- **Aside narratives**: 3-4 short paragraphs, each starting with a bold keyword. Written like a newspaper sidebar — facts first, interpretation second
- **Flyouts**: reserved for actionable insights or methodology notes. The ✦ symbol marks them as "pay attention"
- **No "tells its own story"** or similar filler. Every sentence should contain a number or a decision

## Dual-Font Strategy

| Context | Font | Why |
|---------|------|-----|
| All body text, headers, captions | EB Garamond | Classical editorial feel, excellent readability |
| All numbers in tables | Monaspace Argon | Tabular figures align in columns, monospace scannability |
| Big numbers in cards/dashboards | Monaspace Argon | Visual weight, distinct from prose |
| Status indicators, trend percentages | Monaspace Argon | Precision signaling |
| Data source tags, code references | Monaspace Argon | Technical register |
| Ornament separators (:::) | Monaspace Argon with ligatures | Programming aesthetic, replaces floral Unicode |

## Color Principles

Use `--ink` (near-black) for text, `--bg` (warm white) for background. Chart colors must be semantically meaningful — don't assign colors randomly:

- **Orange** (`--spark-claude`, #c45a28): primary data stream, effort/work metrics
- **Green** (`--spark-wispr`, #2a7a5a): growth, positive health signals, English language
- **Purple** (`--spark-social`, #5a5aaa): social/communication metrics
- **Blue** (rgba(42,80,140)): secondary overlay lines on charts
- **Red** (#a02a2a): alerts, negative trends, declining metrics
- **Amber** (#c89000): warnings, watch-level signals
- **Green** (#2a7a3a): healthy baselines, positive trends

Never use more than 3 colors in a single chart. If you need more, use opacity/saturation variations of the same hue.

## Session Lessons (What Goes Wrong)

Based on building the reference report, these are the recurring problems:

1. **Chart.js CDN version**: Use `@4` not a specific patch version — specific versions may not exist
2. **Chart.js defaults**: Set individual properties, never replace entire objects (`Chart.defaults.scale.grid.color = '#eee'` not `Chart.defaults.scale.grid = {color: '#eee'}`)
3. **Legend circles**: Use `usePointStyle: false` with `boxWidth: 8, boxHeight: 8, borderRadius: 4` for true circles. `usePointStyle: true` creates ovals
4. **file:// protocol**: Charts won't load CDN scripts via file://. Always test via localhost
5. **Back-to-back charts**: Always separate consecutive charts with narrative, a table, or an ornament. Two charts in a row = "wall of data"
6. **Table overflow on mobile**: Wrap in `.table-wrapper` and add `.hide-mobile` to secondary columns
7. **Dual-axis charts**: Use sparingly — they invite false visual equivalence. Always label both axes clearly
8. **Narrative overreach**: Don't claim correlations without computing them. "r = 0.10" is more trustworthy than "strong relationship"

## Universal Data Adapter

When the user provides data from any source (CSV, JSON, SQLite, API, raw numbers), normalize it into the standard **ReportData** intermediate format before generating HTML. This decouples data ingestion from report rendering.

Read `references/data-adapter.md` for the ReportData JSON schema, field reference, and adapter instructions for each source type.

**Workflow:**
1. User provides data → identify source type
2. Transform into ReportData JSON (ask user for `meta.question` and desired sections)
3. Confirm the normalized structure with the user
4. Generate HTML from the ReportData using the block library

## Composable Block Library

Reports are assembled from typed blocks, each with a defined data contract. This replaces ad-hoc HTML generation with a systematic approach.

Read `references/blocks.md` for the complete block catalog: sparkline-row, kpi-card, trend-chart, data-table, correlation-matrix, narrative, heatmap, strip-chart.

Each block defines:
- **Data contract** (what JSON shape it expects)
- **HTML template** (copy-paste ready)
- **Composition rules** (how blocks pair and sequence)

## Preview Server

For iterative development, use the built-in live-reload server:

```bash
python3 ~/.claude/skills/tufte-report/scripts/serve.py report.html
```

Serves on `localhost:8042`, auto-reloads on file change with scroll position preserved. Zero dependencies — Python stdlib only.

Read `references/preview-server.md` for details. After generating a report, offer to start the preview server for the user.

