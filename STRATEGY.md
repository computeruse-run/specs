# Strategy

**Version**: 1 · **Date**: 2026-05-25 · **Owner**: TBD

## The one-line positioning

> Computer Use Cloud is the cloud browser for AI agents. Drop-in compatible with Anthropic Computer Use, Browser Use SDK, and Browserbase Session API. Per-active-second billing.

Brand: **Computer Use Cloud**. Domain: **computeruse.run**. Backup brand asset: cloudbrowser.live (parked, registered).

## Why "agentic browser cloud" and not "agentic browser"

We considered three category framings:

1. **"Agentic browser"** (consumer-facing, like Comet / Atlas / Dia / BrowserOS). Owned positionally by frontier labs and well-funded browser companies. We don't have the budget or distribution to compete head-on.
2. **"AI browser"** (generic). Wikipedia owns the definitional page. Search competition is dominated by ranked explainers (Norton, DigitalOcean, Built In).
3. **"Cloud browser for AI agents"** (infrastructure). Established players (Browserbase, Browser Use Cloud, E2B Desktop) but no one has all three of (a) per-active-second billing, (b) multi-provider SDK, (c) Apache-2.0 open-source runtime. **This is the lane.**

The May 25 Semrush data confirmed "computer use" as the highest-volume head term in the category (1,900/mo, 4,940/mo cluster) with Browserbase ranking at #5 — directly outrankable with a focused page.

## The three competitors (in order of strategic importance)

### 1. Browserbase (`browserbase.com`) — the incumbent we're priced against

- **Their position**: $300M valuation, 50M sessions in 2025, Stagehand SDK at 23k stars. Generic cloud browser for any agent.
- **Their weakness**: per-browser-hour billing — meter runs while the model is thinking. Computer Use is "wire it yourself" because the abstraction is generic browser automation.
- **Our angle**: per-active-second billing (10× cheaper on a standard agent task), Computer Use as a first-class primitive, multi-provider SDK.
- **Risk to us**: production polish, three years of docs, SOC 2 Type II today. We have to be honest about this in `/vs/browserbase.html`.

### 2. Anthropic Computer Use (self-hosted Docker reference) — the per-user pain we eliminate

- **Their position**: Anthropic ships a reference Docker container; ~45× more expensive than it looks once you add EC2 + IP + CAPTCHA + ops.
- **Their weakness**: it's a reference, not a product. Single-tenant, single-session, no concurrency, no managed proxy.
- **Our angle**: managed multi-tenant hosted version. Same Claude code, same tool schema, just the execution backend swaps.
- **Risk to us**: Anthropic ships their own hosted Computer Use within 12-18 months. Our hedge: multi-provider, per-active-second, Apache-2.0 self-host.

### 3. Browser Use Cloud (`browser-use.com` hosted) — three meters we collapse to one

- **Their position**: Browser Use SDK is the most popular open-source agent SDK (95k stars). Their hosted Cloud stacks browser-time + LLM step + per-task surcharge.
- **Their weakness**: three meters make the bill unpredictable. Long-running scrapes blow the budget.
- **Our angle**: same SDK works unchanged — only change the CDP endpoint URL. Single per-active-second meter.
- **Risk to us**: they ship their own per-second pricing as a SKU. Unlikely short-term but possible.

## The wedge: three compatibility modes

The deepest insight from the IA spec is that **AI agent code today already speaks one of three protocols**: Anthropic's Computer Use tool schema, Chrome DevTools Protocol (Browser Use, Playwright, Puppeteer, Stagehand), or Browserbase's Session API. By being drop-in compatible with all three, we're not asking developers to learn a new SDK — we're letting them swap the execution backend without rewriting their agent code.

This is why "compatibility" beats "innovation" on the homepage. The pitch is *"keep your code, change one URL, your bill drops to a tenth."*

## Five user archetypes (the IA's spine)

Detailed in [IA-SPEC.md](IA-SPEC.md). Ranked by purchasing power:

| Order | Archetype | Monthly budget | Primary pain |
|---|---|---|---|
| D | Agent product cloud backend | $500-$50,000 | Opaque pricing, infra burden |
| A | RPA / internal systems | $200-$5,000 | Ops cost of self-hosted Docker |
| B | Data collection / scraping | $100-$2,000 | 3-meter pricing variance |
| C | AI QA / UI testing | $50-$500 | Plan ceilings, overage rates |
| E | Individual / hackathon | $0-$20 | No public URL for live view |

The site leads with D (highest spend) and ends with E (largest top-of-funnel).

## What we're explicitly not doing

- Not building our own LLM (bring-your-own-key).
- Not a no-code agent builder UI.
- Not a high-level agent framework (LangChain / CrewAI / AutoGen sit on top of us).
- Not a browser extension or desktop app (Comet / Atlas / Dia territory).
- Not mobile-device automation.
- Not a scraping product per se (scrapers can use us, but we don't market to scrapers).

## Pricing summary

Free 100h/mo · Pro $20/500h · Team $200/5000h. Standard task baseline: 10 min browser + 30 LLM steps + 1 CAPTCHA = $0.01 on us (vs $0.10 Browserbase, $0.15 Browser Use Cloud, $0.20+ Anthropic reference path).

Full reconciliation: [sdk/SPEC.md §4](https://github.com/computeruse-run/sdk/blob/main/SPEC.md).

## Open strategic questions

1. **TS SDK timing.** Python ships first; TS deferred to M2. Some teams (especially the D archetype) are TS-first. Risk of losing them in the early window.
2. **Pricing anomaly.** Pro overage rate ($0.01/hour) is currently cheaper than the included rate ($0.04/hour) — this is in the spec as a flagged inconsistency. Decide before launch whether this is intentional (loyalty pricing) or a typo.
3. **First-party hosted Computer Use risk.** Anthropic and OpenAI will both ship managed Computer Use within 12-18 months. Our moat needs to be (a) multi-provider, (b) per-active-second, (c) Apache-2.0. If any of those erode, we erode.
4. **Browserbase Sessions API compatibility shim.** Claimed on the site but not yet built. Either commit to building it in M2 or remove the claim.
5. **SOC 2 path.** D-archetype customers will ask. Realistically 6-9 months of audit; need to start before public launch if we want it ready for enterprise sales.

## History of pivots (so future-us doesn't re-litigate)

- **2026-05-22**: cloudbrowser.live launched as a consumer "public AI browser session" demo (Twitch-Plays-Pokémon for AI). Mock UI, no real backend.
- **2026-05-24 (afternoon)**: Pivoted to generic developer marketing for "agentic browser" category. Realized brand-category mismatch (cloud browser ≠ agentic browser).
- **2026-05-24 (evening)**: Considered `agenticbrowser.live` rebrand. Killed by Semrush data — `agentic browser` has thin volume, `computer use` has 1,900/mo head term.
- **2026-05-25**: Locked on Computer Use Cloud at `computeruse.run`. Use-case-first IA shipped (5 cards, 3 compat modes, 5-way comparison). Org migrated from `computeruse-dev` to `computeruse-run`.

Each pivot was data-driven; we're not afraid to pivot again if the next data point demands it.
