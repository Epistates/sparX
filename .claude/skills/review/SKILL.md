---
name: review
description: Analyze post-publish X performance and extract lessons. Use when the user wants to review how their posts performed, analyze engagement data, understand what worked, or improve future content based on past results.
argument-hint: "[post URL, engagement data, or analytics screenshot]"
---

# Post-Publish Performance Review

Analyze how published posts performed against Phoenix scoring predictions and extract actionable lessons for future content.

## Input

The user provides one or more of:
- **Post URL(s)** — to analyze directly
- **Engagement data** — impressions, replies, reposts, likes, bookmarks, link clicks
- **Analytics screenshot** — from X Premium analytics dashboard
- **General request** — "review my recent posts" or "what's working?"

## Process

### Step 1 — Gather Performance Data

**If the user provides a URL:**
Use WebFetch to read the post text and any publicly visible metrics. WebFetch can extract the post content, author, and basic engagement signals visible on the page.

For **full authenticated metrics** (detailed impression counts, bookmark counts, analytics dashboard data), suggest running `/analyze [url]` which uses chrome browser automation for logged-in access to richer data.

**If the user provides raw data**, use that directly.

Key metrics to capture:
- **Impressions** — total eyeballs
- **Engagement rate** — (all engagements / impressions) × 100
- **Reply count** — most important engagement metric
- **Reposts** — distribution amplifier
- **Bookmarks** — quality signal
- **Likes** — baseline (least important positive)
- **Profile visits** — discovery signal
- **Follower change** — growth impact
- **Video views / completion %** (if applicable)
- **Link clicks** (if applicable)

### Step 2 — Score Against Phoenix Hierarchy

Map actual performance to algorithm signals:

| Metric | Value | Algorithm Interpretation |
|--------|-------|------------------------|
| Author reply threads | ? | 75–150× weight — did the author create conversation threads? |
| Replies | ? | 13–27× weight — [assessment] |
| Reposts | ? | ~20× weight — [assessment] |
| Bookmarks | ? | ~10× weight — [assessment] |
| Impressions vs followers | ? | Distribution multiplier — [assessment] |
| Likes | ? | 1× baseline — [assessment] |
| Engagement rate | ? | Overall quality signal — [assessment] |

**Engagement rate benchmarks:**
- < 1%: Below average — content or timing issue
- 1-3%: Average
- 3-5%: Good
- 5-10%: Excellent
- 10%+: Exceptional (viral territory)

**Reply-to-like ratio** (key health metric):
- < 0.05: Low conversation — hook or CTA needs work
- 0.05-0.15: Normal
- 0.15-0.30: Good conversation driver
- 0.30+: Excellent — algorithm heavily rewards this

### Step 3 — Diagnose Performance

**If high impressions + low engagement:**
- Content reached people but didn't resonate
- Likely issue: weak hook, wrong audience timing, or content quality
- The algorithm showed it but people didn't engage → future posts may get reduced distribution

**If low impressions + high engagement:**
- Content resonated but wasn't distributed widely
- Likely issue: timing, small follower base, or posting frequency penalty
- The algorithm may expand distribution on future similar content

**If high replies specifically:**
- Excellent — this is the highest-weight signal
- Analyze what in the post triggered replies
- Replicate this pattern

**If high bookmarks:**
- Content was save-worthy — strong quality signal
- This content works well as a thread or series
- Consider expanding into related topics

### Step 4 — Extract Lessons

For each post reviewed, identify:
1. **What worked** — specific elements to replicate
2. **What underperformed** — specific elements to change
3. **Algorithm diagnosis** — why the algo distributed (or didn't) as it did
4. **Actionable next step** — one specific thing to try next post

### Step 5 — Output

Present:
1. **Performance summary** — Key metrics in a clear table
2. **Phoenix score analysis** — How each metric maps to algorithm signals
3. **Diagnosis** — Why the post performed as it did
4. **Lessons learned** — Specific, actionable takeaways
5. **Recommended next post** — Based on what worked, suggest the next content piece
6. **Trend over time** — If reviewing multiple posts, identify patterns (improving, declining, inconsistent)

## If Using OpenTweet MCP

Query analytics directly:
- "Show me my best performing posts this week"
- "What posting time got the best engagement?"
- Use this data to refine the schedule skill recommendations
