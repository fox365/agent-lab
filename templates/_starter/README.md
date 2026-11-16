# `<TEMP_TEMPLATE_NAME: Project Template Name>`

> Copy this `_starter` folder to `templates/<your-project-slug>/` to author a new shareable project template for `agent-lab`.

## Overview

`<TEMP_SHORT_DESCRIPTION: Brief summary of the workflow, integrations, and what the orchestrator + sub-agents automate.>`

## Included Files

- [`prompts/orchestrator.md`](./prompts/orchestrator.md) — Main orchestrator prompt starting at Phase 0 interactive onboarding.
- [`prompts/subagents/maintainer.md`](./prompts/subagents/maintainer.md) — Autonomous scheduled audit/governance sub-agent skeleton.
- [`workspace/.env.example`](./workspace/.env.example) — Sanitized secret variable names.
- [`workspace/HANDOFF.template.md`](./workspace/HANDOFF.template.md) — Living state template shared across orchestrator and sub-agents.

## Quick Start

1. Copy this folder to your working project or `templates/<your-project-slug>/`.
2. Replace all `<TEMP_...>` placeholders in `prompts/` and `workspace/`.
3. Review the [Sanitization Checklist](../../CONTRIBUTING.md#mandatory-sanitization-checklist) before committing.
