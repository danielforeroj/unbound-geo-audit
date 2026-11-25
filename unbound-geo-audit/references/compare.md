# Comparing scans

Use when the user asks "compare my last two scans", "did it work", or "what changed since last month".

## Steps

1. `list_scans` for the brand with `status` completed. Take the two newest. If only one exists, say so and stop. Never compare scans from different brands or markets.
2. `compare_scans` with `scanIdA` the older and `scanIdB` the newer.
3. Read comparability first: same prompt set version, same market, same engine mix. If any differ, say which, and say the movement below is a rough guide only. If prompt set versions differ, the questions changed and the counts measure different things.
4. Read the per-entity movement and the findings unique to each side.
5. Pull counts from each scan with `get_share_of_voice` so every change reads "named in N of M before, N of M now". M can differ between scans. Show both.

## How to read a change honestly

Single runs prove nothing. In Unbound's own test, two identical runs minutes apart agreed on only about a third of the brands. That is the noise floor. A brand moving from 31 to 36 named answers out of 120 sits inside it.

- Treat a change as a signal when it points the same way across two or more consecutive scans, or when a specific fix has a specific finding that disappeared.
- A finding that shows up in one scan and is gone in the next, with no fix in between, is noise.
- A finding that disappears after you fixed its page, and stays gone for a second scan, is a real result.
- A rival jumping in count is a prompt to read its cited pages, not a reason to copy it.
- An engine added or failed moves the totals. Compare per engine if the tool gives it. Otherwise say you cannot.
- A partial scan is not a clean comparison with a completed one.

## Wording

Say: "Lumen was named in 31 of 120 answers on Oct 17 and in 36 of 120 on Nov 17. That is inside the run to run noise we see, so it does not show a change yet."

Not: "Visibility is up 16 percent." Not: "You moved up."

When the movement is large: "This is larger than the noise we expect. Confirm it with the next scan before you tell anyone it worked."

## Report layout for a comparison

```
# Scan comparison: <Brand>

<older date> to <newer date> | comparable: yes or no, because <reason>

## Named in
| Brand | Before | Now |
|---|---|---|
(top five plus the user's brand, counts as N of M)

## Findings
Gone since the older scan: ...
New in the newer scan: ...
Unchanged: <count>

## What this does and does not show
<two or three sentences using the rules above>

## Next
Rescan on <date> with the same questions.
```

Attribute nothing to a fix unless the user told you the fix and its date. Do not guess what caused a change.
