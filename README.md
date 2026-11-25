# unbound-geo-audit

An agent skill that audits how your brand shows up in AI answers (ChatGPT, Gemini, Perplexity, Claude, Google AI Mode, AI Overviews) from your latest Unbound GEO scan, over MCP.
Read only. You get named-in counts, who the engines named instead, the pages they cited, and three fixes with the literal how.

## What you get

An excerpt from the report. The brand is fictional, see the [full example](examples/example-audit.md).

```
# AI visibility audit: Lumen Ledger

Lumen Ledger was named in 31 of 120 answers across ChatGPT, Gemini, Perplexity,
Claude, Google AI Mode and Google AI Overviews on Nov 17, 2026.

| Brand            | Named in   | Tracked rival |
|------------------|------------|---------------|
| Tallybird        | 78 of 120  | yes           |
| Penwise          | 64 of 120  | yes           |
| Ormond Books     | 47 of 120  | yes           |
| Lumen Ledger     | 31 of 120  | n/a           |
| Kestrel Accounts | 22 of 120  | no            |

1. Pitch the author of the most cited listicle
   Why: bestfreelancetools.example/bookkeeping-apps-2026 was cited 24 times
        and does not name Lumen Ledger.
   How: Email the byline author. Two lines on what you do, one verifiable
        differentiator, a free account, the pricing page.
   Check: that page lists you in the next scan.
```

Every number is a count with its total. No percentages without a count, no rankings, no promises.

## Requirements

- An Unbound GEO paid plan (Local, Starter, Growth or Scale) with at least one scan run. No scan yet? Run the free scan at [unboundgeo.com](https://unboundgeo.com).
- Claude, ChatGPT, Claude Code, or any agent that speaks MCP over HTTP.
- Growth or Scale if you want real answer text and finding evidence. Local and Starter get the same audit from finding summaries, and the skill says so.

## Connect

Server: `https://unboundgeo.com/api/mcp`

**Claude.** Customize, then Connectors, Add custom connector. Name it unbound geo, paste the server address, sign in with your Unbound GEO account.

**ChatGPT.** Plugins, the plus sign, Add custom MCP server. Server URL as above, authentication OAuth. Accept the third party warning, Create as a plugin, install, sign in.

**Claude Code.**

```bash
claude mcp add --transport http unbound-geo https://unboundgeo.com/api/mcp
```

Then run `/mcp` and sign in.

**Header key, for agents that cannot do OAuth.** Create a key at [unboundgeo.com/app/mcp](https://unboundgeo.com/app/mcp). Keys start with `ubg_`. Treat them like passwords: put them in the client's MCP config, never in chat.

## Install the skill

**Claude Code.** Copy the folder into your skills directory.

```bash
git clone https://github.com/danielforeroj/unbound-geo-audit.git
cp -r unbound-geo-audit/unbound-geo-audit ~/.claude/skills/
```

You should end up with `~/.claude/skills/unbound-geo-audit/SKILL.md` and its `references/` folder.

**Claude.ai.** Zip the `unbound-geo-audit` folder (the folder itself, with `SKILL.md` and `references/` inside) and upload it under Settings, Skills.

**Anything else.** Paste `unbound-geo-audit/SKILL.md` into the project or system instructions. Paste the files in `references/` too, or tell the agent to read them if it can open files.

## First message to paste

```
Use the unbound-geo-audit skill. You are connected to my Unbound GEO account over MCP. Start with list_brands, then find my latest completed scan and audit it. Give me the report in the skill's format. Do not run a new scan unless I ask.
```

Other prompts that trigger it: "how does my brand show up in ChatGPT", "who does AI recommend instead of us", "what pages do AI answers cite", "compare my last two scans".

## What is in the repo

| file | what it is |
|---|---|
| `unbound-geo-audit/SKILL.md` | the skill: rules, steps, never list |
| `references/tools.md` | each read tool, when to call it, what to read from it |
| `references/report-template.md` | the exact report layout |
| `references/fixes.md` | turn a finding or cited page into a fix, by page type |
| `references/compare.md` | month over month, and why one run proves nothing |
| `references/troubleshooting.md` | plan errors, empty results, wrong brand, auth |
| `examples/example-audit.md` | a full fictional report |

## What it will never do

- Run a scan or an SEO capability without you asking in plain words. Those spend quota.
- Call a percentage without its count, describe visibility as a share or a rank, or promise a ranking.
- Invent a brand, a count or a page. An empty result is reported as a failed read, not as good news.
- Write to your account. Every tool it uses is read only.
- Repeat your API key or ask you to paste one into chat.
- Say "improve your content". Every fix names the page, the person, the words and the check.

Single scans are noisy. In our own test, two identical runs minutes apart agreed on about a third of the brands. The skill treats one run as a baseline, not a verdict.

## Want it done for you

Unbound GEO does it for you under one of our managed plans. See [unboundgeo.com](https://unboundgeo.com).

## Related skills

- [unbound-geo-content](https://github.com/danielforeroj/unbound-geo-content) turns one real report into a short video script, carousel or caption, and refuses to invent a number.
- [unbound-seo-geo](https://github.com/danielforeroj/unbound-seo-geo) is the full program: audit, plan, produce and measure.

## License

MIT. See [LICENSE](LICENSE).

---

Built by Unbound GEO. [unboundgeo.com](https://unboundgeo.com). Get named. Then PROVE it.
