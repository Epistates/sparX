# sparX

Turn [Claude Code](https://claude.ai/code) into the ultimate X content engine. Every skill is grounded in how the Phoenix algorithm actually scores posts — not guesswork, but the documented signal weights from X's open-source ranking system.

sparX is a collection of Claude Code [skills](https://code.claude.com/docs/en/skills), [agents](https://code.claude.com/docs/en/sub-agents), and deep reference material that transforms your terminal into a full X content studio: drafting, optimizing, scoring, scheduling, trend research, performance review, and visual content creation.

## Quick Start

```bash
# Clone the repo
git clone https://github.com/epistates/sparX.git
cd sparX

# Open Claude Code
claude

# Draft your first post
/compose I just shipped a feature that cuts API latency by 73%

# Or optimize an existing draft
/optimize We released v2.0 with lots of improvements. Check it out at https://example.com
```

That's it. No API keys, no dependencies, no configuration. sparX works out of the box.

## Why sparX Exists

The X algorithm is not a black box. X [open-sourced](https://github.com/twitter/the-algorithm) its recommendation system, and the 2026 Phoenix update is documented in detail. The scoring weights are known:

| Signal | Weight vs Like | What This Means |
|--------|---------------|-----------------|
| Author replies to comments | 75–150× | Reply to every comment in the first hour |
| Threaded conversations | 13–27× | Create content that sparks genuine discussion |
| Reposts / Quote tweets | ~20× | Make posts worth sharing with commentary |
| Bookmarks | ~10× | Create reference-worthy, save-able content |
| Dwell time | Very high | Write posts people actually spend time reading |
| Likes | 1× | The least valuable positive signal |

Most creators optimize for likes. The algorithm cares about conversations, bookmarks, and dwell time — signals that are 10–150× more valuable.

sparX embeds this knowledge into every skill, so you don't have to memorize the hierarchy. Just use the skills and the optimization is built in.

## Skills

| Skill | Purpose | Example |
|-------|---------|---------|
| `/compose` | Draft algorithm-optimized posts | `/compose local LLM inference is now faster than cloud APIs` |
| `/thread` | Create high-engagement threads | `/thread 5 lessons from building a distributed cache` |
| `/optimize` | Score and rewrite existing drafts | `/optimize [paste your draft]` |
| `/hooks` | Generate scroll-stopping openers | `/hooks announcing a new developer tool` |
| `/schedule` | Data-driven posting time recommendations | `/schedule tech audience, EST timezone` |
| `/research` | Discover trending topics and content opportunities | `/research what's trending in the Rust ecosystem` |
| `/review` | Analyze post-publish performance | `/review 12K impressions, 47 replies, 89 bookmarks` |
| `/strategy` | Plan weekly/monthly content strategy | `/strategy dev tools niche, 500 followers, growth mode` |
| `/repurpose` | Transform content across formats | `/repurpose [blog post] → thread` |
| `/media` | Visual content strategy and creation | `/media what visual should I add to this benchmark post` |
| `/post` | Publish directly to X via browser | `/post [content]` or compose then `/post last` |
| `/analyze` | Read real analytics from X via browser | `/analyze recent` or `/analyze [post URL]` |
| `/engage` | Reply to comments via browser (75–150× multiplier) | `/engage [post URL]` or `/engage notifications` |
| `/setup` | Install optional integrations | `/setup remotion` |

### How Skills Work

When you invoke a skill, Claude:

1. Loads **CLAUDE.md** — essential Phoenix algorithm context (always present)
2. Reads the **skill instructions** — step-by-step process for the specific task
3. Progressively loads **reference docs** — deep algorithm data only when needed
4. Reads **supporting files** — templates, patterns, examples, checklists
5. Produces **optimized output** — scored, structured, ready to use

```
/compose → reads CLAUDE.md (algorithm weights)
         → reads compose/SKILL.md (composition process)
         → reads reference/scoring.md (signal details)
         → reads compose/templates.md (proven structures)
         → outputs: optimized post + score + alternatives
```

## Architecture

```
sparX/
├── .claude/
│   ├── skills/                  ← 14 slash-command skills
│   │   ├── compose/             ← /compose: Draft optimized posts
│   │   │   ├── SKILL.md         ← Composition process
│   │   │   ├── templates.md     ← Proven post structures & hooks
│   │   │   └── examples.md      ← High-performing post examples
│   │   ├── thread/              ← /thread: Create thread sequences
│   │   │   ├── SKILL.md         ← Thread building process
│   │   │   └── structures.md    ← 6 proven thread archetypes
│   │   ├── optimize/            ← /optimize: Score & rewrite drafts
│   │   │   ├── SKILL.md         ← Scoring methodology
│   │   │   └── checklist.md     ← Pre-publish optimization checklist
│   │   ├── hooks/               ← /hooks: Generate opening lines
│   │   │   ├── SKILL.md         ← Hook generation process
│   │   │   └── patterns.md      ← 8 hook pattern categories
│   │   ├── media/               ← /media: Visual content strategy
│   │   │   ├── SKILL.md         ← Media tier system & creation guides
│   │   │   └── remotion-guide.md ← Remotion video integration
│   │   ├── post/                ← /post: Publish to X via browser
│   │   ├── analyze/             ← /analyze: Read analytics via browser
│   │   ├── engage/              ← /engage: Reply management via browser
│   │   ├── schedule/            ← /schedule: Posting time optimization
│   │   ├── research/            ← /research: Trend & topic discovery
│   │   ├── review/              ← /review: Performance analysis
│   │   ├── strategy/            ← /strategy: Content planning
│   │   ├── repurpose/           ← /repurpose: Format transformation
│   │   └── setup/               ← /setup: Integration installation
│   └── agents/
│       └── scorer.md            ← Phoenix score simulation subagent
│
├── reference/                   ← Deep algorithm knowledge base
│   ├── algorithm.md             ← Complete Phoenix pipeline architecture
│   ├── scoring.md               ← All signal weights & multipliers
│   ├── content-formats.md       ← Format-specific optimization
│   ├── timing.md                ← Data-driven posting time analysis
│   └── penalties.md             ← What kills reach & how to avoid it
│
├── docs/                        ← Comprehensive documentation
│   ├── getting-started.md       ← First post in 5 minutes
│   ├── skills-guide.md          ← Detailed usage for every skill
│   ├── algorithm-guide.md       ← Creator-friendly algorithm explainer
│   ├── media-strategy.md        ← Visual content strategy
│   ├── integrations.md          ← Optional integration setup guide
│   └── playbooks.md             ← End-to-end workflow walkthroughs
│
├── setup/
│   └── README.md                ← Setup reference & file structure
├── CLAUDE.md                    ← Core algorithm context (always loaded)
└── README.md                    ← This file
```

## Browser Automation (claude-in-chrome)

Three skills turn sparX into a fully end-to-end system — draft, post, analyze, and engage without leaving Claude Code:

```
/compose my new feature cuts cold starts by 90%
    ↓ draft optimized, scored, ready
/post last
    ↓ opens X in Chrome, types the post, screenshots for your approval, publishes
    ↓ ...one hour later...
/engage [post URL]
    ↓ reads replies, prioritizes by value, drafts responses, posts with your approval
    ↓ ...next day...
/analyze [post URL]
    ↓ reads real metrics from X, runs Phoenix scoring analysis, suggests next content
```

| Skill | What It Does | Confirmation Required |
|-------|-------------|----------------------|
| `/post` | Types and publishes posts/threads in your browser | Yes — screenshots before every post |
| `/analyze` | Reads engagement metrics directly from X | No — read-only |
| `/engage` | Drafts and posts replies to comments | Yes — approval before each reply |

**Requirements:** [claude-in-chrome](https://github.com/anthropics/claude-in-chrome) extension installed. You must be logged into X in Chrome. The skills never handle authentication.

## The Phoenix Algorithm in 30 Seconds

Every "For You" post goes through this pipeline:

```
Your post → shown to ~10-20% of followers → Phoenix AI scores engagement signals
    ↓
Strong signals (replies, bookmarks, dwell)? → expand to more followers + non-followers
    ↓
Still strong? → broader distribution → viral potential
    ↓
Weak or negative signals? → distribution stops
```

**The critical window is the first 30-90 minutes.** Your followers' engagement in that window determines whether the algorithm amplifies or suppresses your post.

For the full technical breakdown, see [docs/algorithm-guide.md](docs/algorithm-guide.md).

## Visual Content & Media

sparX includes a tiered media strategy because X is the **only major platform where text outperforms video by ~30%** — but the best-performing posts combine text + visuals:

| Tier | Format | Effort | Best For |
|------|--------|--------|----------|
| 1 | Screenshots & images | Low | Benchmarks, code, data, before/after |
| 2 | GIFs & short animations | Medium | Quick demos, speed comparisons |
| 3 | Short video (15-45s) | Higher | Tutorials, product demos |
| 4 | Remotion (programmatic video) | Setup once | Recurring content, data viz, branded animations |

The `/media` skill recommends the right tier for your content and guides creation step by step. For programmatic video, run `/setup remotion` to install Remotion Agent Skills.

See [docs/media-strategy.md](docs/media-strategy.md) for the complete visual content guide.

## Optional Integrations

sparX works standalone. These integrations add superpowers:

| Integration | What It Adds | Cost | Setup |
|------------|-------------|------|-------|
| [Remotion](https://remotion.dev) | Programmatic video from React | Free (personal) | `/setup remotion` |
| [OpenTweet](https://opentweet.io) MCP | Scheduling, analytics, voice learning | $5.99/mo | `/setup opentweet` |
| [last30days](https://github.com/mvanhorn/last30days-skill) | Real-time trend research across 10+ platforms | ~$0.05/query | `/setup last30days` |
| [X API](https://developer.x.com) | Direct API access | Free-$5K/mo | `/setup x-api` |

See [docs/integrations.md](docs/integrations.md) for the full integration guide with decision tree.

## Playbooks

End-to-end workflows for common scenarios:

- **[Ship a Product Announcement](docs/playbooks.md#playbook-ship-a-product-announcement)** — Research → Draft → Media → Thread → Schedule → Review
- **[Weekly Content Pipeline](docs/playbooks.md#playbook-weekly-content-pipeline)** — Sustainable 5-post/week cadence in 30-45 min/day
- **[Grow from 0 to 1,000 Followers](docs/playbooks.md#playbook-grow-from-0-to-1000-followers)** — 90-day structured growth plan
- **[Repurpose a Blog Post](docs/playbooks.md#playbook-repurpose-a-blog-post)** — One blog post → a week of X content
- **[Recover from a Slump](docs/playbooks.md#playbook-recover-from-a-slump)** — Diagnose and fix declining engagement
- **[Create Visual Content with Remotion](docs/playbooks.md#playbook-create-visual-content-with-remotion)** — Set up programmatic video templates

See [docs/playbooks.md](docs/playbooks.md) for all playbooks.

## Documentation

| Document | What It Covers |
|----------|---------------|
| [Getting Started](docs/getting-started.md) | First post in 5 minutes, skill cheat sheet |
| [Skills Guide](docs/skills-guide.md) | Detailed usage for every skill with examples |
| [Algorithm Guide](docs/algorithm-guide.md) | Creator-friendly Phoenix algorithm explainer |
| [Media Strategy](docs/media-strategy.md) | Visual content tiers, tools, specifications |
| [Integrations](docs/integrations.md) | Optional integration setup and comparison |
| [Chrome Workflow](docs/chrome-workflow.md) | End-to-end browser automation with /post, /analyze, /engage |
| [Playbooks](docs/playbooks.md) | End-to-end workflow walkthroughs |

## Key Principles

**Algorithm-grounded, not algorithm-gaming.** Every recommendation traces to documented Phoenix scoring weights. But the goal is creating content humans genuinely engage with — the algorithm rewards what humans reward.

**Progressive disclosure.** CLAUDE.md has the essentials. Skills load deep reference docs only when needed. Supporting files (templates, patterns, examples) are available but not forced into context. This keeps Claude fast and focused.

**Text-first.** X is the only major platform where text beats video. sparX optimizes for text quality first, then layers on visual content where it amplifies the message.

**Conversations over likes.** A post with 10 genuine replies is worth more to the algorithm than a post with 270 likes. Every skill optimizes for reply triggers, not vanity metrics.

## Requirements

- [Claude Code](https://claude.ai/code) CLI
- That's it. Everything else is optional.

## License

MIT
