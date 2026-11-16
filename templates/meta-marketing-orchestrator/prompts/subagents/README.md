# Sub-Agent Prompt Templates

These four modular sub-agent prompt templates decompose the responsibilities defined in [`../orchestrator.md`](../orchestrator.md) into focused, safety-bounded roles.

> **Before Using Any Sub-Agent Prompt:**
> Ensure **Phase 0** has been completed with the Orchestrator so every `<TEMP_...>` placeholder is replaced with your verified project configuration and `<workspace_root>/.env` is populated locally.

---

## Sub-Agent Roster & Ownership Matrix

| Sub-Agent | Trigger / Schedule | Primary Inputs | Primary Outputs | Strict Boundaries |
| :--- | :--- | :--- | :--- | :--- |
| [`maintainer.md`](./maintainer.md) *(runtime: `MAINTAINER_PROMPT.md`)* | Scheduled **3x/day** (`9:00 AM`, `3:00 PM`, `11:00 PM` local) or post-deploy | `HANDOFF.md`, `prod-www/index.html`, `drive-www/index.html`, `.env`, Meta/IG/GA4 APIs, Foot-Traffic Sheet | `MAINTAINER_AUDIT_LATEST.md`, `MAINTAINER_AUDIT_<YYYY-MM-DD>.md`, `api/latest_audit_snapshot.json`, `HANDOFF.md` | **NEVER** exceed `hard_spend_cap_usd` (`APPROVAL_GATE`); **NEVER** retry IG publish on `2207051` |
| [`media-pipeline.md`](./media-pipeline.md) | New raw photos in `posts/` or `story/`, or lineup update | Raw photos + Shell metadata (`18, 12, 21, 22, 31`), `prod-www/index.html` | `New Photos/`, `vendorpics/`, `assets/01_organic_carousels/`, `02_stories/`, `03_paid_ads/`, SHA-256 synced `drive-www/` | **ZERO** solid borders; **NO** color emojis in `ImageDraw.text`; **NO** cancelled entities |
| [`organic-social-publisher.md`](./organic-social-publisher.md) | Approved organic carousel/story batch ready in `assets/` | `CAMPAIGN_PLAYBOOK.md`, `api/published_log.json`, public `https://` asset URLs | Published IG carousels/stories, updated `api/published_log.json`, manual fallback captions if `2207051` | Verify `HTTP 200` on every URL first; **NEVER** loop-retry after `2207051`; bio copy `<= 150` chars |
| [`ads-manager-browser.md`](./ads-manager-browser.md) | Meta API creative creation fails with `error_subcode: 1885183` (Dev Mode) | `assets/03_paid_ads/`, UTM URL, campaign/ad-set targets, `ads_cutoff_iso`, `hard_spend_cap_usd` | Ad creatives created/updated in `adsmanager.facebook.com`, screenshots & IDs in `HANDOFF.md` | **NEVER** raise `hard_spend_cap_usd` or unpause triple-locked legacy campaigns; stop on 2FA/CAPTCHA |
