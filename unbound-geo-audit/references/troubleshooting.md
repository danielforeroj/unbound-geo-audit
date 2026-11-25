# Troubleshooting

An empty result is a failed read. Never turn it into "nothing to report".

## No tools show up, or a tool says unauthorized

- OAuth connectors (Claude, ChatGPT): the sign in expired or never finished. Ask the user to open the connector settings, reconnect and sign in to their Unbound GEO account.
- Header key: keys start with `ubg_`. A key with a stray space, a missing prefix or a revoked state fails with 401. New keys are created at https://unboundgeo.com/app/mcp. Never ask the user to paste a key into chat. Tell them to put it in the client's MCP config.
- Claude Code: check the server was added with `claude mcp add --transport http unbound-geo https://unboundgeo.com/api/mcp`, then run `/mcp` to see its state.

## Plan errors

- `get_raw_response`, `get_finding_evidence`: Growth and Scale only. Say: "Your plan does not include answer evidence, so this section uses finding summaries." Continue.
- SEO tools: `get_seo_snapshot` refuses when the plan lacks a capability. That means nothing was bought, not that the data is empty. `get_seo_capabilities` shows which capabilities exist.
- Do not retry a plan error. Do not call a different tool to get around it.

## list_brands returns nothing

The account has no brand, or the sign in belongs to another workspace. Ask the user to check they are in the right Unbound GEO account. If they have no brand, send them to unboundgeo.com for the free scan, and stop.

## No completed scan

- `list_scans` empty: no scan has run. The MCP needs a paid plan with at least one scan. Point to unboundgeo.com. Offer to run one only if the user asks, and only after saying it uses quota.
- Only `queued` or `running`: say the scan is in progress and stop. Do not report on half a scan.
- Only `partial`: report it, flagged, with how many cells returned.
- Only `failed` or `aborted_budget`: say so with the status. Suggest checking the scan in the app. Do not start another one yourself.

## Wrong brand

- Two similar brands: confirm by name and domain with `get_brand`.
- Answers describe a different company with the same name: that is a finding. Check `get_brand` aliases and say which alias looks wrong. Do not try to edit it, there are no write tools here.
- The user asks about a brand not in `list_brands`: say it is not tracked in this account. Do not substitute another brand, and never use a competitor's row as theirs.

## Findings empty but the brand is missing from many answers

Findings may not be computed yet, or the scan is partial. Say what `get_share_of_voice` shows, say findings came back empty, and say you cannot explain the misses without them. Offer `get_latest_snapshot` as a cross-check.

## Cited sources are mostly unresolved redirects

Some engines return grounding redirects that cannot be resolved to a page. The tool counts them separately. Report the count. Do not guess the target pages.

## Numbers differ between tools

The weighted and raw figures in `get_share_of_voice` differ by design. Report the raw count and say a weighted figure exists. `get_latest_snapshot` may be a different scan than the one you chose, so compare scan ids first.

## Response too long or timed out

`get_raw_response` is large. Do not retry in a loop. Ask whether the evidence from `get_finding_evidence` is enough. For other tools, lower `limit` and page with `offset`.

## Still stuck

Tell the user which call failed and the error text, minus any key. They can send that to Unbound GEO through unboundgeo.com.
