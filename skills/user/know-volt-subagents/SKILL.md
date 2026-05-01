# VoltAgent Awesome Claude Code Subagents (126 agents)

## Trigger
Use when activating a specialized subagent for a specific domain task in Claude Code. Reference any agent below by name or domain.

## What Is It
127+ markdown subagent definition files in 9 categories. Each defines: persona, expertise, tool access, workflow patterns. Installed to `~/.claude/agents/`.

## Categories & Key Agents

### Development (40 agents)
| Agent | When to Use |
|-------|-------------|
| `code-architect` | System design, architecture decisions, ADRs |
| `python-expert` | Python idioms, async, typing, packaging |
| `typescript-expert` | TS types, generics, React patterns |
| `rust-systems-engineer` | Memory safety, lifetimes, async |
| `go-engineer` | Goroutines, channels, interface design |
| `react-specialist` | Components, hooks, state management |
| `sql-optimizer` | Query plans, index strategy, normalization |
| `api-designer` | REST/GraphQL design, versioning, OpenAPI |
| `mobile-developer` | React Native / Flutter cross-platform |
| `webgl-engineer` | Three.js, shaders, 3D rendering |

### Testing (15 agents)
| Agent | When to Use |
|-------|-------------|
| `test-architect` | Test strategy, pyramid, coverage goals |
| `unit-test-specialist` | Fast, isolated unit tests |
| `integration-test-engineer` | Service integration, test containers |
| `e2e-test-engineer` | Playwright/Cypress end-to-end |
| `performance-tester` | Load testing, k6, latency analysis |

### Infrastructure (20 agents)
| Agent | When to Use |
|-------|-------------|
| `kubernetes-engineer` | K8s manifests, Helm, operators |
| `terraform-architect` | IaC, modules, state management |
| `docker-specialist` | Multi-stage builds, compose, security |
| `ci-cd-engineer` | GitHub Actions, GitLab CI pipelines |
| `cloud-cost-optimizer` | Right-sizing, reserved instances, savings |

### Security (12 agents)
| Agent | When to Use |
|-------|-------------|
| `security-auditor` | Code security review, OWASP Top 10 |
| `penetration-tester` | Vulnerability scanning, threat modeling |
| `secrets-manager` | Secret rotation, vault integration |
| `compliance-engineer` | SOC2, GDPR, HIPAA compliance |

### Data & Analytics (18 agents)
| Agent | When to Use |
|-------|-------------|
| `data-pipeline-engineer` | ETL/ELT, Airflow, dbt |
| `ml-engineer` | Model training, feature engineering |
| `analytics-engineer` | Warehouse design, BI tooling |
| `real-time-engineer` | Kafka, Flink, streaming analytics |
| `visualization-expert` | D3.js, chart design, dashboards |

### Product & Process (12 agents)
| Agent | When to Use |
|-------|-------------|
| `product-manager` | PRDs, user stories, roadmaps |
| `technical-writer` | API docs, READMEs, runbooks |
| `agile-coach` | Sprint planning, retrospectives |
| `incident-commander` | Runbooks, post-mortems |

### AI/ML Specialized (10 agents)
| Agent | When to Use |
|-------|-------------|
| `llm-engineer` | Prompt engineering, RAG, fine-tuning |
| `agent-architect` | Multi-agent orchestration design |
| `vector-db-specialist` | Embeddings, similarity search, chunking |
| `ai-safety-engineer` | Guardrails, red-teaming, alignment |

## Install
```bash
claude plugin marketplace add VoltAgent/awesome-claude-code-subagents
# or:
git clone https://github.com/VoltAgent/awesome-claude-code-subagents
cp -r awesome-claude-code-subagents/subagents ~/.claude/agents/
```

## Usage
Agents activate automatically based on context, or explicitly:
```
@agent-sql-optimizer "optimize this query: SELECT ..."
@agent-security-auditor "review this auth implementation"
@agent-ml-engineer "design a feature store for this use case"
```
