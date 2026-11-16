# Agent Handoff — `<TEMP_PROJECT_NAME: Acme Holiday Makers Market 2026>`

**Last Updated:** `<TEMP_TIMESTAMP_ISO>`  
**Timezone:** `<TEMP_TIMEZONE: America/Los_Angeles>`  
**Campaign Slug:** `<TEMP_CAMPAIGN_SLUG: acme_market_2026>`

---

## 1. Phase 0 Preflight Status
- [ ] All `<TEMP_...>` values replaced in `PROJECT_CONFIG` and `MAINTAINER_PROMPT.md`
- [ ] `.env` and GA4 service account JSON verified locally (never printed or committed)
- [ ] Meta Graph API (`v21.0`) permissions verified (`ads_read`, `ads_management`, `instagram_basic`, `instagram_content_publish`, `instagram_manage_insights`, `pages_read_engagement`)
- [ ] Ad Account (`account_status == 1`, `disable_reason == 0`) & `spend_cap` aligned to `$<TEMP_HARD_CAP_USD: 50.00>`
- [ ] GA4 `v1beta` test `runReport` verified
- [ ] Optional offline Foot-Traffic Sheet export verified (`gdrive readonly export`)

---

## 2. Website Parity & Lineup Safety
- **Live Site URL:** `<TEMP_LIVE_SITE_URL: https://example-market.com/>`
- **Active Featured Count:** `<TEMP_ACTIVE_COUNT: 13>`
- **`prod-www` <-> `drive-www` SHA-256 Parity:** `PENDING`
- **Live Image `HTTP 200` Check:** `PENDING`
- **Removed / Cancelled Entities Blocklist:**
  - `<TEMP_CANCELLED_1: Cancelled Food Truck>`
  - `<TEMP_CANCELLED_2: Former Vendor Name>`

---

## 3. Paid Meta Ads Ledger (`hard_spend_cap_usd`: `$<TEMP_HARD_CAP_USD: 50.00>`)
- **Account `amount_spent`:** `$0.00`
- **Account `spend_cap`:** `$<TEMP_HARD_CAP_USD: 50.00>` (`5000` cents)
- **Ads Cutoff (`end_time`):** `<TEMP_ADS_CUTOFF: 2026-11-15T13:30:00-0800>`
- **Legacy Campaigns Triple-Locked (`PAUSED` at Campaign + Ad Set + Ad):** `PENDING`

| Campaign / Objective | Ad Set ID | Status | Lifetime Budget | Budget Remaining | Bid Strategy | End Time |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Awareness (`OUTCOME_AWARENESS`) | `<TEMP_ID>` | `PENDING` | `$25.00` | `$25.00` | `TBD` | `<TEMP_ADS_CUTOFF>` |
| Traffic (`OUTCOME_TRAFFIC`) | `<TEMP_ID>` | `PENDING` | `$25.00` | `$25.00` | `TBD` | `<TEMP_ADS_CUTOFF>` |

> **Meta App Dev Mode (`error_subcode: 1885183`):** Track any UI creative updates delegated to [`ads-manager-browser`](../prompts/subagents/ads-manager-browser.md) here.

---

## 4. Organic Instagram Publishing State
- **IG User ID:** `<TEMP_IG_USER_ID: 17841400000000000>`
- **Published Log (`api/published_log.json`):** `0` entries
- **Burst Block (`2207051`) Cooldown Active:** `No`

---

## 5. Latest Maintainer Audit Summary
- **Schedule:** `9:00 AM`, `3:00 PM`, `11:00 PM` `<TEMP_TIMEZONE: America/Los_Angeles>`
- **Last Audit Run:** `N/A`
- **Autonomous Rules Fired:** None yet

---

## 6. Pending Approvals (`APPROVAL_GATE`) & Next Actions
- Complete **Phase 0** onboarding before running live mutations.
