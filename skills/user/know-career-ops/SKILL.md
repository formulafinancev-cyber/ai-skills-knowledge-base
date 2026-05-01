# Career-Ops — AI-Powered Job Search System

## Trigger
Use when conducting a job search, evaluating job postings, customizing CVs, preparing for interviews, or automating application tracking.

## What Is Career-Ops
Multi-agent job search command center. 14 skill modes, A-F scoring across 10 dimensions, ATS-optimized PDF resume generation, career portal scanning via Playwright, batch processing. 740+ listings evaluated, 100+ CVs generated per user.

## Skill Modes (14)
| Mode | Purpose |
|------|---------|
| `analyze` | Deep analysis of job posting (fit score, red flags, opportunities) |
| `score` | A-F score across 10 dimensions |
| `cv-customize` | Tailor CV to specific job posting |
| `cv-generate` | Generate ATS-optimized PDF resume |
| `cover-letter` | Write targeted cover letter |
| `company-research` | Deep company analysis (culture, financials, growth) |
| `interview-prep` | Generate likely questions + model answers |
| `salary-research` | Market rate analysis for role + location |
| `scan-portal` | Scrape job board for matching listings |
| `batch-scan` | Process multiple listings in parallel |
| `track` | Update application status in tracker |
| `follow-up` | Draft follow-up email |
| `negotiate` | Salary negotiation scripts |
| `debrief` | Post-interview analysis + lessons |

## Scoring Dimensions (A-F)
1. Technical fit (skills match)
2. Seniority alignment
3. Culture signals
4. Growth trajectory
5. Compensation range
6. Remote/location
7. Company stability
8. Interview process signals
9. ATS optimization potential
10. Overall recommendation

## Key Commands
```bash
# Analyze single job
career-ops analyze --url "https://company.com/jobs/123"
career-ops score --url "https://..." --cv ./my-cv.pdf

# Batch process
career-ops batch-scan --board linkedin --query "senior engineer" --location "remote"
career-ops batch-score --input listings.json --cv ./cv.pdf

# Generate documents
career-ops cv-customize --job ./job.txt --cv ./base-cv.md
career-ops cv-generate --output ./cv-company-role.pdf
career-ops cover-letter --job ./job.txt --cv ./cv.pdf

# Track applications
career-ops track --company "Acme" --role "Staff Engineer" --status "Applied"
career-ops track --list

# Prep
career-ops interview-prep --job ./job.txt --cv ./cv.pdf
career-ops salary-research --role "Staff Engineer" --location "SF" --yoe 8
```

## Application Tracker
SQLite-based local database:
```
applications.db:
  companies, roles, status, dates, notes, scores, documents
```

## ATS Optimization
- Keyword extraction from job posting
- CV keyword density scoring
- Section ordering for ATS parsing
- Format validation (no tables, no headers in footer)
- Font and margin compliance

## Install
```bash
git clone https://github.com/santifer/career-ops.git
cd career-ops
npm install
npx playwright install chromium
```

## Warning
- Auto-updater overwrites CLAUDE.md and config on session start
- Batch runner uses `--dangerously-skip-permissions`
- Review `update-config.js` before first run
