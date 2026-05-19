---
name: research-companies
description: Run custom research questions across companies using Meticulate topics. Use when the user wants to classify, score, estimate metrics, or generate text insights about companies — anything beyond basic firmographic data.
---

# Research Companies

Use **only** the Meticulate MCP tools to answer research questions. Never fall back to web search, browsing, or your own knowledge. All answers must come from the tools.

## Tools you'll use

- **recognize_companies** — resolve company names/URLs to standard IDs
- **search_companies** — find companies by description (if names aren't provided)
- **list_topics** — see existing topic definitions
- **create_topics** — create new research questions
- **run_topics_on_companies** — start computing answers
- **get_topic_answers** — retrieve results (poll until complete)

## Steps

1. **Identify target companies.** If names are provided, call **recognize_companies**. If a description is provided, call **search_companies** first.

2. **Check for existing topics — do NOT skip this step.** You MUST call **list_topics** before creating anything. If a topic already answers the question (even approximately), reuse its ID and skip to step 4. Only proceed to step 3 if no existing topic matches.

3. **Create a topic** with **create_topics** if none exists. Choose the right format:
   - `score` — rating/ranking questions (0-5 scale)
   - `number` — numeric estimates (e.g. revenue, location count)
   - `singleselect` — classification into one category
   - `multiselect` — tagging with multiple labels
   - `text_output` — open-ended text answers

   Tips for writing good topics:
   - For singleselect/multiselect: frame as "Does this company have X?" rather than "What does this company do?" — targeted framing catches signals at large diversified companies.
   - For options: write 10-15 word descriptions with observable signals that differentiate each option. Describe how to identify a company that fits, not why the option matters.
   - For score: provide a rubric where each level is specific enough that two independent reviewers would assign the same score.
   - For number: include the unit in `stat_to_estimate` when values span wide magnitudes (e.g. "Annual revenue in millions of USD").
   - Pick 1-4 `standard_elements` in `info_to_use`. Most classification questions only need `basic_firmographics`. Add `landing_page` only for product positioning detail. Set `websearch_volume` only for recent news or events.

4. **Run the topic.** Call **run_topics_on_companies** with the company IDs and topic ID(s).

5. **Poll for results.** Topics take 30-120 seconds to compute. Repeat this loop until done:
   - Wait 30 seconds before polling again. In Codex, run `sleep 30` with the local shell when available.
   - Call **get_topic_answers** with the same company_ids and topic_ids
   - If `overall_status` is `complete`, stop and present results
   - If `overall_status` is `computing`, loop again — do NOT skip the sleep, drop companies, or stop early

6. **Present the answers** organized by company. If the question implies a ranking or comparison, sort accordingly.
