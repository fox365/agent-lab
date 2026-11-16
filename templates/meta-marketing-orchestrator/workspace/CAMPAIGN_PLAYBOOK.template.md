# Campaign Playbook — `<TEMP_PROJECT_NAME: Acme Holiday Makers Market 2026>`

> Copy to `<workspace_root>/prod-www/marketing-2026/CAMPAIGN_PLAYBOOK.md` and populate during Phase 0 / Phase 1.

---

## 1. Event / Campaign Facts (Single Source of Truth)
- **Project Name:** `<TEMP_PROJECT_NAME: Acme Holiday Makers Market 2026>`
- **Dates & Hours:** `<TEMP_EVENT_START: 2026-11-14T10:00:00-0800>` to `<TEMP_EVENT_END: 2026-11-15T15:00:00-0800>`
- **Venue:** `<TEMP_VENUE_NAME: Acme Community Hall>`, `<TEMP_VENUE_ADDRESS: 123 Main St, YourCity, WA 98000>`
- **Website:** `<TEMP_LIVE_SITE_URL: https://example-market.com/>`
- **Paid Ads UTM URL:** `<TEMP_LIVE_SITE_URL: https://example-market.com/>?utm_source=meta&utm_medium=paid_social&utm_campaign=<TEMP_CAMPAIGN_SLUG: acme_market_2026>`
- **Active Featured Lineup Count:** `<TEMP_ACTIVE_COUNT: 13>`
- **Featured Partner Handle:** `<TEMP_PARTNER_HANDLE: @examplecoffee>`
- **Day-2 Only Participants:** `<TEMP_VENDOR_SUN_1: Artisan A (Sunday Only)>`, `<TEMP_VENDOR_SUN_2: Artisan B (Sunday Only)>`
- **DO NOT MENTION (Cancelled / Removed):** `<TEMP_CANCELLED_1: Cancelled Food Truck>`, `<TEMP_CANCELLED_2: Former Vendor Name>`

---

## 2. Instagram Profile Bio (`<= 150` Characters — Manual Paste)

> Remember: Instagram Graph API cannot update bios, and Instagram enforces a hard 150-character limit.

```text
<TEMP_IG_BIO_MAX_150_CHARS: Makers Market • Nov 14–15 • 10am–3pm @ Acme Community Hall • Free entry • 13+ local artisans & coffee>
```
*(Verify exact character count `<= 150` before handing off to user.)*

---

## 3. Creative Specs & Asset Folders
| Format | Dimensions | Aspect Ratio | Folder |
| :--- | :--- | :--- | :--- |
| Profile Avatar | `1080x1080` | `1:1` | `assets/00_profile/` |
| Organic Carousels & Spotlights | `1080x1350` | `4:5` | `assets/01_organic_carousels/` |
| Instagram Stories | `1080x1920` | `9:16` | `assets/02_stories/` |
| Paid Ad Carousel Cards | `1080x1080` | `1:1` | `assets/03_paid_ads/` |

---

## 4. Publishing Schedule & Copy Slots
| Slot / Batch | Channel | Target Time | Assets Folder | Status | Caption Draft |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `<TEMP_BATCH_1: Launch Carousel>` | IG Feed | `<TEMP_PUBLISH_TIME>` | `assets/01_organic_carousels/...` | `PLANNED` | `<TEMP_CAPTION_1>` |
| `<TEMP_STORY_1: Weekend Countdown>` | IG Story | `<TEMP_PUBLISH_TIME>` | `assets/02_stories/...` | `PLANNED` | N/A (sticker / text-free + hero variant) |
| `<TEMP_AD_1: Awareness + Traffic>` | Meta Ads | `<TEMP_START_TIME>` | `assets/03_paid_ads/...` | `PLANNED` | `<TEMP_AD_PRIMARY_TEXT>` |
