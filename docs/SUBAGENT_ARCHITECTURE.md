# Multi-Agent & Sub-Agent Architecture

Templates in `agent-lab` separate **orchestration**, **specialized execution**, and **continuous governance** so prompts remain modular, auditable, and easy to delegate across sessions or sub-agents.

---

## Core Roles

```text
                        ┌──────────────────────────┐
                        │       User / Owner       │
                        └────────────┬─────────────┘
                                     │ Phase 0 config + Approval Gates
                                     ▼
                        ┌──────────────────────────┐
                        │       Orchestrator       │
                        │ (prompts/orchestrator.md)│
                        └──────┬────────────┬──────┘
                               │            │
            Delegates scoped   │            │ Configures & schedules
            tasks on demand    ▼            ▼ (e.g. 3x/day)
             ┌───────────────────────┐    ┌────────────────────────┐
             │ Specialist Sub-Agents │    │  Autonomous Maintainer │
             │ (media, browser, API) │    │  (subagents/maintainer)│
             └───────────┬───────────┘    └───────────┬────────────┘
                         │                            │
                         └──────────┬─────────────────┘
                                    ▼
                        ┌──────────────────────────┐
                        │  HANDOFF.md + Snapshots  │
                        │ (Single Source of Truth) │
                        └──────────────────────────┘
```

### 1. Orchestrator (`prompts/orchestrator.md`)
- Owns **Phase 0** onboarding, workspace bootstrapping, and `PROJECT_CONFIG`.
- Maintains the big-picture plan and resolves cross-system dependencies.
- Delegates heavy or narrow tasks to specialist sub-agents instead of overloading a single context window.

### 2. Specialist Sub-Agents (`prompts/subagents/<specialist>.md`)
- Scoped to one domain or tool surface (for example: media cropping & site sync, browser UI fallback, or social API publishing).
- Receive explicit inputs from the Orchestrator (or `HANDOFF.md`), verify pre-flight invariants, execute deterministically, and report structured outputs/IDs back.
- Never silently expand scope (for example, a media sub-agent never edits ad budgets; a browser creative sub-agent never increases spend caps).

### 3. Autonomous Maintainer (`prompts/subagents/maintainer.md`)
- Runs on a recurring schedule (or after major deploys) as a **governance and drift-detection** loop.
- Performs deterministic read-only checks first (parity, safety blocklists, spend pacing, funnel metrics).
- Executes only explicitly pre-authorized, bounded optimizations (such as pausing unsafe ads or throttling high-CPC bid caps within the hard budget cap).
- Escalates any out-of-bounds action through an explicit **`APPROVAL_GATE`** rather than guessing.

### 4. Living Handoff (`HANDOFF.md`)
- Bridges stateless agent runs and scheduled sub-agent invocations.
- Records verified configuration state, active IDs, spend ledger, published content logs, and pending user approvals so no run repeats work or loses critical constraints.
