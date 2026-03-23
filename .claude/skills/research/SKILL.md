---
name: research
description: Research trending topics, conversations, and content opportunities for X posts. Use when the user wants content ideas, wants to know what's trending in their niche, or needs to research what to post about.
argument-hint: "[niche or topic to research]"
---

# Topic & Trend Research for X Content

Research what's being discussed, debated, and shared in a specific niche to identify high-potential content opportunities.

## Input

The user provides:
- A **niche or topic** to research (e.g., "Rust", "local LLMs", "developer tools")
- Or asks "what should I post about?"
- Or wants to understand what's trending

## Process

### Step 1 — Web Research

Search for current conversations and trends using WebSearch:

1. **Search X/Twitter directly** for the niche topic + "2026" to find recent discussions
2. **Search Reddit** (r/programming, niche subreddits) for hot topics
3. **Search Hacker News** for trending technical discussions
4. **Search for recent releases/announcements** in the niche
5. **Search for controversies or debates** (these drive highest engagement)

Use WebSearch with queries like:
- `site:x.com [niche topic] 2026`
- `[niche] trending discussion March 2026`
- `[niche] controversial opinion 2026`
- `[niche] new release announcement 2026`

**Deep-read promising results** using WebFetch to extract full content from the most relevant search results. This gives you the actual conversations, not just titles.

**If chrome is available** and you need to browse X's live feed for real-time conversations, you can navigate to X search:
- `https://x.com/search?q=[topic]&f=live` — latest posts on the topic
- Read the actual discussions, not just search snippets

### Step 2 — Identify Content Opportunities

Categorize findings into opportunity types:

**Hot Takes** — Controversial discussions where you can add a unique perspective
- Look for: debates, strong opinions, "unpopular opinion" threads
- Signal: High reply counts indicate engagement potential

**Tutorials** — Questions people are asking that you can answer
- Look for: "How do I...", Stack Overflow trending, common mistakes
- Signal: Repeat questions indicate unmet demand

**Announcements** — New releases, updates, or changes you can contextualize
- Look for: GitHub releases, product launches, API changes
- Signal: Timing matters — first-mover advantage in commentary

**Comparisons** — Tools/approaches being debated
- Look for: "X vs Y", "switching from A to B", benchmark results
- Signal: People love definitive comparisons with data

**Pain Points** — Frustrations being expressed
- Look for: "I hate when...", "why can't...", bug reports, rants
- Signal: Pain point posts have extremely low negative signal risk

**Build-in-Public** — Trends in the making/building space
- Look for: What others are sharing about their progress
- Signal: Gaps in what's being shared that you could fill

### Step 3 — Prioritize by Phoenix Score Potential

Rank opportunities by predicted engagement:
1. **Conversation potential** — Will this generate replies the author can respond to? (75–150× for author reply threads, 13–27× for replies)
2. **Bookmark potential** — Is this save-worthy reference material? (~10× weight)
3. **Dwell potential** — Will people spend time reading carefully? (high weight)
4. **Timeliness** — Is this trending NOW? (freshness bonus)
5. **Authenticity fit** — Can you write about this genuinely? (reduces negative risk)

### Step 4 — Generate Content Briefs

For the top 5 opportunities, create a brief:

```
## Opportunity: [Title]

**Why now**: [What's happening that makes this timely]
**Angle**: [Your unique perspective or value-add]
**Format**: [Post / Thread / Poll / Quote tweet]
**Hook idea**: [Draft opening line]
**Key points**: [3-5 bullets of what to cover]
**Reply trigger**: [The question or take that will drive replies]
**Risk**: [Low / Medium — any negative signal concerns]
```

### Step 5 — Output

Present:
1. **Trend summary** — What's happening in the niche right now (2-3 sentences)
2. **Top 5 content opportunities** — Ranked by predicted engagement
3. **Content briefs** — For each opportunity
4. **Suggested posting schedule** — When to publish each piece
5. **Reply farming targets** — 5-10 active discussions to engage with (builds visibility before posting)

## Tips
- The best content comes from the intersection of what's trending + what you genuinely know
- "Reply farming" (engaging in relevant conversations) for 15-30 min before posting increases your visibility to the algorithm
- Time-sensitive opportunities should be published within 24-48 hours
- Evergreen opportunities can be queued for optimal timing
