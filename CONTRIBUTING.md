# Contributing to agent-lab

Thanks for sharing reusable AI agent project templates! The goal of `agent-lab` is to turn real, battle-tested agent workflows into clean, safe, copy-and-run templates that anyone can adapt in Phase 0.

---

## Adding a New Project Template

1. **Copy the starter blueprint:**
   ```bash
   cp -r templates/_starter templates/<your-project-slug>
   ```
   Use lowercase kebab-case for `<your-project-slug>` (for example, `meta-marketing-orchestrator`, `cloudflare-zt-audit`, `release-triage-ops`).

2. **Organize prompts cleanly:**
   - `prompts/orchestrator.md`: End-to-end mission, `PROJECT_CONFIG` registry, Phase 0 interactive onboarding, high-level phases, and platform guardrails.
   - `prompts/subagents/README.md`: Sub-agent roster explaining when each sub-agent runs, its inputs/outputs, and escalation boundaries.
   - `prompts/subagents/<role>.md`: Standalone prompt templates for scheduled maintainers, browser workers, media/data pipelines, or channel publishers.

3. **Include starter workspace artifacts (`workspace/`):**
   - `.env.example`: Every required secret key name with dummy values (no real secrets).
   - `HANDOFF.template.md`: Living state file template so the orchestrator and sub-agents share one source of truth.
   - Optional `config.example.yaml` or playbook/spec templates referenced by your prompts.

4. **Update the catalog in root [`README.md`](./README.md):**
   Add a row to the **Project Templates Catalog** table with domain, included agents, integrations, and best-fit use cases.

---

## Mandatory Sanitization Checklist

Before committing or opening a pull request, verify **every file** in your template passes all checks below:

- [ ] **No real credentials or tokens:** Search for API keys, OAuth tokens, service account JSON blobs, or `.env` files. Only `.env.example` with `<TEMP_...>` placeholders may be committed.
- [ ] **No real IDs or PII:** Replace account IDs, property IDs, sheet IDs, phone numbers, personal emails, street addresses, GPS coordinates, and private URLs with `<TEMP_KEY: example>` placeholders.
- [ ] **No real client/vendor/internal names:** Scrub proprietary brand, vendor, customer, or colleague names into neutral examples (e.g., `Acme Makers Market`, `@examplepartner`, `Vendor A`).
- [ ] **No hardcoded local machine user paths:** Replace personal home folders or local repo paths with `<TEMP_WORKSPACE_ROOT: ...>` or relative paths.
- [ ] **Phase 0 safety gate present:** Both `orchestrator.md` and autonomous sub-agent prompts explicitly block live mutating/API calls until `<TEMP_...>` values are replaced.
- [ ] **Hard safety/cost guardrails preserved:** Include spend caps, read-only preflight checks, approval gates, and any hard-won platform failure workarounds in a dedicated **Guardrails / Lessons Learned** section.

### Quick Pre-Commit Verification

```bash
# 1. Confirm no forbidden secret files are staged
git status

# 2. Scan for real-looking tokens or personal paths (customize patterns as needed)
grep -rnE "(EAAB|AIza|sk-|ghp_|gho_|xoxb-|BEGIN PRIVATE KEY)" templates/
```
