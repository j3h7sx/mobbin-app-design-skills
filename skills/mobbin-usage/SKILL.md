---
name: mobbin-usage
description: Use Mobbin's official MCP to research real iOS and web screens and flows before designing or implementing product UI. Load when Mobbin tools are available and the task involves screen references, flow research, onboarding, paywalls, feature design, or improving an existing interface.
license: MIT
metadata:
  author: solodevmaxxing
  upstream: Appllama/appllama-skills
  version: 1.0.0
---

# Mobbin Usage

Mobbin supplies real product screens and ordered flows through its official
MCP server. Use those images as design evidence. Extract patterns from several
relevant products, then apply the useful pattern to the user's product.

Pair this skill with **mobbin-app-design-skill** during design and
implementation. This skill controls reference research. The app-design skill
controls the build and simulator standard.

## Connection

The official MCP endpoint is:

```text
https://api.mobbin.com/mcp
```

Mobbin MCP requires a Pro, Team, or Enterprise subscription and OAuth
authorization. In Codex CLI, connect with:

```bash
codex mcp add mobbin --url https://api.mobbin.com/mcp
codex mcp login mobbin
```

If Mobbin tools are unavailable, state that the reference pass is pending.
Give the connection command. Continue without reference research only when the
user asks for that path.

## Research contract

1. Start with a named design question. Examples include where a primary action
   sits, how a symptom scale reads, or when a flow asks for permission.
2. Search for one screen or one journey per query. Describe visible elements
   and their relationship. Set the platform through the tool parameter.
3. Inspect the returned images. Metadata alone cannot support a visual claim.
4. Keep the canonical `mobbin_url` for every screen or flow used in the
   analysis. Cite those URLs when presenting the result.
5. Compare references across products. Separate repeated conventions from one
   product's visual taste.
6. Stop when additional results stop changing the decision.

## Tool map

| Tool | Use |
|---|---|
| `search_screens` | Find individual iOS or web screens with natural-language queries. Use `standard` for a quick broad pass. Use `deep` for a detailed intent. Carry selected screen IDs into `exclude_screen_ids` during follow-up searches. |
| `search_flows` | Find ordered iOS or web journeys such as onboarding, checkout, permission prompts, logging, or paywall flows. Start with `limit=1`, inspect that flow, and expand when comparison is useful. Paginate with `page` when needed. |
| `search_sections` | Find web sections such as pricing tables, headers, and footers. Use this tool for web work. |

Tool names may include a host prefix such as `mcp__mobbin__`.

## Query rules

- Describe one visible screen structure or one user journey.
- Put `ios` or `web` in the platform parameter.
- Name a specific app in the query when the task requires that app.
- Prefer concrete relationships such as "severity choices above a fixed save
  action" over broad style words.
- Run separate queries for separate intents.
- Inspect each image that supports the conclusion.

For screen searches, `standard` mode gives a low-latency result set. `deep`
mode interprets a more detailed brief and ranks candidates for relevance. A
useful research pass can use both modes, then exclude duplicates.

For flow searches, the result includes the flow name, app name, canonical
Mobbin URL, screen count, ordered screen IDs, and temporary image URLs. Inline
previews can sample the journey. The result limit controls the number of flows,
while one returned flow can still contain many screens. Inspect the steps
needed for the claim before describing the complete flow.

## Evidence handling

Mobbin screen image URLs expire after 30 days in the current MCP contract.
Record the canonical screen or flow URL with the app name and the decision it
supports. The Mobbin attribution strip is provenance outside the referenced
interface. Exclude it from visual analysis and from the UI you build.

The MCP rate limit is 60 requests per 60 seconds per user. On a `429`, follow
`Retry-After` before another request.

Use task-scoped research. Keep the user's selected references and design
question in view. Do not use this workflow to reproduce the Mobbin catalog.

## Playbooks

| Request | Read |
|---|---|
| Build a product or feature from scratch | [references/build-from-scratch.md](references/build-from-scratch.md) |
| Improve an existing screen | [references/improve-a-screen.md](references/improve-a-screen.md) |
| Study flows, components, or several products | [references/research-methods.md](references/research-methods.md) |

## Reference record

Keep a compact local record when the task benefits from durable research:

```text
research/<topic>/
  references.md   # app, screen or flow name, canonical Mobbin URL, decision
  patterns.md     # repeated structure, meaningful differences, chosen pattern
```

The record should explain why each reference matters. A list of links without
decisions is incomplete research.
