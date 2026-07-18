# Job Search Tracker — n8n + AI Scoring

An automated workflow built in [n8n] (https://n8n.io) that monitors multiple job sources (Adzuna, acad.jobs) for positions relevant to a quantitative/data-science/IT background, scores each posting for real fit using an LLM (Gemini), deduplicates against a Google Sheet history, and emails a notification only when genuinely new, relevant postings are found.

## Overview

Built as a hands-on way to learn workflow automation while solving a real problem during an active job search: surfacing relevant postings — including ones with non-obvious job titles — across multiple sources, without manually re-checking job boards every day.

**What it does:**
1. Queries **Adzuna's API** with multiple search terms in parallel (rate-limited via a loop)
2. Scrapes **acad.jobs** across several academic/technical fields (Physics, Math/Stats/Data Science, Computer Science, Earth & Environmental Sciences, Engineering), parsing the HTML directly since there's no public API
3. Normalizes both sources into a common schema and deduplicates postings found via multiple queries/fields
4. Sends each posting's description to **Gemini** with a calibrated recruiter-style prompt, which returns a fit score (0–10), a category tag, and a short rationale — evaluating actual requirement/skill match rather than relying on keyword filtering alone
5. Cross-references against a Google Sheet of previously seen postings to avoid duplicates
6. Appends new, relevant postings to the sheet and sends an email notification — skipped entirely if nothing new was found

