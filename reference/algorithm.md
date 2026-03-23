# Phoenix Algorithm — Complete Pipeline Architecture

## For You Feed Pipeline

Every "For You" feed request flows through this exact pipeline:

```
FOR YOU FEED REQUEST
    ↓
HOME MIXER (orchestration layer)
    ↓
1. Query Hydration
   - Load user engagement history
   - Build user feature vector (interests, past interactions, network graph)
    ↓
2. Candidate Sources
   ├── Thunder (in-network)
   │   - Posts from people you follow
   │   - In-memory store, sub-millisecond latency
   │   - Recency-weighted: newer posts from follows get priority
   │
   └── Phoenix Retrieval (out-of-network)
       - Two-tower embedding model
       - Your interest embedding vs. global post embeddings
       - Similarity search across entire corpus
       - This is how posts reach people who DON'T follow you
    ↓
3. Hydration
   - Attach metadata: author info, media entities, video length
   - Enrich with engagement counts, author reputation scores
    ↓
4. Pre-Scoring Filters
   - Dedup (same content, reposts)
   - Old posts (age decay)
   - Self-posts (you don't see your own)
   - Muted keywords, blocked authors
   - Spam classifiers
    ↓
5. Scoring (Phoenix Transformer)
   - Full transformer model (Grok-1 derived)
   - Input: [user context embedding] + [single candidate post]
   - Candidate Isolation: posts cannot attend to each other
   - Output: 15-18 action probabilities simultaneously
    ↓
6. Weighted Scorer + Author Diversity Scorer
   - Apply weight hierarchy to action probabilities
   - Attenuate repeated authors (won't flood with one account)
   - Apply recency/variety mixing
    ↓
7. Selection
   - Top-K by final score
   - Position-aware adjustments
    ↓
8. Post-Selection Visibility Filters
   - Final safety checks: deleted, spam, violence, gore
    ↓
RANKED FEED
```

## Phoenix Transformer — How It Works

Phoenix is a Grok-1-derived transformer that serves dual roles:

### Retrieval (Two-Tower)
- Separate encoders for users and posts
- Both produce embeddings in shared vector space
- Similarity search finds relevant out-of-network content
- **This is the gateway to viral reach** — your post's embedding must be close to target users' interest embeddings

### Ranking (Full Transformer)
- Takes user context + single candidate post as input
- **Candidate Isolation** via special attention masking
  - Posts cannot attend to each other during scoring
  - Each score is independent and cacheable
  - Prevents position-based gaming
- Outputs simultaneous probabilities for all engagement actions

### What This Means for Content Creators

1. **Embedding quality determines discovery.** Your post needs to embed close to your target audience's interest vectors. Use the vocabulary, concepts, and framing your niche uses.

2. **Each post is scored independently.** You can't boost one post by having another do well — each stands on its own merit.

3. **In-network (Thunder) is your launch pad.** Your followers see it first. Their engagement in the first 30-90 minutes determines whether Phoenix Retrieval picks it up for out-of-network distribution.

4. **The transformer learns sequences.** It doesn't just look at this post — it considers the user's entire engagement history. Users who consistently engage with your type of content become more likely to see future posts.

## Out-of-Network Discovery Mechanics

For a post to escape the follower bubble:

1. **Strong initial signal** from followers (replies, bookmarks, dwell time)
2. **Embedding match** — post topic aligns with non-follower interest clusters
3. **No negative signals** — no blocks, mutes, or "not interested" from the test audience
4. **Author quality signal** — account history, follower/following ratio, past engagement patterns
5. **Premium boost** — verified accounts get 2-4× distribution amplification

The key insight: **out-of-network reach is earned, not given.** The algorithm tests with a small non-follower sample first, then expands distribution only if engagement metrics justify it.

## The Engagement Velocity Curve

```
Post published
    |
    v
[0-30 min] — Critical window
    - Shown to ~10-20% of followers
    - Phoenix measures: reply rate, dwell time, bookmark rate
    - Decision: expand or suppress
    |
    v
[30-90 min] — Expansion or death
    - If metrics strong: shown to more followers + small out-of-network test
    - If metrics weak: distribution flatlines
    |
    v
[90 min - 6 hr] — Viral window
    - Strong posts enter out-of-network distribution
    - Each expansion round tests new audience segment
    - Compound effect: more engagement → more distribution → more engagement
    |
    v
[6-24 hr] — Long tail
    - Posts with sustained engagement continue getting distributed
    - Threads get extended lifetime (each reply in thread renews visibility)
    - Diminishing returns as recency decay kicks in
```

## Author Diversity Scorer

The algorithm deliberately prevents any single account from dominating a user's feed:

- **Attenuation**: After showing 1-2 posts from the same author, subsequent posts get score penalties
- **Impact on strategy**: Spacing posts 1-2 hours apart avoids self-competition
- **Exception**: Threads count as one "unit" — the algorithm treats a thread as a single content piece
- **For small accounts**: This means you can't brute-force reach with volume. Quality per post matters more than quantity.
