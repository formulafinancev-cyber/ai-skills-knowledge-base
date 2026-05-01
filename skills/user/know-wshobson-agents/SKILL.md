# wshobson/agents — 73 Focused Plugins, 112 Agents, 146 Skills

## Trigger
Use when needing specialized agent personas for specific technical domains: ML, data science, DevOps, security, frontend, API design, database optimization.

## What Is It
73 focused plugins with 112 specialized agents and 146 skills optimized for minimal token usage. Each agent is a focused prompt persona with domain expertise.

## Agent Categories

### Engineering
| Agent | Activate | Purpose |
|-------|---------|---------|
| `backend-architect` | `/backend` | API design, microservices, system design |
| `frontend-specialist` | `/frontend` | React/Vue/Svelte patterns, a11y |
| `api-designer` | `/api` | REST/GraphQL/gRPC design + OpenAPI specs |
| `database-optimizer` | `/db` | Query optimization, schema design, indexes |
| `performance-engineer` | `/perf` | Profiling, bottleneck analysis, benchmarks |
| `refactoring-expert` | `/refactor` | Code smells, clean architecture, SOLID |

### Data & ML
| Agent | Activate | Purpose |
|-------|---------|---------|
| `ml-engineer` | `/ml` | Model architecture, training pipelines |
| `data-scientist` | `/ds` | Statistical analysis, A/B testing, EDA |
| `data-engineer` | `/de` | ETL/ELT, pipelines, data quality |
| `mlops-engineer` | `/mlops` | Model deployment, monitoring, drift detection |
| `analytics-engineer` | `/analytics` | dbt, Snowflake, BI tooling |

### Infrastructure & Security
| Agent | Activate | Purpose |
|-------|---------|---------|
| `devops-engineer` | `/devops` | CI/CD, Docker, K8s, Terraform |
| `security-analyst` | `/security` | OWASP, threat modeling, vulnerability analysis |
| `cloud-architect` | `/cloud` | AWS/GCP/Azure architecture patterns |
| `sre-engineer` | `/sre` | Reliability, SLOs, incident response |

### Product & Process
| Agent | Activate | Purpose |
|-------|---------|---------|
| `product-manager` | `/pm` | PRD writing, user stories, prioritization |
| `technical-writer` | `/docs` | API docs, README, architecture docs |
| `code-reviewer` | `/review` | PR review, code quality, best practices |
| `architect` | `/arch` | System architecture, ADRs, trade-offs |

## Orchestration Patterns (16 workflows)

### Feature Development
```
/pm → PRD
/arch → system design
/backend + /frontend → parallel implementation
/review → code review
/docs → documentation
```

### Data Pipeline
```
/de → pipeline design
/ds → data validation strategy
/mlops → deployment + monitoring
/sre → alerting + SLOs
```

### Security Audit
```
/security → threat model
/review → code security review
/devops → infra security
/docs → security runbook
```

## Token Optimization
Each agent: ~200-400 tokens system prompt (vs 2000+ in full-featured frameworks). Designed for high-frequency use without burning context.

## Install
```bash
/plugin marketplace add wshobson/agents
```
Or manually:
```bash
git clone https://github.com/wshobson/agents ~/.claude/agents/wshobson
```
