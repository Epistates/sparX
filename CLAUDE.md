# sparX — X Post Optimization System

Turn Claude Code into the ultimate X (Twitter) content engine. Every skill in this project is grounded in how the Phoenix algorithm actually scores posts.

## How This Project Works

This is a **skill-based system**. You interact with it through `/slash-commands`:

| Skill | Purpose |
|-------|---------|
| `/compose` | Draft algorithm-optimized single posts |
| `/thread` | Create high-engagement thread sequences |
| `/optimize` | Score and rewrite existing drafts for max reach |
| `/hooks` | Generate scroll-stopping opening lines |
| `/schedule` | Get optimal posting times based on data |
| `/research` | Research trending topics in your niche |
| `/review` | Analyze post-publish performance |
| `/strategy` | Plan weekly content strategy |
| `/repurpose` | Transform content across formats (post→thread, thread→post, etc.) |
| `/media` | Plan and create visual content (screenshots, GIFs, Remotion video) |
| `/post` | Publish posts/threads directly to X via chrome browser automation |
| `/analyze` | Read real engagement analytics from X via browser |
| `/engage` | Manage replies and conversations on X via browser (75–150× multiplier) |
| `/setup` | Install optional integrations (Remotion, OpenTweet, last30days, X API) |
| `/test` | Verify sparX setup is working correctly |

## Phoenix Algorithm — Essential Context

**Always apply this knowledge when working with X content in this project.**

### The Scoring Formula

Every post shown in "For You" is scored by the Phoenix transformer:

```
Final Score = Σ (weight × P(action)) - negative_penalties + diversity_adjustment
```

Phoenix predicts 15-18 engagement probabilities per user×post pair. The weights are **not equal** — this hierarchy determines reach:

| Signal | Weight vs Like | Why It Matters |
|--------|---------------|----------------|
| Author replies to comments | 75–150× | Creates conversation velocity → massive distribution |
| Deep replies / threaded convos | 13–27× | Strongest standard positive signal |
| Repost / Quote | ~20× | High trust signal from other users |
| Bookmark | ~10× | "Silent like" — extremely predictive of quality |
| Dwell time (time spent reading) | Very high | Core transformer signal; longer = much better |
| Video completion % | High | Media gets natural boost |
| Like | 1× | Baseline — least valuable positive signal |
| Block/Mute/Report/Not interested | Heavy penalty | Asymmetric — one bad interaction tanks future reach |

### Critical Rules (Violating These Kills Reach)

1. **First 30-90 minutes decide everything.** The initial test slice from followers must trigger high P(reply) and P(dwell) or the post dies.
2. **External links are penalized 30-50%.** Never put bare links in the main post. Use a follow-up reply or "link in bio."
3. **"Follow for more" / engagement bait** triggers low-quality signals.
4. **Text outperforms video by ~30% on X** (unique among platforms). But video+text combos maximize dwell.
5. **1-2 hashtags optimal.** More looks spammy. Zero is fine for strong content.
6. **Premium/Verified accounts get 2-4× distribution boost** (up to 10× in some cases).
7. **The diversity filter** won't flood feeds with multiple posts from one low-follower account. Space posts 1-2h apart.
8. **Author replies to every comment** in the first hour is the single highest-leverage action (75-150× multiplier).

### What Makes Posts Score High

- **First 8-12 words are everything** — this is the stop-scroll hook
- **Dwell time** — longer, more readable posts that people actually read
- **Reply magnets** — questions, controversial takes, "what's your experience?"
- **Visual proof** — screenshots, benchmarks, before/after
- **Social proof** — numbers, stars, user counts, testimonials
- **Specificity** — "2.1× faster" beats "much faster"

### Optimal Thread Structure (7 tweets is the sweet spot)

1. **Hook** — Promise a specific, valuable outcome
2-6. **Value delivery** — One clear insight per tweet, each standalone
7. **CTA** — Question that triggers replies + soft ask

Threads get **3× more engagement** than single tweets when quality is comparable.

## Content Quality Standards

- We write posts that humans want to engage with, not posts that trick an algorithm
- Every post must deliver genuine value: insight, entertainment, utility, or perspective
- Authenticity > optimization. The algorithm rewards what humans reward.
- No engagement bait, no empty platitudes, no "10 things you need to know" without substance

## Reference Documents

For deep dives, skills should read from `reference/`:
- `reference/algorithm.md` — Complete Phoenix pipeline architecture
- `reference/scoring.md` — Detailed scoring weights and signal analysis
- `reference/content-formats.md` — Format-specific guidance (posts, threads, polls, quotes)
- `reference/timing.md` — Data-driven posting time optimization
- `reference/penalties.md` — Comprehensive guide to what kills reach

## Clipboard Output

**When the user approves a final post, thread, or reply — copy it to the clipboard automatically.** This avoids copy errors from terminal padding, invisible characters, and line-break differences.

Use the platform-appropriate command:
- **macOS**: `echo -n "content" | pbcopy`
- **Linux**: `echo -n "content" | xclip -selection clipboard`
- **Windows/WSL**: `echo -n "content" | clip.exe`

For threads, copy all tweets separated by a blank line so the user can paste them sequentially.

If the user selects an alternative hook, reconstruct the full post with that hook swapped in and copy the updated version.

Confirm with: `Copied to clipboard.`

## MCP Integration

If OpenTweet MCP is configured, skills can directly schedule and post content. See `setup/` for configuration instructions. Skills should check for MCP availability and offer scheduling when available, but always work standalone for draft generation.
