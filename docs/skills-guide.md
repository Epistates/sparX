# Skills Guide — Detailed Usage & Examples

## /compose — Draft Optimized Posts

**When to use**: You have a topic, rough draft, or announcement and want an algorithm-optimized post.

### Examples

**From a topic:**
```
/compose the hidden costs of microservices that nobody talks about
```

**From a rough draft:**
```
/optimize We just added WebSocket support to our API. It's really fast and works well with existing clients. Check our docs for more info.
```

**From a product announcement:**
```
/compose announcing our v3.0 release: 40% smaller bundle size, tree-shaking support, and zero-config TypeScript
```

### What you get

1. An optimized post ready to copy-paste
2. Phoenix score breakdown (dwell, reply, bookmark, negative risk — each 0-10)
3. A separate reply draft if links are needed
4. 2-3 alternative hooks to choose from

### Pro tips

- Provide as much raw material as possible — specific numbers, benchmarks, user quotes
- Mention your audience if it's niche: `/compose for Rust developers: memory-safe async runtime`
- If you have a link, include it in your prompt — Claude will handle it correctly (in a reply, not the body)

---

## /thread — Create Thread Sequences

**When to use**: Deep dives, tutorials, storytelling, benchmark breakdowns, or anything that benefits from multi-tweet format.

### Examples

**Tutorial thread:**
```
/thread step-by-step guide to setting up a local LLM on Apple Silicon
```

**From notes:**
```
/thread Here are my rough notes, turn into a thread:
- switched from PostgreSQL to SQLite for caching
- latency dropped 40%
- ops complexity dropped 90%
- lesson: not everything needs a distributed system
```

**From a blog post:**
```
/thread [paste full blog post] — distill into a 7-tweet thread
```

### What you get

1. Complete thread (5-7 tweets, each under 280 chars)
2. Character count per tweet
3. Score breakdown
4. Suggested visual content for middle tweets
5. Link reply draft
6. Suggested posting time

### Thread archetypes

The skill uses 6 proven structures — it selects the best one for your content:
- **Tutorial**: Step-by-step with actionable takeaways
- **Deep Dive**: Technical exploration with findings
- **Story**: Narrative arc (problem → struggle → breakthrough → result)
- **Listicle**: Curated insights or tips
- **Comparison**: Side-by-side analysis with data
- **Contrarian**: Challenging conventional wisdom

---

## /optimize — Score & Rewrite Drafts

**When to use**: You have a draft and want to know how the algorithm would score it, with specific improvements.

### Examples

**Score a draft:**
```
/optimize Just shipped our new CLI tool. It makes deployment easy. Built with Go. Star us on GitHub: https://github.com/example/tool
```

**Output includes:**
```
Phoenix Score: 32/100

Top 3 Issues:
1. Link in body → 30-50% reach penalty (move to reply)
2. No hook — "Just shipped" is generic, no stop-scroll power
3. No reply trigger — nothing invites engagement

Optimized Version:
"Deploying to production shouldn't require a 200-line YAML file.

Our new CLI does it in one command. Written in Go. 2-second cold starts.

What's your current deploy process look like? Genuinely curious."

New Score: 71/100
```

### Pro tips

- Run `/optimize` on your draft BEFORE posting — it catches reach killers you might miss
- Use it iteratively: optimize → tweak → optimize again
- The score is relative — context matters (a 60 from a 50-follower account is different from a 50K account)

---

## /hooks — Generate Opening Lines

**When to use**: You know what you want to post but need a compelling first line.

### Examples

```
/hooks local AI inference becoming faster than cloud APIs
```

```
/hooks announcing a developer tool for automated testing
```

### What you get

7-10 hooks across different pattern categories:
- **Curiosity gap**: "Local AI just crossed a threshold nobody expected—"
- **Specific number**: "2.3× faster than GPT-4 API. Running on a laptop."
- **Contrarian**: "Cloud AI is becoming the new technical debt."
- **Pain point**: "Developers are still paying $0.03/request for something their MacBook can do."
- **Before/after**: "$847/mo in API costs → $0. What changed:"

Each hook is ranked by predicted effectiveness and annotated for best use case.

---

## /schedule — Optimal Posting Times

**When to use**: Deciding when to post, building a weekly schedule, or planning a content calendar.

### Examples

**Single post:**
```
/schedule when should I post a technical thread aimed at US developers
```

**Weekly plan:**
```
/schedule build me a weekly posting schedule, developer tools niche, EST timezone
```

**Content calendar:**
```
/schedule monthly content calendar, 3 posts per week, B2B SaaS audience
```

### Key timing data the skill uses

- **Wednesday 9 AM ET** is the single highest-engagement slot
- **Tuesday-Thursday** dominates weekday engagement
- **Threads** perform best at 8-9 AM ET (morning reading time)
- **Polls** peak at 10-11 AM ET (catches morning + afternoon voters)
- **Weekend** engagement drops ~40% vs midweek

---

## /research — Topic & Trend Discovery

**When to use**: Finding content ideas, understanding what's trending, or discovering conversations to join.

### Examples

```
/research what are developers talking about in the Rust ecosystem right now
```

```
/research trending debates in the AI/ML space this week
```

```
/research content opportunities around developer experience and tooling
```

### What you get

1. Trend summary (what's happening in the niche right now)
2. Top 5 content opportunities ranked by engagement potential
3. Content briefs for each opportunity (angle, format, hook idea, key points)
4. Suggested posting schedule
5. Reply farming targets (active discussions to engage with before posting)

### Enhanced with last30days

If you've installed last30days (`/setup last30days`), the research skill searches across X, Reddit, Hacker News, YouTube, and more with a 30-day recency window. Without it, the skill uses web search.

---

## /review — Performance Analysis

**When to use**: Understanding how your published posts performed and extracting lessons.

### Examples

**With engagement data:**
```
/review This post got 12,000 impressions, 47 replies, 23 reposts, 156 likes, 89 bookmarks
```

**With a URL:**
```
/review https://x.com/username/status/123456789
```

**General review:**
```
/review here are my last 5 posts with their metrics: [data]
```

### Key metrics the skill analyzes

| Metric | What it tells the algorithm |
|--------|---------------------------|
| Reply-to-like ratio | >0.15 = strong conversation driver |
| Bookmarks | Quality signal — people save useful content |
| Impressions vs followers | Distribution multiplier (>2× = algorithm amplifying) |
| Engagement rate | <1% = underperforming, 5%+ = excellent |

---

## /strategy — Content Planning

**When to use**: Building a content strategy, setting growth goals, or planning your content mix.

### Examples

```
/strategy I'm a backend engineer posting about distributed systems, 400 followers, want thought leadership
```

```
/strategy indie hacker building in public, SaaS product, 1.2K followers, goal is 5K by end of Q2
```

### What you get

1. Account stage assessment (Launch / Growth / Scale / Authority)
2. 3-5 content pillars with example topics
3. Weekly posting calendar with specific days and times
4. Growth tactics matched to your current stage
5. 30-day measurable goals
6. 10 specific post ideas across your pillars

---

## /repurpose — Format Transformation

**When to use**: Getting more mileage from existing content by transforming it across formats.

### Examples

**Blog post to thread:**
```
/repurpose [paste blog post] → thread
```

**Thread to single post:**
```
/repurpose [paste thread] → single post distilling the key insight
```

**One insight, multiple angles:**
```
/repurpose "SQLite is underrated for caching" → give me 5 different post angles
```

**Changelog to announcement:**
```
/repurpose v2.0 changelog: added WebSocket support, 40% faster cold starts, new CLI → announcement post
```

---

## /media — Visual Content Strategy

**When to use**: Adding images, videos, GIFs, or screenshots to your posts. Deciding what visual to create.

### Examples

```
/media what visual should I add to a post about benchmark results
```

```
/media create a Remotion animation showing a 3× speed improvement
```

```
/media I have a post about our new CLI tool — what screenshot should I take
```

### Media tier system

The skill recommends from 4 tiers (ordered by effort-to-impact):

1. **Screenshots** (lowest effort, highest ROI) — terminal output, benchmarks, code
2. **GIFs** (medium effort) — 5-10s demos, speed comparisons
3. **Short video** (higher effort) — tutorials with captions, product demos
4. **Remotion** (specialized) — programmatic animations, templated recurring content

---

## /setup — Integration Setup

**When to use**: Installing optional integrations to enhance sparX.

### Examples

```
/setup remotion
/setup opentweet
/setup last30days
/setup x-api
/setup all
```

Each integration walks you through prerequisites, installation, verification, and post-setup usage. See [Integrations Guide](integrations.md) for details.

---

## /post — Publish to X via Browser

**When to use**: You have composed content and want to publish it directly to X without copy-pasting. Requires claude-in-chrome.

### Examples

**Post the output of a previous /compose:**
```
/post last
```

**Post specific content:**
```
/post Cut our deploy time from 4 minutes to 11 seconds. One config change.\n\nThe secret: ARM-native Docker layers skip emulation entirely.\n\nWhat's your current build time?
```

**Post a thread:**
```
/post [paste your thread tweets]
```

### How it works

1. Opens X in your Chrome browser (or uses an existing X tab)
2. Opens the compose dialog
3. Types your content
4. **Takes a screenshot and asks for your confirmation** before posting
5. After you approve, clicks Post
6. If there's a link reply, posts that as a follow-up reply

### What it handles
- Single posts
- Threads (adds each tweet sequentially using the + button)
- Link replies (posts the link as a reply to your main post)
- Media uploads (if you provide an image)

### Important
- You must be **logged into X in Chrome** — the skill never handles authentication
- **Always confirms before posting** — you see a screenshot first
- Requires [claude-in-chrome](https://github.com/anthropics/claude-in-chrome)

---

## /analyze — Read Analytics via Browser

**When to use**: You want real engagement data from X without manually typing numbers. Reads metrics directly from the X interface.

### Examples

**Analyze a specific post:**
```
/analyze https://x.com/username/status/123456789
```

**Analyze recent posts:**
```
/analyze recent
```

### What you get

1. Real metrics pulled from X (impressions, replies, reposts, likes, bookmarks)
2. Phoenix score analysis mapping each metric to algorithm weights
3. Key ratios: reply-to-like, bookmark-to-like, impressions/followers
4. Conversation velocity assessment (did you reply to comments?)
5. Diagnosis: why the post performed as it did
6. Recommended next content based on what's working

### Important
- Read-only — doesn't modify anything on X
- Works best on posts 24+ hours old (distribution curve completed)
- X Premium users get deeper analytics from x.com/analytics
- Requires [claude-in-chrome](https://github.com/anthropics/claude-in-chrome)

---

## /engage — Reply Management via Browser

**When to use**: You want to reply to comments on your posts to activate the 75–150× conversation velocity multiplier. This skill reads comments, prioritizes them, drafts replies, and posts them with your approval.

### Examples

**Engage with replies on a specific post:**
```
/engage https://x.com/username/status/123456789
```

**Review all recent notifications:**
```
/engage notifications
```

### How it works

1. Navigates to the post or your notifications
2. Reads all replies/mentions
3. **Prioritizes** by conversation value (questions > disagreements > agreements > spam)
4. **Drafts a reply** for each high-priority comment
5. Shows you each draft: "Replying to @user: [their comment] — [your drafted reply]"
6. **Asks for your approval** before posting each reply
7. Summarizes: N replies posted, N conversation threads created

### Reply farming mode
```
/engage farm [niche topic]
```
Searches for posts in your niche to engage with before posting your own content. Builds visibility with the algorithm.

### Important
- **Confirms before every reply** — you approve each one individually
- Drafts substantive replies, not "thanks!" (quality extends conversations)
- Requires [claude-in-chrome](https://github.com/anthropics/claude-in-chrome)

---

## Chaining Skills

Skills work best in combination. Common workflows:

**Research → Compose → Optimize:**
```
/research trending in developer tools
# Pick the best opportunity
/compose [write about the chosen topic]
/optimize [review the draft]
```

**Strategy → Schedule → Compose:**
```
/strategy plan this week's content
/schedule convert to specific times
/compose [each post from the plan]
```

**Compose → Media → Review (next day):**
```
/compose announcement for v2.0
/media what visual should I add
# Post it
# Next day:
/review how did the v2.0 announcement perform
```

**Repurpose pipeline:**
```
/thread deep dive on topic X
# After it performs well:
/repurpose [thread] → single post (highlight reel)
/repurpose [thread] → 3 different angle posts (extend the content lifecycle)
```

**Full end-to-end with browser (the power workflow):**
```
/research trending in my niche
/compose [chosen topic]
/optimize [review the draft]
/post last
# Post goes live, you get the URL
# 30-60 minutes later:
/engage [post URL]
# Reply to comments, build conversation velocity
# Next day:
/analyze [post URL]
# Real metrics → Phoenix analysis → what to post next
```
