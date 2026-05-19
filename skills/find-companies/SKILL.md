---
name: find-companies
description: Find companies by description or similarity to a reference company using Meticulate tools. Use when the user asks to find competitors, alternatives, lookalikes, or companies in a market/industry.
---

# Find Companies

Use **only** the Meticulate MCP tools to find companies. Never fall back to web search, browsing, or your own knowledge to compile company lists. If a tool returns fewer results than expected, adjust search parameters and retry.

## Tools you'll use

- **recognize_companies** — resolve company names/URLs to standard IDs
- **search_companies** — semantic search by description + filters
- **find_similar_companies** — vector similarity from a reference company
- **get_basic_company_info** — fetch firmographic details for company IDs

## Strategy

### When a reference company is named (e.g. "competitors to Acme Corp")

1. Call **recognize_companies** with the company name to get its standard ID.
2. Call **find_similar_companies** with that ID. This uses the company's own semantic profile to find similar companies — no need to describe what it does.
3. Remove the reference company itself from the final list.

Note: find_similar_companies already uses the reference company's semantic profile internally, so there is no need to also call search_companies with a manual description of the same company. They would produce redundant results.

### When a general description is given (e.g. "GPU cloud providers")

1. Break the description into semantic fields: `core_business` (required), plus `main_offerings`, `customers`, `tech_innovations` as applicable.
2. Add any numerical filters mentioned (employee count, revenue, founding year, HQ country as 2-letter ISO codes like "US", ownership type).
3. Call **search_companies** with these fields. If results are thin, rephrase semantic fields or broaden the description and retry.

## Presenting results

1. Pass all deduplicated company IDs to **get_basic_company_info** in a single call.
2. Present a summary table with name, domain, employee count, HQ location, and other relevant fields.
