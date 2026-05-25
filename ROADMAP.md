# Roadmap

**Version**: 1 · **Date**: 2026-05-25

Phased milestones M0 → GA. Engineering scope is the same as [sdk/SPEC.md §9](https://github.com/computeruse-run/sdk/blob/main/SPEC.md); marketing + go-to-market merged in here.

## Milestone overview

| Milestone | Scope | Estimate (solo) | Status |
|---|---|---|---|
| **M0** | Site + stub SDK + spec + 4 org repos | 1 week | **shipped 2026-05-25** |
| **M1** | Local single-sandbox prototype (Claude CU on a laptop) | 2-3 weeks | not started |
| **M2** | Unify Claude+OpenAI behind `sb.agent.run()`; publish `computeruse==0.1.0` | 3-4 weeks | not started |
| **M3** | Cloud orchestration: control plane, pool warmer, CDP gateway | 4-6 weeks | not started |
| **M4** | Live view + per-active-second metering + Stripe billing | 6-8 weeks | not started |
| **M5** | Public beta + open `computeruse-run/runtime` source drop | +4 weeks | not started |
| **GA** | SOC 2 Type I in audit, p95 cold start verified live, 10 customers in prod | +6-8 weeks | not started |

**Total M1 → GA: realistically 4-6 months solo, 2-3 months with a co-founder + 1 engineer.**

## M0 — DONE (2026-05-25)

Engineering:
- [x] Stub `computeruse` Python package (PyPI-publishable, twine-check passed)
- [x] Apache-2.0 license + open-source positioning baked into copy
- [x] Engineering SPEC.md in the sdk repo (12 sections, ~1k lines, contract for everything claimed on the site)

Marketing:
- [x] computeruse.run domain registered
- [x] Homepage with use-case-first IA (5 cards D→A→B→C→E)
- [x] 3 compatibility modes section (Claude CU / Browser Use+CDP / Browserbase Session)
- [x] 10-row × 5-column comparison table with standard-task pricing
- [x] 3-tier pricing (Free / Pro / Team)
- [x] FAQ with JSON-LD AEO structure (8 Qs)
- [x] /vs/anthropic-computer-use.html
- [x] /vs/browser-use.html
- [x] /vs/browserbase.html
- [x] HN Show post draft + 6 pre-written replies + 10 backlink targets

Org infrastructure:
- [x] github.com/computeruse-run org with 4 repos: site, sdk, runtime, specs
- [x] cloudbrowser.live retained as backup brand asset
- [x] cross-references swept (computeruse-dev → computeruse-run, completed 2026-05-25)

Pending user action (still M0):
- [ ] Publish `computeruse` to PyPI (one `twine upload` command — instructions in [sdk/PUBLISHING.md](https://github.com/computeruse-run/sdk/blob/main/PUBLISHING.md))
- [ ] Wire DNS: computeruse.run → static host (Vercel/Netlify/Cloudflare Pages)
- [ ] 301 redirect cloudbrowser.live → computeruse.run
- [ ] Drop a real og.png at the site root (1200×630)
- [ ] Set up Semrush position tracking for the 10 target keywords (see [IA-SPEC.md](IA-SPEC.md))

## M1 — local single-sandbox prototype (2-3 weeks)

**Goal**: a developer on a laptop can run `python -m computeruse.dev claude "find me lisbon flights"` and watch Claude Computer Use drive a real Chromium against a real site.

Engineering:
- [ ] Docker container: Debian + pinned Chromium + Xvfb + Playwright Python
- [ ] In-container agent runner: Claude API client + screenshot capture + action dispatch
- [ ] Local CLI: `computeruse.dev claude <prompt>` (no cloud orchestration, runs against local Docker)
- [ ] Live view: noVNC at `http://localhost:8080/live` for the running session
- [ ] Real `Sandbox.claude()` class that actually instantiates a sandbox (not just PreviewError)

Non-engineering:
- [ ] First real customer conversation: pick one D-archetype team, walk through the use case, confirm IA-SPEC archetype model isn't wrong

Exit criteria:
- A Claude Computer Use task that takes ~5 minutes wall-clock runs end-to-end without manual intervention.
- The action loop matches Anthropic's reference Docker behaviorally (modulo the cloud network path being absent).

## M2 — unify Claude + OpenAI behind one API (3-4 weeks)

**Goal**: `Sandbox.claude()` and `Sandbox.openai()` both work with the same `sb.agent.run()` interface. Publish `computeruse==0.1.0` as a real package (no longer just a preview stub).

Engineering:
- [ ] Provider abstraction in `computeruse/providers/` (Anthropic + OpenAI)
- [ ] Action type normalization (Claude's `computer_20241022` ⇄ OpenAI's `computer-use-preview` differ in coordinate space and action enum)
- [ ] Unified `AgentResult` dataclass
- [ ] Provider-specific termination signal handling
- [ ] Browser Use SDK compatibility test (run the canonical Browser Use example, point it at our local CDP, verify success)
- [ ] `computeruse==0.1.0` published to PyPI (replaces the 0.0.1 stub)

Marketing:
- [ ] HN Show post (publish now that the package is real — see [hn-post.md](https://github.com/computeruse-run/site/blob/main/marketing/hn-post.md))
- [ ] Update `/vs/*.html` migration sections with the real, verified diffs (currently they're aspirational)
- [ ] Resolve the SPEC.md Appendix A inconsistencies — Pro overage rate, p95 cold start labeling, runtime repo presence

Defer: Gemini agent support to M3 (Vertex API still moving as of May 2026).

## M3 — cloud orchestration (4-6 weeks)

**Goal**: customers can create real sandboxes in our cloud via API. Pool warmer keeps cold start under 2s p95. CDP gateway routes Browser Use / Playwright / Stagehand traffic.

Engineering:
- [ ] Control plane (Fly.io or Modal, decide via M2 spike)
- [ ] Per-tenant sandbox pool warmer
- [ ] CDP gateway exposing `wss://connect.computeruse.run/{sandbox_id}?apiKey=...`
- [ ] Tenant isolation primitive (Docker for M3, gVisor by GA)
- [ ] Residential proxy integration (vendor TBD: Bright Data / IPRoyal / Oxylabs)
- [ ] CAPTCHA solver integration (vendor TBD: 2Captcha / CapSolver / AntiCaptcha)
- [ ] Synthetic cold-start probe (1/min in every region; rolling p50/p95/p99 published at `/status`)

Defer: Browserbase Sessions API shim to M4. Self-host runtime to M5.

## M4 — live view + metering + billing (6-8 weeks)

**Goal**: customers can sign up, see live agent sessions in their dashboard, get monthly invoices via Stripe.

Engineering:
- [ ] In-sandbox ffmpeg → WebRTC SFU at `live.computeruse.run/{token}`
- [ ] Embedable iframe at the customer's URL
- [ ] Per-active-second metering daemon (gRPC stream from sandbox → control plane)
- [ ] Billing aggregator (PostgreSQL or ClickHouse, rolled up to invoice rows)
- [ ] Stripe Checkout + Customer Portal integration
- [ ] Sign-up flow + email verification + API key issuance

Non-engineering:
- [ ] First 10 paid customers (beta program)
- [ ] Pricing reconciliation done (resolve the Pro overage anomaly before billing real customers)

## M5 — public beta + runtime open-source (+4 weeks after M4)

**Goal**: open `computeruse-run/runtime` (Apache-2.0). Public sign-up. Self-host path supported.

Engineering:
- [ ] Source drop into `computeruse-run/runtime` (currently a stub README)
- [ ] Self-host Docker license issuance for Team plan customers
- [ ] `@computeruse/stagehand` npm package shipped (Stagehand fork w/ COMPUTERUSE env)
- [ ] `browserbase_compat` shim package (1:1 Browserbase Sessions API surface against our cloud)

Marketing:
- [ ] Hacker Newsletter / TLDR AI pitch with HN traffic numbers
- [ ] First customer case study published
- [ ] ChangeLog podcast pitch

## GA — production-ready (+6-8 weeks after M5)

**Goal**: enterprise customers can buy this. SOC 2 Type I in audit. p95 cold start measured live and publicly disclosed.

Engineering:
- [ ] SOC 2 Type I controls in place (audit firm engaged in M4)
- [ ] gVisor sandbox isolation (upgrade from Docker for stronger boundary)
- [ ] HIPAA + BAA available on Scale tier
- [ ] TS SDK at parity with Python SDK

Non-engineering:
- [ ] At least 10 customers in production
- [ ] First $10k MRR
- [ ] First enterprise contract signed

## Things we're NOT roadmapping

(From `sdk/SPEC.md §11` non-goals; restated for clarity.)

- Building our own LLM
- A no-code agent builder UI
- High-level agent frameworks (LangChain / CrewAI / AutoGen sit on top of us, not adjacent)
- Browser extension or desktop app
- Mobile-device automation
- A scraping product (scrapers can use us, but we don't market to scrapers)
- A web crawler / search index (different category)

## Cadence

The above is a single-thread roadmap. With a co-founder or a hired engineer, M1-M3 can parallelize. The estimates assume one person doing all engineering + marketing.

## When this roadmap changes

- A milestone slips by >2 weeks → re-estimate downstream and update here
- A market signal forces a pivot (e.g., Anthropic ships their own hosted Computer Use during M2) → STRATEGY.md gets updated first, then this roadmap
- A customer commits to a feature that's currently in M3+ → consider pulling it forward; document the trade-off in this file

Reviewed: 2026-05-25 (initial draft).
