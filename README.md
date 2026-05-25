# Computer Use Cloud — specs

The strategy, information architecture, pricing, and roadmap documents that drive everything at [computeruse.run](https://computeruse.run/). This repo is the "what" and "why"; the SDK repo is the "how" (engineering contract tied to code).

## What's in here

| File | What |
|---|---|
| [STRATEGY.md](STRATEGY.md) | Positioning, competitive landscape, the "three compatibility modes" bet, why we picked the agentic-browser-cloud lane. Sources the research that drove every pivot since 2026-05-22. |
| [IA-SPEC.md](IA-SPEC.md) | The use-case-first information architecture spec. Five user archetypes (D, A, B, C, E), the comparison table, the three compatibility modes, the pricing tiers, the FAQ. Marketing-side spec that drove the May 25 site rebuild. |
| [ROADMAP.md](ROADMAP.md) | Phased milestones M0 → GA, derived from the SDK SPEC §9. Marketing milestones merged in. |

## Sibling repos in this org

| Repo | Purpose |
|---|---|
| [computeruse-run/site](https://github.com/computeruse-run/site) | Marketing site source. Implements the IA in this repo. |
| [computeruse-run/sdk](https://github.com/computeruse-run/sdk) | Python preview package + engineering SPEC (the contract for the runtime + cloud API). |
| [computeruse-run/runtime](https://github.com/computeruse-run/runtime) | Reserved for the open-source sandbox runtime drop at M5. README points at the SDK SPEC sections that define it. |

## Why split docs across two repos

- **`sdk/SPEC.md`** — engineering contract. Lives with the code that implements it. Updates when the code surface changes.
- **`specs/*`** — strategy + IA + roadmap. Lives independently of code. Updates when positioning, pricing, or competitive landscape moves.

Both sides cross-reference. The sdk SPEC §1.1 defines the Python API; this repo's IA-SPEC defines what that API should feel like to the five user archetypes who will hold it.

## How to use this repo

- **New positioning question** ("are we still targeting agentic browsers or did we pivot?") → STRATEGY.md
- **New page on the site** ("where does the runtime docs page fit?") → IA-SPEC.md
- **Timeline question** ("when does the runtime open-source?") → ROADMAP.md
- **API question** ("what does Sandbox.claude() actually do?") → [sdk/SPEC.md](https://github.com/computeruse-run/sdk/blob/main/SPEC.md)

## Status

| Doc | Status | Last reviewed |
|---|---|---|
| STRATEGY.md | v1 (2026-05-25) | 2026-05-25 |
| IA-SPEC.md | v1 (2026-05-25) | 2026-05-25 |
| ROADMAP.md | v1 (2026-05-25) | 2026-05-25 |

All v1. Expect rapid revisions through M2.
