# Template Conventions

All project templates in `agent-lab` follow consistent conventions so users and AI agents can understand and adopt any project quickly.

---

## 1. Directory Standard (`templates/<project-slug>/`)

Every project template is self-contained under `templates/<project-slug>/`:

```text
templates/<project-slug>/
├── README.md                  # Architecture, prerequisites, quick start, & runtime layout
├── prompts/
│   ├── orchestrator.md        # Primary orchestrator prompt (starts at Phase 0)
│   └── subagents/
│       ├── README.md          # Roster, invocation triggers, & ownership matrix
│       └── <subagent>.md      # Modular, standalone sub-agent prompt templates
└── workspace/
    ├── .env.example           # Secret variable names with <TEMP_...> placeholders
    ├── config.example.yaml    # Optional extracted config registry
    └── HANDOFF.template.md    # Living state template shared across agents
```

### Naming Rules
- **Template folders:** lowercase `kebab-case` describing the capability (e.g., `meta-marketing-orchestrator`).
- **Orchestrator prompt:** always `prompts/orchestrator.md`.
- **Sub-agent prompts:** lowercase `kebab-case` role names under `prompts/subagents/` (e.g., `maintainer.md`, `media-pipeline.md`, `ads-manager-browser.md`).
- **Starter/template workspace files:** suffix with `.example` (for configs/env) or `.template.md` (for Markdown templates copied into a live workspace).

---

## 2. Placeholder Syntax (`<TEMP_...>`)

Never leave blank `TODO` fields without context, and never leave real project values in place. Use explicit `<TEMP_...>` placeholders with a realistic example value:

```yaml
PROJECT_CONFIG:
  project_name: "<TEMP_PROJECT_NAME: Acme Holiday Makers Market 2026>"
  campaign_slug: "<TEMP_CAMPAIGN_SLUG: acme_market_2026>"
  live_site_url: "<TEMP_LIVE_SITE_URL: https://example-market.com/>"
  hard_spend_cap_usd: 50.00  # <TEMP_HARD_CAP_USD: $50.00 — NEVER exceed without sign-off>
```

### Why This Format Works
1. **Unambiguous detection:** Any agent (or grep check) can immediately detect unresolved `<TEMP_` strings and refuse to run live API mutations.
2. **Self-documenting defaults:** Including a realistic sample after the colon (`: Acme Holiday Makers Market 2026`) teaches the agent the exact expected format (ISO timestamps, slug style, `act_` prefixes, etc.) without exposing real data.
3. **Zero accidental leakage:** Real credentials stay strictly in `<workspace_root>/.env` and are referenced in prompts only by environment variable name.

---

## 3. The Phase 0 Interactive Onboarding Pattern

Every `prompts/orchestrator.md` starts with **Phase 0**:

1. **Inspect Workspace First:** Check existing files, directories, and `.env` key names (never print secret values).
2. **Interview the User:** Ask concise, batched questions to replace every `<TEMP_...>` value in `PROJECT_CONFIG` and `workspace/` files.
3. **Verify Read-Only Access & Scopes:** Test API permissions, account status, and safety caps (for example, spend caps or dry-run endpoints) *before* creating assets, modifying sites, or publishing.

---

## 4. Guardrails & Lessons Learned Section

Real-world integrations fail in specific, undocumented ways (API mode restrictions, silent rate-limit blocks, OS shell encoding issues, font rendering pitfalls). Capture every resolved gotcha as an explicit numbered rule inside the prompt that owns that surface so future runs never repeat the mistake.
