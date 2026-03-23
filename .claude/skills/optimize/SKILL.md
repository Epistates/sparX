---
name: optimize
description: Score and rewrite X post drafts for maximum algorithm reach. Use when the user has a draft tweet or post they want improved, reviewed, or scored against the Phoenix algorithm.
argument-hint: "[draft post to optimize]"
---

# Optimize an X Post Draft

You are a Phoenix algorithm scoring engine. Analyze a draft post, identify weaknesses against the scoring model, and rewrite for maximum predicted reach.

## Input

The user provides:
- A **draft post** (or thread) they want optimized
- An **X post URL** — read the actual published post via WebFetch, score it, and suggest an improved version
- A **URL to content** they posted about — read it to understand context for better optimization

### URL Resolution

If the input contains an X post URL (x.com or twitter.com), use WebFetch to read the post text. If you also need live engagement metrics to assess how it's currently performing, suggest the user run `/analyze [url]` which uses chrome for authenticated metric access.

For any other URL, read via WebFetch to understand the context behind the draft. See [../../../reference/url-reading.md](../../../reference/url-reading.md).

## Process

### Step 1 — Load Scoring Context
Read these references:
- [../../../reference/scoring.md](../../../reference/scoring.md) — weight hierarchy
- [../../../reference/penalties.md](../../../reference/penalties.md) — reach killers
- [checklist.md](checklist.md) — optimization checklist

### Step 2 — Analyze the Draft

Score the draft against every Phoenix signal:

**Positive Signal Analysis**
| Signal | Score (0-10) | Assessment |
|--------|-------------|------------|
| **Dwell potential** | ? | Will people spend time reading this? |
| **Reply magnet** | ? | Does this trigger genuine replies? |
| **Bookmark worthy** | ? | Would someone save this? |
| **Repost/Quote appeal** | ? | Would someone share this with their audience? |
| **Follow trigger** | ? | Does this make people want more from this author? |
| **Hook strength** | ? | Do the first 8-12 words stop the scroll? |

**Negative Signal Risk**
| Risk | Score (0-10, lower is better) | Assessment |
|------|------------------------------|------------|
| **"Not interested" risk** | ? | Could this feel irrelevant to non-target viewers? |
| **Engagement bait** | ? | Does it use manipulative patterns? |
| **Link penalty** | ? | Are external links in the body? |
| **Spam signals** | ? | Excessive hashtags, salesy tone, etc.? |

**Conversation Velocity**: Assess whether this post sets up the author to create conversation threads (75–150× multiplier). Does the CTA invite replies worth responding to?

**Composite Phoenix Score**: Weight the signals by algorithm hierarchy (author reply conversations 75–150×, replies 13–27×, reposts/quotes ~20×, bookmarks 10×, dwell very high, likes 1×) and produce an estimated composite score from 0-100.

### Step 3 — Identify Top 3 Issues

List the 3 biggest problems in priority order. Be specific:
- Bad: "Hook could be better"
- Good: "Hook uses jargon ('Metal 4 kernels') that only insiders understand — narrows the test audience"

### Step 4 — Rewrite

Produce an optimized version that:
1. Fixes all identified issues
2. Preserves the author's core message and voice
3. Maximizes the highest-weight signals (conversation velocity, dwell, bookmarks)
4. Follows all penalty avoidance rules

### Step 4b — Enforce Character Limits

**Hard limit: 280 characters per post.** Verify the optimized version fits.

- If it fits → show character count: `(237/280)`
- If it exceeds 280 → either tighten the copy to fit, or split into a thread with clear `[Tweet N] (count/280)` markers and `---` separators between tweets
- If the original was a thread, verify each tweet individually

### Step 5 — Output

**Always end with a clear, visible Phoenix Score Block.** This is what users look for — the "algorithm thinks this is good" signal.

Present in this order:

**1. Original draft** with character count

**2. Phoenix Score (original):**
```
Phoenix Score: 3.2/10
Strengths: [specific positives]
Weaknesses: [specific issues]
```

**3. Top 3 issues** — specific, actionable

**4. Optimized version** with character count per tweet (ready to copy-paste)
- If multi-tweet: each tweet separated with `---` and `[Tweet N] (count/280)` markers

**5. Phoenix Score (optimized):**
```
Phoenix Score: 8.1/10 (+4.9)
Strengths: strong dwell potential (specific numbers create pause), reply trigger (question CTA), bookmark-worthy (actionable reference)
Weaknesses: [any remaining concerns]
```

**6. What changed and why** — brief explanation

**7. Alternative hooks with scores** — 2-3 alternative opening lines, each scored as the cumulative post score if that hook replaced the one in the optimized version:

```
Alternative hooks:
  "Cut our API latency by 73% with one config change."  → 8.6/10 (specific number + curiosity)
  "Everyone told us to use Redis. We deleted it."        → 7.9/10 (contrarian + tension)
  "The caching decision that saved us $2K/month."        → 8.2/10 (money hook + specificity)
```

**8. Timing reminder** — based on the content type and likely audience:
- Recommended day/time window from `reference/timing.md`
- "Post when you can stay available for 30-60 min to reply — that's the 75–150× multiplier window"

### Phoenix Score Scale

| Score | Meaning | Action |
|-------|---------|--------|
| 9-10 | Exceptional — publish at peak time, clear your schedule for replies | Post immediately |
| 7-8 | Strong — good to publish as-is | Post with confidence |
| 5-6 | Decent — will perform but could be better | Consider suggested improvements |
| 3-4 | Weak — significant issues reducing reach | Rewrite before posting |
| 1-2 | Reach killer present — this will hurt your account | Do not post, fix fundamental issues |

## Optimization Priorities (in order)

1. **Remove reach killers first** — links in body, engagement bait, hashtag spam
2. **Strengthen the hook** — first 8-12 words determine everything
3. **Maximize conversation velocity** — design the CTA so replies invite author responses (75–150× multiplier)
4. **Add reply triggers** — questions, takes worth debating (13–27×)
5. **Increase dwell potential** — specificity, proof points, readability formatting
6. **Boost bookmark appeal** — make it reference-worthy
7. **Preserve authenticity** — never sacrifice voice for optimization
