# Tools reference

Every tool here is read only. Server: `https://unboundgeo.com/api/mcp`. Parameters below are the ones the server documents. Do not pass anything else.

## Call order for the audit

```
list_brands -> list_scans -> get_scan -> get_share_of_voice
            -> list_findings -> list_competitors -> list_cited_sources
            -> (Growth/Scale) get_finding_evidence -> report
```

`get_latest_snapshot` can replace the `list_scans` and `get_scan` steps when the user wants a quick read, then go on from `get_share_of_voice`.

## Core tools

### list_brands
When: first call, always. Params: `limit`, `offset`.
Read: brand id and name. More than one brand means ask the user which. Never guess from the name in the user's message if two are close.

### get_brand
When: the user asks about aliases, markets or who is tracked, or answers name the brand oddly.
Read: confirmed and proposed aliases, competitors, markets. A wrong proposed alias can explain a low count. Report it, do not try to edit anything.

### list_scans
When: right after the brand is chosen. Params: `brandId`, `status` (queued, running, completed, partial, aborted_budget, failed), `limit`, `offset`. Newest first.
Read: id, date, status. Take the newest `completed`. Mention a newer `running` or `queued` scan in one line, since results are about to change. For a comparison, take the two newest completed scans.

### get_scan
When: after choosing the scan. Params: `scanId`.
Read: status, engines, cost, cell coverage. Coverage gives M, the total answers. If coverage is below what engines times questions would give, say how many cells are missing. Never fill the gap.

### get_latest_snapshot
Params: `brandId`, optional `marketId`.
Read: the latest completed or partial scan with share of voice, top findings, top cited sources and up to two example answers. Use for a fast cross-check and for example answer text on plans without `get_finding_evidence`.

### get_share_of_voice
Params: `scanId` (required).
Read: each entity with a weighted and a raw figure plus coverage and confidence. Use the raw count, "appeared in N of M", because anyone can verify it by hand. Quote confidence notes if present. Do not call the weighted number a share in the report.

### get_total_share_of_voice
Params: `brandId`.
Read: both buyer surfaces, AI answers and search results. The blended total is null when only one surface has a publishable figure, and then the single surface is returned labelled. Never present the blend alone. If you mention it, give both components as the tool labels them. This audit is about AI answers, so this call is optional.

### list_findings
Params: `scanId` or `brandId` (latest scan), `type` (`competitor_absent`, `source_gap`, `misdescription`), `limit` (max 200), `offset`. Most severe first.
Read: type, severity, the entity or page involved. Page through when the first page is full. An empty list for a scan where `get_share_of_voice` shows many misses is suspicious: say so.

### list_competitors
Params: `brandId`, `activeOnly`.
Read: tracked rivals, manual or detected, active or not. Match against `get_share_of_voice` names exactly. Do not merge two similar names.

### list_cited_sources
Params: `scanId` or `brandId`, `limit`, `offset`. Ranked by frequency.
Read: URLs and domains, counts, and unresolved grounding redirects counted separately. Report the redirect count as its own line. Page type is your reading of the URL and title, say "looks like a listicle" when unsure.

### list_prompts
Params: `brandId`, `promptSetId` (defaults to the active set).
Read: the exact questions tracked, their intent, library or custom. Use it when the user asks "what did you ask the AI". Quote questions verbatim.

## Plan gated (Growth and Scale only)

### get_finding_evidence
Params: `findingId`.
Read: the evidence stored with the finding plus answer text, mentions and citations from every cell it cites. Quote one short fragment of a real answer per finding type. On Local and Starter you get a plan error. Say so in one line, continue.

### get_raw_response
Params: `cellId`.
LARGE. The unprocessed provider envelope for one cell, and a single response can run to tens of thousands of tokens. Call only when a projected field truly lacks what you need, for one cell, and say why before calling. Never loop.

## Comparison

### compare_scans
Params: `scanIdA`, `scanIdB`.
Read: first whether the scans are comparable (same prompt set version, market, engine mix), then per-entity movement and findings unique to each side. If not comparable, say that before any movement. See `compare.md`.

## SEO layer (optional, only if the user asks about search rankings)

- `get_seo_capabilities` (`brandId`): which of five capabilities the plan carries, caps, last run, month cost. Call this first.
- `list_seo_snapshots` (`brandId`, `kind`, `limit`): history of stored cycles, receipts and row counts only.
- `get_seo_snapshot` (`brandId`, `kind`): rows for `rank_tracking`, `keywords`, `backlinks`, `site_audit` or `domain_overview`. Refuses when the plan lacks the capability. That refusal means no data was ever bought, not that the data is empty.
- `list_tracked_keywords` (`brandId`, `activeOnly`): keywords under rank tracking. Each active one costs a SERP task per cycle.

## Tools that spend or are not part of this audit

- `run_scan`, `run_seo_capability`: spend quota. Never without a plain request from the user. When asked, say it uses quota, then run exactly one.
- `run_free_report`: the public free report. Not part of this audit.
