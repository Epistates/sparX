---
name: hooks
description: Generate scroll-stopping opening lines for X posts. Use when the user needs hook ideas, opening lines, first lines, or attention-grabbing openers for tweets.
argument-hint: "[topic or context for the hook]"
---

# Generate Scroll-Stopping Hooks

The first 8-12 words of an X post determine whether anyone reads the rest. Generate multiple high-impact hook options optimized for the Phoenix algorithm's dwell time signal.

## Input

The user provides:
- A **topic** they're posting about
- A **rough idea** of the post content
- An **existing hook** they want alternatives for
- A **URL** — read the content via WebFetch to understand the subject, then generate hooks based on the actual material (see [../../../reference/url-reading.md](../../../reference/url-reading.md))

## Process

### Step 1 — Understand the Content
What is the core message? Who is the audience? What emotion should the hook trigger?

### Step 2 — Read Hook Patterns
Read [patterns.md](patterns.md) for the full hook pattern library.

### Step 3 — Generate 7-10 Hooks

Generate hooks across multiple pattern categories:

1. **Curiosity Gap** — Creates an information gap the reader must fill
2. **Specific Number** — Leads with a concrete, impressive metric
3. **Contrarian** — Challenges conventional wisdom
4. **Pain Point** — Names a frustration the audience feels
5. **Before/After** — Shows transformation in minimal words
6. **Social Proof** — Leads with credibility markers
7. **Question** — Poses something the reader can't ignore

For each hook:
- Keep to 8-12 words (the visible preview before truncation)
- Test: Would this stop YOUR scroll?
- Ensure it's honest — don't promise what the post doesn't deliver

### Step 4 — Rank and Annotate

Rank all hooks by predicted effectiveness and annotate:
- **Best for dwell** — which hook will make people read the full post?
- **Best for replies** — which hook triggers an urge to respond?
- **Best for bookmarks** — which hook signals "save-worthy" content?
- **Safest** — which hook has lowest negative signal risk?
- **Boldest** — which hook has highest ceiling but more risk?

### Step 5 — Output

Present all hooks in a scored table, ranked by Phoenix Score. The score represents what a full post would score with that hook (assuming a solid body + CTA):

```
#  Hook                                                Score   Best for
1. "2.3× faster than MLX — on a MacBook."              8.4/10  Dwell + bookmarks
2. "Your MacBook can fine-tune a 7B model in 12 min."  8.1/10  Specificity + curiosity
3. "Why I rewrote LLM inference in pure Rust."          7.9/10  Curiosity gap
4. "Most devs are overpaying for GPU cloud. Here's why." 7.6/10  Pain point + broad reach
5. "The local AI tipping point just arrived."           7.2/10  Boldest (high ceiling, more risk)
...
```

Also include:
1. Annotations per hook (best for dwell / replies / bookmarks / safest / boldest)
2. Recommended top pick with rationale
3. The complete first 2 lines (hook + bridge to body) for the top 3

## Rules
- Never use engagement bait ("You won't believe...")
- No clickbait that the content doesn't deliver on
- Avoid jargon in the hook unless the audience is entirely specialists
- Specificity always beats vagueness ("2.3× faster" > "much faster")
- The hook must be true
