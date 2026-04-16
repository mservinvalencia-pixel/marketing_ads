# Marketing Analytics Technical Assignment

This repository contains my solution for a cross-channel marketing analytics technical assignment.

## Objective

Transform raw advertising data from three major platforms into a unified analytical model and build a one-page dashboard with actionable cross-channel insights.

## Data Sources

The analysis integrates campaign-level data from:

- Facebook Ads
- Google Ads
- TikTok Ads

Each source includes a different schema, so the main challenge was to standardize shared fields while preserving platform-specific metrics.

## Approach

### 1. Data ingestion
The three CSV files were uploaded into BigQuery as source tables:

- `facebook_ads`
- `google_ads`
- `tiktok_ads`

### 2. Data modeling
A unified table called `unified_ads` was created using `UNION ALL`.

Key modeling decisions:

- Standardized common fields such as:
  - `date`
  - `platform`
  - `campaign_id`
  - `campaign_name`
  - `ad_group_id`
  - `ad_group_name`
  - `impressions`
  - `clicks`
  - `spend`
  - `conversions`

- Renamed source-specific fields to a common structure:
  - Facebook `ad_set_id` → `ad_group_id`
  - Facebook `ad_set_name` → `ad_group_name`
  - TikTok `adgroup_id` → `ad_group_id`
  - TikTok `adgroup_name` → `ad_group_name`
  - Google/TikTok `cost` → `spend`

- Preserved platform-specific metrics using `NULL` when not applicable:
  - Google: `conversion_value`, `avg_cpc`, `quality_score`, `search_impression_share`
  - Facebook: `engagement_rate`, `reach`, `frequency`
  - TikTok: `video_watch_25`, `video_watch_50`, `video_watch_75`, `video_watch_100`, `likes`, `shares`, `comments`

### 3. Metric design
To ensure cross-channel consistency, core metrics were calculated in the dashboard layer instead of relying on source-native definitions.

Calculated metrics:

- **CTR** = clicks / impressions
- **CPC** = spend / clicks
- **Conversion Rate** = conversions / clicks
- **CPM** = (spend / impressions) * 1000

This ensures comparability across all platforms.

### 4. Dashboard
The dashboard was built in Looker Studio and designed to answer four key questions:

- How does the funnel perform overall?
- Which platform generates the most volume?
- Which platform converts more efficiently?
- How do cost and conversion efficiency compare across channels?

## Deliverables

- Live dashboard: https://datastudio.google.com/s/s_0HPaFkskU
- ALL PROCESS Video walkthrough: https://drive.google.com/file/d/1eqVlZ80Psu2-52kYnjT4IDGkIG53LVBL/view?usp=sharing


## Key Insights

- Google shows the strongest conversion efficiency, despite a higher CPC, suggesting higher-intent traffic.
- TikTok drives the largest impression volume, but lower conversion efficiency, indicating a top-of-funnel role.
- Facebook provides a more balanced performance between scale and efficiency.
## - Final Insight: Facebook emerges as the most balanced channel, combining a conversion rate close to Google with a CPC closer to TikTok, making it the most efficient option for investment.


## Tech Stack

- BigQuery
- SQL
- Looker Studio

## Notes

This project focuses on cross-channel comparability and practical business interpretation rather than platform-native reporting alone.
