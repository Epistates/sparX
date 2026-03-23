# Phoenix Scoring — Weights, Signals & Multipliers

## Action Predictions

Phoenix predicts these probabilities for every user×post pair:

### Positive Signals
| Action | Description | Approx Weight vs Like |
|--------|-------------|----------------------|
| P(reply) | User will reply to this post | 13-27× |
| P(author_reply_conversation) | Author replies creating conversation | 75-150× |
| P(repost) | User will repost | ~20× |
| P(quote) | User will quote tweet | ~20× |
| P(bookmark) | User will bookmark | ~10× |
| P(dwell) | User will spend significant time reading | Very high (core signal) |
| P(video_view) | User will watch video | High |
| P(video_completion) | User will watch to completion | Very high |
| P(photo_expand) | User will expand/click photo | Medium |
| P(click) | User will click on post/links | Medium |
| P(profile_visit) | User will visit author's profile | Medium |
| P(follow_author) | User will follow the author | High |
| P(like) | User will like the post | 1× (baseline) |

### Negative Signals
| Action | Impact |
|--------|--------|
| P(not_interested) | Moderate penalty — suppresses similar future content |
| P(block) | Severe — tanks reach to that user's network cluster |
| P(mute) | Severe — similar to block for scoring |
| P(report) | Most severe — can trigger content review + broad suppression |

## The Asymmetry Rule

**Negative signals are asymmetric.** One block or report does far more damage than one like does good. The algorithm is designed to be conservative — it would rather not show a post than risk a negative experience.

**Practical implication**: A post that gets 100 likes and 3 "not interested" signals may perform worse than a post that gets 50 likes and zero negative signals.

## Dwell Time — The Hidden Giant

Dwell time (how long a user spends looking at your post) is one of Phoenix's most powerful signals because:

1. **It's hard to fake** — bots can like instantly but can't simulate genuine reading time
2. **It correlates with quality** — longer, more substantive posts that people actually read score higher
3. **It's measured passively** — users don't have to take any action; just reading counts
4. **Behavioral sequences matter** — the transformer learns patterns like "read slowly → scroll back up → bookmark"

**Example**: Two posts about the same topic (switching from Redis to SQLite). Post A: "We switched to SQLite. It's faster." — 3 seconds average dwell, 800 impressions. Post B: "We switched from Redis to SQLite for our caching layer.\n\nLatency dropped 40%. Ops complexity dropped 90%.\n\nNot every problem needs a distributed system." — 11 seconds average dwell, 14K impressions. Same message, but the specificity and formatting created 3.5× longer dwell time and 17× more distribution.

### How to Maximize Dwell Time
- Write posts worth reading slowly (insight-dense, well-structured)
- Use line breaks to create visual rhythm (easier to read = longer reading)
- Include surprising information that makes people pause
- Images/screenshots that require examination (benchmark tables, code snippets)
- Threads naturally increase dwell (multiple tweets to read through)

## Conversation Velocity — The 75-150× Multiplier

The single most impactful signal is **author replies to comments**. Here's why:

1. Your post gets a reply → that's 13-27× weight
2. You reply back → the algorithm sees a **conversation**
3. A conversation thread signals high-quality, engaging content
4. Phoenix weights this at 75-150× a simple like
5. Each conversation thread is independently weighted

**Example**: A developer posted a benchmark comparison that got 15 replies. They replied to all 15 within 45 minutes, asking follow-up questions. 8 of those turned into 2-3 message threads. Result: 47K impressions from 600 followers (78× distribution multiplier). A similar post the week before with 12 replies but zero author responses got 3K impressions. The content quality was comparable — the difference was entirely conversation velocity.

### Maximizing Conversation Velocity
- Reply to **every** comment in the first hour
- Ask follow-up questions in your replies (extends the conversation)
- Your reply quality matters — substantive replies > "thanks!"
- Multiple conversation threads on one post compound the signal

## The Premium/Verified Multiplier

Premium accounts receive algorithmic distribution boosts:

| Tier | Approximate Boost |
|------|------------------|
| Premium (Blue checkmark) | 2-4× distribution |
| Premium+ | Up to 10× in some cases |
| Free account | 1× baseline |

This multiplier applies at the scoring stage — it's a direct weight adjustment on the final score. For small accounts trying to grow, this is the single highest-ROI investment.

## Signal Interaction Effects

Signals don't exist in isolation. Phoenix models interactions:

- **Bookmark + Dwell** = very strong signal (user read carefully AND saved)
- **Reply + Quote** = strong amplification (user engaged AND shared with commentary)
- **Quick like, no dwell** = weak signal (low-effort engagement)
- **Profile visit + Follow** = strongest growth signal (content led to new connection)
- **Dwell + Not Interested** = conflicting (read but didn't like — reduces future similar content)

## Content-Type Scoring Adjustments

| Content Type | Scoring Bonus | Notes |
|-------------|---------------|-------|
| Text-only | Neutral (but outperforms video by ~30% on X) | Text is king on X uniquely among platforms |
| Image/screenshot | Moderate boost | Photo_expand signal provides additional data |
| Video (< 60s) | Moderate boost | Completion rate is key — shorter = better completion |
| Video (> 60s) | Lower boost unless completion high | Long videos risk low completion penalty |
| Poll | Engagement boost | Voting counts as interaction |
| Thread | Per-tweet scoring + thread bonus | Treated as single unit for diversity filter |
| Quote tweet | Amplified | Both posts benefit from the interaction |
| Link post | 30-50% penalty | External links are actively suppressed |

## Score Decay

Post scores decay over time:
- **0-6 hours**: Full score
- **6-24 hours**: Moderate decay (~50% reduction)
- **24-48 hours**: Significant decay (~80% reduction)
- **48+ hours**: Minimal distribution unless exceptional ongoing engagement

Exception: Threads with active conversations can maintain visibility for days.
