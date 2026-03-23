---
name: strategy
description: Plan weekly or monthly X content strategy. Use when the user wants to plan their content calendar, set growth goals, build a content pipeline, or think strategically about their X presence.
argument-hint: "[niche] [goals] [timeframe]"
---

# Content Strategy Planning

Build a comprehensive X content strategy aligned with the Phoenix algorithm and the user's goals.

## Input

The user provides:
- **Niche/topic area** — what they post about
- **Current state** — follower count, typical engagement, posting frequency
- **Their X profile URL or username** — read their profile and recent posts directly
- **Goals** — growth targets, audience building, product promotion, thought leadership
- **Constraints** — time available, content resources, posting schedule limitations
- **Timeframe** — weekly plan, monthly plan, or long-term roadmap

## Process

### Step 0 — Read User's X Profile (if available)

If the user provides their X username or profile URL, read their profile to auto-assess current state instead of relying on self-reported data:

Use WebFetch to read `https://x.com/[username]` — extract bio, follower/following counts, recent post previews, and pinned post.

For **deeper analysis** (engagement metrics on recent posts, analytics data), suggest running `/analyze recent` which uses chrome for authenticated access.

This replaces the need for the user to manually report their follower count, posting frequency, and engagement levels.

### Step 1 — Assess Current State

Understand where the user is:

**Account Stage:**
| Stage | Followers | Strategy Focus |
|-------|-----------|---------------|
| Launch | 0-100 | Reply farming, community building, 1 quality post/day |
| Growth | 100-1K | Content consistency, thread expertise, niche authority |
| Scale | 1K-10K | Content pillars, collaborations, repurposing pipeline |
| Authority | 10K+ | Thought leadership, selective posting, community building |

**Content Audit:**
- What formats have they tried?
- What's worked best? (ask for data or review)
- What's their authentic voice/personality?
- What unique knowledge or experience do they have?

### Step 2 — Define Content Pillars

Every account needs 3-5 content pillars — recurring themes the audience expects:

```
Pillar 1: [Primary expertise — what you know best]
Pillar 2: [Practical value — tips, tutorials, how-tos]
Pillar 3: [Perspective — opinions, takes, industry commentary]
Pillar 4: [Personal/Build-in-public — behind the scenes, journey]
Pillar 5: [Community — responses, curations, collaborations]
```

The mix should be approximately:
- 40% expertise + practical value (builds authority)
- 30% perspective (drives engagement)
- 20% personal/build-in-public (builds connection)
- 10% community engagement posts (builds network)

### Step 3 — Build the Calendar

**Weekly Template:**

```
MONDAY — [Pillar: Perspective]
  Post: Observation or hot take about the niche
  Time: 9-10 AM ET
  Reply goal: Engage with 10+ posts in niche before posting

TUESDAY — [Pillar: Expertise]
  Thread: Deep dive or tutorial
  Time: 8-9 AM ET
  Reply goal: Respond to all comments within 1 hour

WEDNESDAY — [Pillar: Practical Value] ← Peak day
  Post: Quick tip, code snippet, or actionable insight
  Time: 9 AM ET
  Reply goal: Maximum engagement — clear schedule for 1 hour post-publish

THURSDAY — [Pillar: Community]
  Quote tweet or collaboration with another account
  OR Poll related to niche topic
  Time: 10-11 AM ET

FRIDAY — [Pillar: Build-in-Public]
  Post: Weekly progress update, lesson learned, or behind-the-scenes
  Time: 10 AM ET (lighter engagement expected — that's OK)
```

**Daily Non-Negotiables (20-30 min):**
- Reply to all comments on your posts (75-150× multiplier)
- Engage with 10-15 posts from accounts in your niche
- No self-promotional replies — add genuine value

### Step 4 — Growth Tactics by Stage

**Launch (0-100 followers):**
- Reply to 20-30 posts daily in target niche (visibility building)
- One quality post per day (compound effect over 30 days)
- Find 10 accounts in your niche at similar size — engage consistently
- Don't worry about analytics yet — focus on content quality and consistency

**Growth (100-1K):**
- 3-5 posts per week with at least 1 thread
- Start tracking which formats perform best
- Reply farming before every post (15-30 min)
- Repost/quote tweet others' content with added insight
- Start building email list or external presence to bootstrap engagement

**Scale (1K-10K):**
- Establish a consistent posting rhythm your audience expects
- Repurpose top content (use /repurpose skill)
- Collaborate: quote tweet, co-threads, or shout-outs with similar-sized accounts
- Start an evergreen queue for your best content (OpenTweet)
- Analyze weekly: what's working, what's not (use /review skill)

**Authority (10K+):**
- Quality > quantity — selective posting with high impact
- Launch content series (recurring threads on a specific day)
- Build community through conversations, not broadcasts
- Mentor smaller accounts (creates loyalty and network effects)

### Step 5 — Set Measurable Goals

Define 30-day targets:

| Metric | Current | Target | Strategy |
|--------|---------|--------|----------|
| Followers | ? | ? | [specific growth tactics] |
| Avg impressions/post | ? | ? | [content quality improvements] |
| Avg replies/post | ? | ? | [CTA optimization] |
| Engagement rate | ? | ? | [format and timing optimization] |
| Posts per week | ? | ? | [consistency target] |

### Step 6 — Output

Present:
1. **Account assessment** — Current stage and key observations
2. **Content pillars** — 3-5 defined themes with examples
3. **Weekly calendar** — Specific posting plan with times
4. **Growth tactics** — Stage-appropriate strategies
5. **30-day goals** — Measurable targets
6. **First week action items** — 5-7 specific things to do this week
7. **Content ideas** — 10 specific post ideas across the pillars

## Rules
- Strategy must be sustainable — don't plan more than the user can maintain
- Quality always trumps quantity
- Consistency matters more than perfection
- Adjust strategy based on data — review weekly with /review skill
- The algorithm rewards authentic expertise — don't fake authority in areas you don't know
