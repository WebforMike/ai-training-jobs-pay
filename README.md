# AI training jobs and pay

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24525171.svg)](https://doi.org/10.5281/zenodo.24525171)
[![AI Training Pay MCP connector](https://glama.ai/mcp/connectors/com.aitrainingpay/ai-training-jobs/badges/score.svg)](https://glama.ai/mcp/connectors/com.aitrainingpay/ai-training-jobs)

Open data and a free MCP server for AI training work: RLHF, model evaluation, data annotation, expert data, language and voice roles. Maintained by [AI Training Pay](https://www.aitrainingpay.com), which reads the public job boards of 13 AI training platforms and records the pay each role states.

Snapshot in this repo: 2026-11-25, 4,284 open roles. The live versions of every file update with each data refresh on the site.

## MCP server

Listed in the [official MCP registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.aitrainingpay) as `com.aitrainingpay/ai-training-jobs` and on [Glama](https://glama.ai/mcp/connectors/com.aitrainingpay/ai-training-jobs).

A remote MCP server with no key and no sign-in. Streamable HTTP:

```
https://www.aitrainingpay.com/api/mcp
```

Add it to Claude Desktop, Claude Code, Cursor or any MCP client:

```json
{
  "mcpServers": {
    "ai-training-pay": { "type": "http", "url": "https://www.aitrainingpay.com/api/mcp" }
  }
}
```

Claude Code: `claude mcp add --transport http ai-training-pay https://www.aitrainingpay.com/api/mcp`

| Tool | What it returns |
|---|---|
| `search_ai_training_jobs` | Open roles across platforms, best-paid first: title, platform, field, places, stated pay and a link. Filters: query, field, platform, language, country, minimum hourly pay, remote only. |
| `ai_training_pay` | Median listed hourly pay and open-role counts, overall or by field, platform or language. "Up to" ceilings are reported separately and never mixed into medians. |
| `ai_training_platform` | A sourced profile of one platform (Mercor, Outlier, DataAnnotation, Handshake AI, micro1, xAI and others): whether it's legit, who runs it, how and when it pays, how hiring works, with source links. |
| `new_ai_training_jobs` | Roles first posted in the last 7 days, best-paid first. |
| `list_platforms_and_fields` | Every platform profiled and every field id the other tools accept. |

All tools are read-only. Results are capped at 25 rows and ordered by pay. Some platforms pay the site referral bonuses; that never changes any ranking. Medians need at least 5 priced roles.

There is also a JSON API (`/api/v1/roles`) and embeddable job widgets: https://www.aitrainingpay.com/developers

## Data files

| File | Contents |
|---|---|
| `data/roles.csv`, `data/roles.json` | One row per open role: platform, title, field, language, places, on-site flag, stated pay (min, max, unit, ceiling flag), hourly range where the pay can be stated per hour, stated weekly hours, credentials required, posted and first-seen dates, URL. No listing description text. |
| `data/pay-by-field.csv` | Open roles, roles with an hourly range, median and 75th percentile of listed hourly pay, and ceiling-only roles by field. |
| `data/pay-by-platform.csv` | Open roles, median and top listed hourly pay by platform, with the count of roles that state only a ceiling and their median ceiling. |
| `data/trends.csv` | Daily count and median since 2026-10-19, overall, by platform and by field. |

Live copies: https://www.aitrainingpay.com/open-data

### How pay is recorded

- Pay is what the listing states. Hourly ranges use the midpoint of the stated range.
- Listings that give only a maximum ("up to $X/hr") are flagged as ceilings and left out of every median, because a ceiling isn't what a role typically pays.
- Per-task pay stays per task; it isn't converted to an hourly figure.
- A role posted on two platforms with the same title and identical pay is counted once.

Full method: https://www.aitrainingpay.com/methodology

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please credit and link AI Training Pay (https://www.aitrainingpay.com).

> AI Training Pay (2026). AI training jobs and pay [Data set]. Zenodo. https://doi.org/10.5281/zenodo.24525171

That DOI always resolves to the latest release. Each dated release also has its own DOI, listed on [Zenodo](https://doi.org/10.5281/zenodo.24525171); cite that one when you need the exact files you used.

Corrections: https://www.aitrainingpay.com/about#corrections
