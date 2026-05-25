# Information Architecture Spec

**Version**: 1 · **Date**: 2026-05-25 · **Drives**: [computeruse-run/site](https://github.com/computeruse-run/site)

The information architecture for [computeruse.run](https://computeruse.run/). Not feature-first. Not parameter-table-first. **Use-case-first.** Pick the user, show them what's painful today, show them what changes.

## The five user archetypes

Every real user maps to one of these five. Their search keywords, current tools, and willingness to pay are all different. The IA leads with archetype identification, not feature comparison.

| Order | Letter | Archetype | Typical user | Typical task | Monthly budget |
|---|---|---|---|---|---|
| 1 | **D** | Agent product cloud backend | AI app founders, SaaS PMs | Embed "let AI do this for you" in their product | $500-$50,000 |
| 2 | **A** | AI Agent for RPA / internal systems | Enterprise IT, AI consultants | Claude fills HR system, SAP, insurance claims | $200-$5,000 |
| 3 | **B** | Data collection / web scraping | Data teams, growth hackers, AI pipeline ops | Pull e-commerce prices, listings, SaaS public data | $100-$2,000 |
| 4 | **C** | AI QA / UI test automation | QA engineers, SaaS founding teams | Agent runs regression suite like a human | $50-$500 |
| 5 | **E** | Individual dev / hackathon / side project | Indie devs, students, researchers | Demos, blog posts, weekend hackathons | $0-$20 |

Ranking rationale: D first because highest LTV; E last but largest top-of-funnel; A/B/C in the middle as bread-and-butter monthly subscribers.

## Homepage structure (6 sections)

### Section 1 — Hero

**What to convey**: one sentence positioning that names the three compatibility surfaces (Anthropic Computer Use, Browser Use SDK, Browserbase Session API). Subtitle promises "don't swap your framework, don't learn a new API, just point the browser at us — your bill drops to about a tenth."

**CTAs**: two — "Find your use case" (scrolls to §2), "See pricing" (scrolls to §5).

**Trust anchors**: compatibility row naming the protocols and SDKs we speak (Anthropic Claude, Browser Use, Playwright, CDP, Browserbase Sessions, OpenAI Operator). No logos required — text-only avoids legal questions and feels confident.

### Section 2 — Use case selector (the IA's spine)

Five full-width horizontal cards, ordered D → A → B → C → E. Each card has three columns:

| Column | Content |
|---|---|
| Left (title + pain) | Archetype letter + label · what they're doing · "today you use X" line · 3 pain bullets (each prefixed with `!`) |
| Middle (what they get) | "What you get" header · 4 benefit bullets (each prefixed with `✓`) |
| Right (bill + CTA) | "Typical monthly bill" with `before → after` numbers · CTA button to the matching `/vs/` page |

Card D (product backend) is visually flagged with an accent-colored letter chip; the other four use a neutral chip. This signals D is the lead persona without changing the order's logic.

### Section 3 — Three compatibility modes

Three horizontal blocks. Each shows an info-flow diagram (two boxes + an arrow), not code. The pitch: "whatever your agent already speaks, we already listen."

| Mode | Diagram | Pitch |
|---|---|---|
| 01 — Claude Computer Use | `Anthropic Claude API ↔ Cloud Chromium sandbox` | Anthropic tool schema unchanged; execution backend swaps from local Docker → us |
| 02 — Browser Use / Playwright / CDP | `Any CDP client ↔ CDP gateway` | Any Chrome DevTools Protocol client works; just change the WebSocket URL |
| 03 — Browserbase Session API | `bb.sessions.create() ↔ Compatible Session API` | Swap one base URL; session lifecycle, recording, live view all behave the same |

Code samples deferred to the SDK README, not on the homepage. The homepage shows flow, not syntax.

### Section 4 — Comparison table (10 rows × 6 columns)

The columns: `What I want to do` | `Self-built Playwright` | `Anthropic API` | `Browser Use Cloud` | `Browserbase` | `computeruse.run`.

The rows cover the things developers actually try to do:

1. Run Claude Computer Use agent
2. Run Browser Use agent
3. Run plain Playwright script
4. Run OpenAI Operator
5. Handle CAPTCHA
6. Residential IP rotation
7. 24/7 with 100+ concurrent sandboxes
8. Data never leaves your VPC (self-host)
9. Open-source runtime
10. **Cost per standard agent task** (the punchline row)

Standard agent task = **10 minutes browser uptime · 30 LLM decision steps · 1 CAPTCHA solve · ~35% agent active**. The same baseline is used in every cost claim across the site (and in `sdk/SPEC.md §4` and every `/vs/*.html` page).

Final-row costs: `$0.05` (self-built, excl. ops) · `$0.20+` (Anthropic reference) · `$0.15` (Browser Use Cloud) · `$0.10` (Browserbase) · **`$0.01` (us)**.

### Section 5 — Pricing (3 tiers)

Three cards. Pro is highlighted (most popular).

| Tier | Price | Included active hours | Targets |
|---|---|---|---|
| Free | $0 / mo | 100 | E (individual, hackathon) |
| Pro | $20 / mo | 500 (+ $0.01/extra hr) | A, B, C (RPA, scraping, QA) |
| Team | $200 / mo | 5,000 (custom overage) | D (product backend) |

Each tier card states which use-case letters it targets — closes the loop with §2.

### Section 6 — FAQ (8 questions, AEO-tuned)

The questions are calibrated to win Google AI Overview / Perplexity / ChatGPT Search citations. Each answer is 40-80 words, definitional opener first.

1. What's the relationship between Computer Use Cloud and Anthropic Computer Use?
2. I use Browser Use SDK — how much code do I have to change?
3. Where exactly are you cheaper than Browserbase?
4. Is my data secure? Can I self-host?
5. How are CAPTCHA, residential IP, and concurrency limits handled?
6. What LLMs are supported? Is it Claude-only?
7. Can I replay a failed run? Is there session recording?
8. What's in the free tier? Credit card required?

Mirror the same FAQ in JSON-LD `FAQPage` schema so AI search engines lift them verbatim.

## /vs/ subpage template (7 sections)

All three comparison pages (`/vs/anthropic-computer-use.html`, `/vs/browser-use.html`, `/vs/browserbase.html`) share the same shape:

1. **Hero** — one-line summary positioning ("Anthropic gives you the brain, we give you the body" / "Keep the SDK, collapse three meters into one" / "Honest pricing, feature, and migration comparison").
2. **TL;DR** — 4-5 bullets covering the key claim, the honest caveat, the migration cost.
3. **Who shouldn't switch** — explicit list of cases where the competitor is the right pick. Trust earned through honesty.
4. **Who should switch** — flip side: 4-5 scenarios that make the swap a win.
5. **Three real scenarios** — concrete personas + workloads, each with three paragraphs: "today (their approach), pain, after switching."
6. **Migration** — text explanation (not code). Code lives in the SDK repo. One- to four-paragraph narrative.
7. **Pricing comparison** — same standard task baseline ($0.01 vs $X), with line-item breakdown.
8. **FAQ** — 5 questions specific to that competitor, mirrored in JSON-LD.
9. **CTA** — back to homepage or signup.

(Listed as "7 sections" colloquially; counting headers it's 9.)

## Cost claim discipline

Every cost number across the site references the **same standard task baseline**. If we ever change the baseline, every page changes in lockstep. This is non-negotiable — inconsistent pricing math is the fastest credibility kill on a comparison page.

Numbers:
- Self-built Playwright: ~$0.05 per task (excludes engineering ops)
- Anthropic reference path: ~$0.20 per task
- Browser Use Cloud: ~$0.15 per task
- Browserbase: ~$0.10 per task
- **Computer Use Cloud**: ~$0.01 per task

Source of truth: `sdk/SPEC.md §4.4`. Any new "X cheaper than Y" claim has to derive from that math.

## What we deliberately did NOT do on the homepage

- **No code on the homepage.** Code blocks live in the SDK README and the `/vs/` migration sections. Homepage shows information flow, not syntax.
- **No "Trusted by" logo strip near the H1.** Per minimalist-hero research, logo strips above the fold are the most-copied Stripe-2021 layout and now read as template.
- **No feature grid.** The use-case selector replaces it. Features are surfaced inside use-case cards where they're tied to a specific user's pain.
- **No carousel.** Carousels are user-hostile; the use-case cards are stacked vertically.
- **No comparison without a use case attached.** Every comparison data point appears next to the use case it serves.

## SEO / AEO targets the IA optimizes for

| Query | Target page | Notes |
|---|---|---|
| "computer use" (1,900/mo, KD high) | `/` | Battle the head term via authority + entity coverage |
| "computer use api" | `/` | Listed in compatibility row + FAQ |
| "claude computer use docs" (140/mo, KD 32) | future `/docs/quickstart` | Not yet built |
| "computer use claude" (110/mo, KD 27) | `/` | Listed in compatibility row + Card A |
| "browser use cloud alternative" | `/vs/browser-use.html` | Direct match |
| "browser use pricing" | `/vs/browser-use.html` | Direct match |
| "browserbase pricing" (140/mo, KD 17) | `/vs/browserbase.html` | Direct match |
| "browserbase alternative" | `/vs/browserbase.html` | Direct match |
| "anthropic computer use self host" | `/vs/anthropic-computer-use.html` | Direct match |
| "what is computer use" (90/mo, KD 35) | `/` (FAQ + JSON-LD) | AEO definition page |

## When to revise this spec

- A new competitor enters the category that's substantively different (not just a clone) → add a `/vs/` page + update §4 comparison table.
- A pricing tier changes → update §5 + every cost-per-task claim downstream.
- A new compatibility mode ships (e.g., LangChain agent API direct support) → add a fourth mode block to §3.
- An archetype's pain landscape changes (e.g., Anthropic ships native hosted Computer Use) → revise the corresponding use-case card text.

Otherwise, the spec is stable. Refactor the implementation; keep the spec.
