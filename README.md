<div align="center">

# Mobbin App Design Skills

**Real product references from Mobbin. Native-quality mobile implementation.**

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills.sh](https://skills.sh/b/j3h7sx/mobbin-app-design-skills)](https://skills.sh/j3h7sx/mobbin-app-design-skills)
[![Mobbin MCP](https://img.shields.io/badge/reference_source-Mobbin-5B4DFF.svg)](https://mobbin.com/mcp)
[![Unofficial fork](https://img.shields.io/badge/status-unofficial_fork-555.svg)](https://github.com/Appllama/appllama-skills)

[Skills.sh](https://skills.sh/j3h7sx/mobbin-app-design-skills) · [Mobbin](https://mobbin.com) · [Mobbin MCP](https://mobbin.com/mcp) · [Upstream skills](https://github.com/Appllama/appllama-skills)

</div>

This is an unofficial fork of
[`Appllama/appllama-skills`](https://github.com/Appllama/appllama-skills)
for people who already have a Mobbin subscription.

The fork keeps the upstream research-first build method. Mobbin supplies the
screen and flow references through its official MCP server. The app-design
skill then guides implementation, motion, accessibility, performance, and
simulator review.

## Skills

| Skill | Purpose |
|---|---|
| [`mobbin-usage`](skills/mobbin-usage/SKILL.md) | Search Mobbin screens and flows, inspect the returned images, record canonical links, and turn reference patterns into design decisions. |
| [`mobbin-app-design-skill`](skills/mobbin-app-design-skill/SKILL.md) | Build native-feeling Expo and React Native screens with semantic colors, native controls, deliberate motion, full states, and simulator verification. |

The skills work as a pair. `mobbin-usage` selects and studies references.
`mobbin-app-design-skill` sets the build standard.

## Requirements

Mobbin MCP access is available on Mobbin Pro, Team, and Enterprise plans.
Authorization uses the Mobbin account that owns the subscription.

## Install

Run this command from your project root:

```bash
npx skills@latest add j3h7sx/mobbin-app-design-skills
```

Install only the Mobbin research skill:

```bash
npx skills@latest add j3h7sx/mobbin-app-design-skills --skill mobbin-usage
```

Install only the mobile app-design skill:

```bash
npx skills@latest add j3h7sx/mobbin-app-design-skills --skill mobbin-app-design-skill
```

## Connect Mobbin to Codex

```bash
codex mcp add mobbin --url https://api.mobbin.com/mcp
codex mcp login mobbin
```

The browser authorization screen will ask you to sign in to Mobbin. Other MCP
clients can connect to the same server URL:

```text
https://api.mobbin.com/mcp
```

## What changed from upstream

- Mobbin is the reference source for screens and flows.
- Research uses Mobbin's `search_screens` and `search_flows` tools.
- Every selected reference keeps its canonical Mobbin URL.
- The playbooks use visual relevance and product fit instead of AppLlama
  revenue, download, rating, credit, board, or element-taxonomy data.
- The native build guidance and simulator loop remain based on the upstream
  MIT-licensed skill.

## Try it

> Build a symptom logging flow. Search Mobbin for comparable iOS flows first.
> Show me the references and the pattern you selected before you write UI code.

> Improve this paywall. Use Mobbin screens to diagnose its hierarchy, then run
> the completed flow in the simulator and inspect the motion.

> Study how real iOS apps ask for notification permission. Cite every Mobbin
> screen and flow used in the recommendation.

## Research output

Each research pass should leave a short, reviewable record:

```text
research/<topic>/
  references.md   # Mobbin screen and flow links with one decision note each
  patterns.md     # repeated conventions, useful differences, chosen direction
```

Temporary image URLs can expire. The Mobbin screen and flow URLs are the
durable references.

## Attribution

This project is based on
[`Appllama/appllama-skills`](https://github.com/Appllama/appllama-skills) and
uses its MIT-licensed build guidance. See [LICENSE](LICENSE).

Mobbin is a trademark of its respective owner. This community fork is not an
official Mobbin product and is not affiliated with Mobbin.
