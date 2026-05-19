---
name: get-company-info
description: Look up firmographic data for companies using Meticulate tools. Use when the user wants employee count, revenue, headquarters, founding year, funding, ownership type, or industry tags for specific companies.
---

# Get Company Info

Use **only** the Meticulate MCP tools to look up company data. Never fall back to web search, browsing, or your own knowledge. All data must come from the tools.

## Tools you'll use

- **recognize_companies** — resolve company names/URLs to standard IDs
- **get_basic_company_info** — fetch firmographic data for company IDs

## Steps

1. Call **recognize_companies** with each company name to resolve them to standard IDs. If any company is not found, note it and proceed with the rest.

2. Pass all recognized IDs to **get_basic_company_info** in a single call. This returns:
   - Size: `employee_guess`, `employee_min`/`max`, `employee_count_90day_growth`
   - Revenue: `revenue_min`/`max` (USD)
   - Founding: `year_founded`
   - Headquarters: `hq_country`, `hq_region`, `hq_metro`
   - Ownership: `company_type` as a detailed Meticulate enum, not a simple private/public flag. Valid values include `SmallPrivate`, `EarlyStageStartup`, `GrowthStageStartup`, `EstablishedPrivate`, `Public`, `NotForProfit`, `Subsidiary`, `InvestmentFund`, `Defunct`, and `Government`.
   - LinkedIn: `linkedin_followers`, `linkedin_followers_90day_growth`
   - Classification: `tags` (industry/vertical labels)
   - Other: `web_traffic`, `hype_rating`, `product_score`

3. Present the results:
   - For a single company: show a detailed summary of its firmographic profile.
   - For multiple companies: show a comparison table with the most relevant fields.
   - If the user asked a specific question (e.g. "which is the biggest"), highlight the relevant field and sort by it.
   - If the user asks whether companies are public or private, map `SmallPrivate`, `EarlyStageStartup`, `GrowthStageStartup`, and `EstablishedPrivate` to private; map `Public` to public; call out `Subsidiary`, `Defunct`, `Government`, `NotForProfit`, and `InvestmentFund` separately.

4. If the question goes beyond firmographics (e.g. qualitative assessments, custom metrics, fundraising, or data not in the standard fields), suggest using the **research-companies** skill to create a custom topic for deeper analysis.
