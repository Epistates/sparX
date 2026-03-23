# Understanding the X Algorithm — A Creator's Guide

This guide explains how the X (Twitter) algorithm decides who sees your posts, translated into actionable knowledge for content creators. For the full technical reference, see `reference/algorithm.md`.

## How "For You" Works

Every time someone opens their X feed, a pipeline processes thousands of candidate posts to select the ~50 they'll see. Your post competes for those slots.

```
Your post is published
        ↓
Shown to a small slice of your followers (~10-20%)
        ↓
Phoenix AI predicts: will each viewer reply, bookmark, dwell, repost, or disengage?
        ↓
Based on predictions + early actual engagement → expand or suppress
        ↓
If expanding: test with a small out-of-network audience
        ↓
If that works too: broader distribution → "viral"
```

The key insight: **the algorithm doesn't decide if your post is "good." It predicts whether specific users will engage with it.** Your job is to create content that triggers high-value engagement signals.

## The Engagement Hierarchy

Not all engagement is created equal. The algorithm weights different actions dramatically differently:

```
                                                ▲ Algorithm Value
                                                │
  Author replies to comments ─────────── 75-150× ████████████████████████████████
  Threaded conversations ──────────────── 13-27× ████████████████
  Reposts / Quote tweets ──────────────── ~20×   ██████████████
  Bookmarks ───────────────────────────── ~10×   ██████████
  Dwell time (time spent reading) ─────── High   █████████
  Video completion % ──────────────────── High   █████████
  Profile visits ──────────────────────── Medium ██████
  Likes ───────────────────────────────── 1×     █
                                                │
                                                ▼
```

**The takeaway**: A post with 10 genuine replies is worth more to the algorithm than a post with 270 likes. Optimize for conversations, not likes.

## The Critical Window: First 30-90 Minutes

The first 30-90 minutes after posting determine your post's fate. Here's why:

1. **Initial test**: Your post is shown to a small sample of your followers
2. **Signal collection**: Phoenix measures reply rate, dwell time, bookmark rate, negative signals
3. **The decision**: Based on these signals, the algorithm either expands distribution or lets the post die

**What this means practically:**
- Post when your audience is active (not midnight)
- Be available to reply to comments in the first hour (author replies = 75-150× multiplier)
- Never post and disappear
- Front-load your best content in the hook (determines whether the test audience engages)

## How Posts Go Viral (Out-of-Network Discovery)

Your followers are the launchpad. To reach people who don't follow you:

1. **Strong initial signal** from your followers (replies, bookmarks, dwell)
2. **Embedding match** — Phoenix uses AI to determine if your post's topic matches non-follower interest clusters
3. **No negative signals** — no blocks, mutes, or "not interested" from the test audience
4. **Expansion testing** — small batches of non-followers see it, and if they engage, more batches follow
5. **Compound effect** — each round of engagement triggers the next expansion

**For small accounts**: This means your followers are your most important asset, even if you only have 50. Their engagement in the first hour is the gateway to broader reach.

## The Five Things That Kill Reach

### 1. External Links in the Post Body
**Impact**: 30-50% reach reduction

X wants to keep users on the platform. External links signal that you're sending people away.

**Fix**: Put links in a reply to your own post, or use "link in bio."

### 2. Engagement Bait
**Impact**: Reduced distribution + trust penalty

"Like if you agree", "Follow for more", "RT to spread the word" — the algorithm classifies these as low-quality patterns.

**Fix**: Ask genuine questions that invite real discussion.

### 3. Negative User Signals
**Impact**: Asymmetric — one "not interested" outweighs many likes

Blocks, mutes, reports, and "not interested" clicks do far more damage than equivalent positive signals do good. The algorithm is conservative — it would rather not show your post than risk a bad experience.

**Fix**: Stay on-topic for your niche. Don't be gratuitously provocative. Deliver on what your hook promises.

### 4. Posting Without Replying
**Impact**: Wasted multiplier opportunity

Author replies to comments carry a 75-150× weight. If you post and don't reply to comments, you're leaving the single biggest algorithmic boost on the table.

**Fix**: Block 30-60 minutes after each post to reply to every comment.

### 5. Spam Patterns
**Impact**: Broad suppression

More than 10 posts/day, identical content, automated engagement (likes/follows), unnaturally regular posting intervals — all trigger spam classifiers.

**Fix**: Post quality content at human-realistic intervals. 3-5 posts/week is optimal for most accounts.

## Content That Scores High

Based on the scoring model, posts that perform best share these characteristics:

### High Dwell Time
- Insight-dense content people read slowly
- Surprising information that makes people pause
- Well-formatted with line breaks (easier to read = longer reading time)
- Screenshots, tables, or code that require examination

### Reply Magnets
- Genuine questions with specific enough framing to answer
- Debatable takes that invite "yes, but..." responses
- Personal experiences that prompt "same here" or "I did it differently"
- Ask for recommendations or preferences

### Bookmark Appeal
- Actionable reference material (tips, commands, configurations)
- Curated lists of resources
- Step-by-step tutorials
- Benchmark data people want to revisit

### Low Negative Risk
- On-topic for your established niche
- Hook matches the content (no bait-and-switch)
- Value delivered, not just promised
- Authentic voice (not corporate/AI-generic)

## The Text Advantage

X is the only major platform where **text outperforms video by ~30%**. This is because:

- X's culture is text-first (unlike TikTok, Instagram, YouTube)
- The algorithm can analyze text content more deeply for relevance matching
- Text posts have lower "skip" rates than video (less commitment to start reading)
- Dwell time on text is a stronger signal than passive video viewing

**The optimal strategy**: Text-first posts with supporting visual media. The text carries the algorithm score; the visual boosts dwell time.

## Threads: The 3× Engagement Multiplier

Threads (multi-tweet sequences) get approximately 3× more engagement than equivalent single tweets because:

1. **More dwell time** — multiple tweets to read through
2. **The algorithm treats threads as one unit** — no diversity filter penalty
3. **Each tweet can surface independently** — individual tweets from your thread can appear in other people's feeds
4. **Reply surface area** — people can reply to any tweet in the thread, multiplying conversation opportunities
5. **Extended lifetime** — active threads maintain visibility longer than single posts

**The sweet spot is 5-7 tweets.** Shorter than 5 doesn't justify the thread format. Longer than 10 risks drop-off.

## Premium: The Distribution Multiplier

Premium (verified) accounts receive a direct scoring boost:

| Tier | Boost |
|------|-------|
| Free | 1× (baseline) |
| Premium | 2-4× distribution |
| Premium+ | Up to 10× in some cases |

This is applied at the scoring stage — it's a multiplier on your post's final score. For small accounts trying to grow, Premium is the single highest-ROI investment.

## Practical Daily Routine (20-30 minutes)

1. **Before posting** (10-15 min): Reply to 10-15 posts in your niche. This warms up the algorithm's model of your interests and makes you visible to potential audience.

2. **Post** (5 min): Publish your content at peak time for your audience.

3. **After posting** (15-30 min): Reply to every comment on your post. Substantive replies, not just "thanks!" This is the 75-150× multiplier in action.

4. **Throughout the day** (5 min scattered): Reply to 5-10 more posts in your niche. Build relationships. The algorithm notices your engagement patterns.
