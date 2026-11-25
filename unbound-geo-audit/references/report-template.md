# Report template

Use this layout exactly, in this order. Skip no section: if one has nothing, say which call returned nothing and why that matters. Short sentences. A founder should read it in four minutes.

## Header and headline

```
# AI visibility audit: <Brand>

<Brand> was named in N of M answers across <engines> on <scan date>.
Scan <short id> | <completed or partial> | <K> questions | <S> samples per engine
```

N comes from the raw count in `get_share_of_voice`. M comes from `get_scan` coverage. If the scan is partial, add a line: "Partial scan, X of Y cells returned."

## Who was named instead

```
| Brand | Named in | Tracked rival |
|---|---|---|
| <Brand A> | N of M | yes or no |
| (five rows by raw count) | | |
| <Your brand> (you) | N of M | n/a |
```

If the user's brand is not among the five, add it as a sixth row. After the table, one sentence: "<Rival> was named in N of M answers where <Brand> was left out." Include it only if that count is in a tool result. No words like share, rank, leader or number one.

## Pages the answers cited

```
| Page | Type | Cited | Mentions <Brand> |
|---|---|---|---|
| <url> | listicle, review platform, directory, forum thread, video, news, own site | N times | yes or no |
```

Top five by count. Then, if there are any: "R citations were unresolved redirects and are not in this table." Omit the line when R is zero.

## What the answers got wrong or left out

Group findings by type. For each group give the number of findings and the two most severe, one line each.

- Missing (`competitor_absent`): ...
- Cited pages that skip you (`source_gap`): ...
- Described wrong (`misdescription`): ...

On Growth and Scale, add one real answer fragment under each group, in quotes, with the engine name. On Local and Starter, add: "Answer text is not available on your plan, so this section uses the finding summaries."

## Do these three first

For each of three fixes:

```
1. <Verb phrase naming the page or fact>
   Why: <the finding or cited page, with its count>
   How: <literal steps from fixes.md: which page, who to email, what to write>
   Effort: <minutes, hours, or a week waiting on a third party>
   Check: <the exact question to look at in the next scan>
```

Order by how many answers the fix touches. No fourth fix. No "improve content".

## Rescan

Rescan on <date 30 days out> with the same questions and engines, so the two scans are comparable. One scan does not prove a fix worked. Two or three in a row pointing the same way will.

## Notes

- Plan limits hit: <list or none>
- Calls that returned empty or failed: <list or none>
- Not read: <anything you skipped, for example SEO data>

If the user wants it done for them, close with: "Unbound GEO does it for you under one of our managed plans."

## Style

- US English. No em or en dashes. Use a period where a colon would do.
- Every number traces to a tool call in this session. If you cannot say which, delete it.
- Do not hedge every line. State what the data says, then say once what it cannot show.
