# agent-lab

A curated library of reusable, sanitized AI agent project templates — complete with **orchestrator prompts**, **specialized sub-agent prompts**, **living handoff templates**, and **battle-tested API/tooling guardrails**.

Every template in this repository follows a strict **Phase 0 interactive onboarding** pattern using explicit `<TEMP_...>` placeholders so you can safely share workflows publicly and instantiate them in minutes without leaking secrets or project-specific configuration.

---

## Project Templates Catalog

| Template | Domain | Agents Included | Core Stack / Integrations | Best For |
| :--- | :--- | :--- | :--- | :--- |
| [`meta-marketing-orchestrator`](./templates/meta-marketing-orchestrator/README.md) | Marketing & Growth | 1 Orchestrator + 4 Sub-Agents (`maintainer`, `media-pipeline`, `organic-social-publisher`, `ads-manager-browser`) | Meta Ads Graph API (`v21.0`), Instagram Graph API, GA4 Data API (`v1beta`), Google Sheets (`gdrive`), Pillow, Static Site Sync | Local events, markets, pop-ups, and product launches |
| [`_starter`](./templates/_starter/README.md) | Template Blueprint | 1 Orchestrator + 1 Maintainer Skeleton | Stack-agnostic | Creating and contributing new project templates |

---

## Repository Structure

```text
agent-lab/
├── README.md                                  # Catalog, quick start, and architecture overview
├── CONTRIBUTING.md                            # How to sanitize & submit new project templates
├── docs/
│   ├── TEMPLATE_CONVENTIONS.md                # <TEMP_...> syntax, Phase 0 onboarding & folder standards
│   └── SUBAGENT_ARCHITECTURE.md               # Orchestrator + Sub-agent + Maintainer + HANDOFF pattern
└── templates/
    ├── _starter/                              # Copy-paste skeleton for new project templates
    │   ├── README.md
    │   ├── prompts/
    │   │   ├── orchestrator.md
    │   │   └── subagents/
    │   │       └── maintainer.md
    │   └── workspace/
    │       ├── .env.example
    │       └── HANDOFF.template.md
    └── meta-marketing-orchestrator/           # Full-stack marketing & autonomous maintainer template
        ├── README.md
        ├── prompts/
        │   ├── orchestrator.md                # Main orchestrator prompt (formerly MetaMarketingAgent_orca.md)
        │   └── subagents/
        │       ├── README.md                  # Sub-agent roster, triggers & boundaries
        │       ├── maintainer.md              # 3x/day scheduled audit & budget-capped optimizer
        │       ├── media-pipeline.md          # Drop-folder ingestion, Pillow crops & site mirror sync
        │       ├── organic-social-publisher.md # IG Graph API publishing, idempotency & 2207051 safety
        │       └── ads-manager-browser.md     # Meta Ads Manager UI creative worker (1885183 workaround)
        └── workspace/
            ├── .env.example                   # Sanitized credential keys
            ├── config.example.yaml            # Standalone PROJECT_CONFIG template
            ├── HANDOFF.template.md            # Living multi-agent state & single source of truth
            └── CAMPAIGN_PLAYBOOK.template.md  # Copy, schedule, handles & creative specs template
```

---

## How to Use a Template

1. **Copy the project template folder** (`templates/<project-slug>/`) into your project directory or working repo.
2. **Initialize your workspace starter files** from `workspace/` (for example, copy `.env.example` to `.env` and populate secrets locally — never commit `.env`).
3. **Launch your primary agent with `prompts/orchestrator.md`.**
   - Every orchestrator prompt starts in **Phase 0**: it inspects your workspace, interviews you to replace all `<TEMP_...>` placeholders, and verifies read-only API access before running mutations.
4. **Attach or schedule the companion sub-agents** from `prompts/subagents/`:
   - Use specialized execution sub-agents (media processing, browser UI, channel publishing) on demand so each worker stays focused with minimal context bloat.
   - Deploy `maintainer.md` as your scheduled autonomous governance/audit agent.

---

## Design Principles

- **Zero Secrets in Templates (`<TEMP_...>`):** Every project-specific domain, ID, coordinate, budget, entity name, and credential path uses `<TEMP_...>` placeholders, paired with explicit instructions forbidding live API calls until Phase 0 completes.
- **Orchestrator + Sub-Agent Separation:** The orchestrator handles onboarding, planning, and cross-system coordination, while sub-agents own narrow, repeatable, high-reliability jobs (auditing, media transforms, browser UI workarounds, API publishing).
- **Single Source of Truth (`HANDOFF.md`):** Multi-agent workflows stay synchronized via a structured living handoff file plus deterministic state snapshots.
- **Battle-Tested Guardrails First:** Platform quirks (rate-limit blocks, API mode limitations, rendering bugs, safety caps) are documented directly in prompts so agents avoid known failure modes.

---

## Contributing a New Project Template

Have a battle-tested multi-agent workflow you want to turn into a shareable template?

1. Copy [`templates/_starter/`](./templates/_starter/) to `templates/<your-project-slug>/`.
2. Follow [`CONTRIBUTING.md`](./CONTRIBUTING.md) and [`docs/TEMPLATE_CONVENTIONS.md`](./docs/TEMPLATE_CONVENTIONS.md) to extract your orchestrator prompt, sub-agent prompts, and sanitized workspace files.
3. Run the sanitization checklist before opening a pull request.