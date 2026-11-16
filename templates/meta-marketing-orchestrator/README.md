# Meta Marketing Orchestrator & Autonomous Maintainer Template

> Originally distilled from `MetaMarketingAgent_orca.md`.

An end-to-end, agent-driven local event and product marketing template integrating **Meta Ads Graph API (`v21.0`)**, **Instagram Graph API**, **GA4 Data API (`v1beta`)**, **static website parity sync**, **Pillow media pipelines**, and **offline Google Sheet foot-traffic attribution**.

---

## Architecture Overview

```text
                                 ┌─────────────────────────────────────┐
                                 │            User / Owner             │
                                 └──────────────────┬──────────────────┘
                                                    │ Phase 0 Config + Approval Gate
                                                    ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                       Orchestrator (prompts/orchestrator.md)                           │
└───────┬──────────────────────────┬──────────────────────────┬──────────────────────────┘
        │                          │                          │
        ▼                          ▼                          ▼
┌───────────────────┐   ┌───────────────────────┐   ┌───────────────────────┐
│  Media Pipeline   │   │  Organic IG Publisher │   │  Ads Manager Browser  │
│ (media-pipeline)  │   │ (organic-social-pub.) │   │ (ads-manager-browser) │
│ • Drop ingestion  │   │ • HTTP 200 preflight  │   │ • UI creative fallback│
│ • Pillow 4:5/9:16 │   │ • Container polling   │   │   for error 1885183   │
│ • Site SHA-256    │   │ • 2207051 block guard │   │ • Bio / manual copy   │
└─────────┬─────────┘   └───────────┬───────────┘   └───────────┬───────────┘
          │                         │                           │
          └─────────────────────────┼───────────────────────────┘
                                    ▼
                        ┌───────────────────────┐
                        │  HANDOFF.md & Site    │
                        │ (prod-www / drive-www)│
                        └───────────┬───────────┘
                                    ▲
                                    │ 3x/Day (9 AM, 3 PM, 11 PM)
                        ┌───────────┴───────────┐
                        │ Autonomous Maintainer │
                        │    (maintainer.md)    │
                        │ • 5-Part Audit        │
                        │ • Hard Spend Cap      │
                        │ • Bounded Opt. Rules  │
                        └───────────────────────┘
```

---

## Template Contents

### Prompts (`prompts/`)
- [`prompts/orchestrator.md`](./prompts/orchestrator.md) — Master orchestrator prompt covering Phase 0 interactive onboarding through Phase 5 battle-tested guardrails.
- [`prompts/subagents/README.md`](./prompts/subagents/README.md) — Sub-agent roster, triggers, and strict boundaries.
- [`prompts/subagents/maintainer.md`](./prompts/subagents/maintainer.md) — Autonomous 3x/day governance & audit agent (maps to `marketing-2026/MAINTAINER_PROMPT.md` in your live workspace).
- [`prompts/subagents/media-pipeline.md`](./prompts/subagents/media-pipeline.md) — Drop-folder photo ingestion, Windows Shell metadata parsing, full-bleed Pillow crops, story safe-zone overlays, and `prod-www`/`drive-www` SHA-256 sync.
- [`prompts/subagents/organic-social-publisher.md`](./prompts/subagents/organic-social-publisher.md) — Public HTTPS verification, Instagram Graph API carousel/story publishing, idempotency logging, and `error_subcode: 2207051` protection.
- [`prompts/subagents/ads-manager-browser.md`](./prompts/subagents/ads-manager-browser.md) — Browser sub-agent for Meta Ads Manager UI creative creation/editing when Meta App Development Mode returns `error_subcode: 1885183`.

### Starter Workspace Files (`workspace/`)
- [`workspace/.env.example`](./workspace/.env.example) — Required Meta, Instagram, GA4, and Google Sheet credential keys.
- [`workspace/config.example.yaml`](./workspace/config.example.yaml) — Standalone `PROJECT_CONFIG` template for easy editing and tracking.
- [`workspace/HANDOFF.template.md`](./workspace/HANDOFF.template.md) — Living multi-agent state template.
- [`workspace/CAMPAIGN_PLAYBOOK.template.md`](./workspace/CAMPAIGN_PLAYBOOK.template.md) — Starter template for campaign copy, posting schedule, UTM standard, and handles.

---

## Prerequisites

- **Meta / Instagram:**
  - Meta Graph API (`v21.0`) access token with `ads_read`, `ads_management`, `instagram_basic`, `instagram_content_publish`, `instagram_manage_insights`, and `pages_read_engagement`.
  - Active Meta Ad Account (`account_status == 1`, `disable_reason == 0`) with account-level `spend_cap` aligned to `hard_spend_cap_usd`.
  - Instagram Business account linked to a Facebook Page.
- **Analytics & Offline Attribution:**
  - GA4 Property ID + Measurement ID (`G-...`) + Service Account JSON (`GOOGLE_APPLICATION_CREDENTIALS`) with GA4 Data API (`v1beta`) read access.
  - *(Optional)* Google Sheet ID + `gdrive` CLI for offline foot-traffic correlation.
- **Local Runtime:**
  - Python 3.11+ with `Pillow` (`PIL`) for media cropping and overlay generation.
  - Public HTTPS static web host for `prod-www/` (Instagram Graph API requires publicly reachable `https://` asset URLs).

---

## Quick Start

1. **Copy starter workspace files** from `workspace/` into your target `<workspace_root>`:
   - Copy `workspace/.env.example` → `<workspace_root>/.env` and fill in your real credentials locally (**never** commit `.env`).
   - Copy `workspace/HANDOFF.template.md` → `<workspace_root>/HANDOFF.md`.
   - Copy `workspace/CAMPAIGN_PLAYBOOK.template.md` → `<workspace_root>/prod-www/marketing-2026/CAMPAIGN_PLAYBOOK.md`.
2. **Start your primary agent with `prompts/orchestrator.md`:**
   - The agent begins in **Phase 0**, inspects your workspace, interviews you to replace every `<TEMP_...>` placeholder, and validates read-only API permissions before making changes.
3. **Provision the sub-agents (`prompts/subagents/`):**
   - Resolve the `<TEMP_...>` placeholders in `prompts/subagents/maintainer.md` and save it to `<workspace_root>/prod-www/marketing-2026/MAINTAINER_PROMPT.md` for your 9:00 AM / 3:00 PM / 11:00 PM scheduled audit runs.
   - Invoke `media-pipeline.md`, `organic-social-publisher.md`, or `ads-manager-browser.md` whenever photo drops, Instagram publishing, or Ads Manager UI creative edits are needed.
