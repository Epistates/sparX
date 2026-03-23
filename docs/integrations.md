# Integrations Guide

sparX works standalone with zero configuration. Optional integrations add superpowers.

## Quick Comparison

| Integration | Cost | What It Adds | Setup Time |
|------------|------|-------------|------------|
| **Remotion** | Free (personal) | Programmatic video generation | 10 min |
| **OpenTweet MCP** | $5.99/mo | Scheduling, analytics, voice learning, evergreen queue | 5 min |
| **last30days** | ~$0.02-0.10/query | Real-time trend research across 10+ platforms | 5 min |
| **X API (Free)** | $0/mo | Direct posting (~16 posts/day) | 15 min |
| **X API (Basic)** | $200/mo | Read + write + analytics | 15 min |

## claude-in-chrome — Browser Automation

### What it does
Connects Claude Code directly to your Chrome browser. Enables `/post`, `/analyze`, and `/engage` skills.

### Login & Session Persistence
- **You must be logged into X in Chrome.** The skills never handle passwords.
- Chrome maintains your X session through normal browser cookies — as long as you stay logged in to X in Chrome, the skills work.
- If your session expires (X logs you out), the skills will detect this, screenshot the login page, and ask you to log in manually.
- There is no special "automation profile" — it uses your regular Chrome browser and session.

### Automation Detection
- X may detect automated behavior (rapid clicks, repetitive patterns, unusual timing)
- sparX includes rate-limit pauses (3-5 seconds between actions) to minimize detection risk
- If X presents a CAPTCHA or verification challenge, the skills stop immediately and inform you
- **Dry-run mode**: Add "dry run" to any `/post` or `/engage` command to test the full flow without actually posting

### Setup
Install the [claude-in-chrome](https://github.com/anthropics/claude-in-chrome) browser extension. No API keys needed — it connects Claude Code to your browser directly.

Run `/test browser` to verify the connection works.

---

## Remotion — Programmatic Video

### What it does
Generates video content from React code. Claude Code + Remotion Agent Skills lets you describe videos in natural language and Claude writes the React components.

### What it enables
- `/media` skill can generate and render video compositions
- Templated benchmark animations, metrics dashboards, code reveals
- Consistent branded video across all posts
- Batch video generation from data

### Setup
```
/setup remotion
```

Or manually:
```bash
# Create video project (interactive — say Yes to all 3 prompts: Git repo, Tailwind, agent skills)
cd path/to/sparX
pnpm create video --blank marketing

# Install dependencies and verify
cd marketing && pnpm i && pnpm run dev
```

The installer handles everything: Remotion, Tailwind, and agent skills (choose Claude Code, Project scope, Symlink).

### Usage examples
```
/media create a 10-second benchmark race showing Tool A at 2.3s vs Tool B at 5.1s

/media generate a code reveal animation for this Python snippet

/media create a weekly metrics template showing follower growth, impressions, and engagement rate
```

### Cost
- Free for personal/open source use
- Company license required for commercial use ($$$)
- No per-render costs — runs locally

---

## OpenTweet MCP — Scheduling & Analytics

### What it does
Connects Claude Code directly to X/Twitter through an MCP server. Post, schedule, analyze, and manage content without leaving the terminal.

### What it enables
- `/compose` and `/thread` offer to schedule content at optimal times
- `/review` auto-fetches analytics data
- `/schedule` batch-schedules a week of content
- Voice Learning matches AI-generated content to your writing style
- Evergreen queue auto-recycles your best-performing content
- GitHub/RSS/Stripe connectors auto-generate posts from events

### Setup
```
/setup opentweet
```

Or manually:
```bash
# Add MCP server
claude mcp add opentweet -- npx -y @opentweet/mcp-server

# Set API key (get from opentweet.io dashboard)
echo 'export OPENTWEET_API_KEY="your-key"' >> ~/.zshrc
source ~/.zshrc
```

### Available MCP tools (18 total)
| Tool | Purpose |
|------|---------|
| `opentweet_create_tweet` | Post immediately |
| `opentweet_schedule_tweet` | Schedule for specific time |
| `opentweet_create_thread` | Post a thread |
| `opentweet_batch_schedule` | Schedule multiple posts at once |
| `opentweet_get_analytics` | Fetch engagement data |
| `opentweet_evergreen_add` | Add to auto-recycling queue |
| `opentweet_voice_learn` | Train on your writing style |

### Voice Learning
After connecting your account:
1. Dashboard → Settings → Voice Learning → Enable
2. Analyzes your last 10-50 tweets (~30 seconds)
3. Learns sentence structure, vocabulary, tone, humor, emoji patterns
4. All AI-generated content matches your voice

### Cost
- 7-day free trial
- $5.99/month (Pro plan: 10 evergreen tweets, 2 daily auto-posts)
- Advanced plan: 999 evergreen tweets, 10 daily auto-posts

### Why OpenTweet vs. X API Basic ($200/mo)
OpenTweet at $5.99/mo gives you scheduling, analytics, voice learning, connectors, and evergreen queue. X API Basic at $200/mo gives you raw API access with 15K reads. For most creators, OpenTweet is dramatically better value.

---

## last30days — Real-Time Trend Research

### What it does
A Claude Code skill that researches any topic across Reddit, X, Hacker News, YouTube, Bluesky, TikTok, Polymarket, and the web. Enforces a 30-day recency window and produces actionable content briefs.

### What it enables
- `/research` skill gets real-time data on what people are actually discussing
- Surface trending topics, viral content, and community debates
- Discover content opportunities based on real conversations
- Find the exact language and framing your audience uses

### Setup
```
/setup last30days
```

Or manually:
```bash
# Install the skill
cd ~/.claude/skills
git clone https://github.com/mvanhorn/last30days-skill.git last30days

# Set API keys
echo 'export OPENAI_API_KEY="your-key"' >> ~/.zshrc  # For Reddit search
echo 'export XAI_API_KEY="your-key"' >> ~/.zshrc      # For X search
source ~/.zshrc
```

### Usage
```
/last30days Rust developer tools

/last30days local LLM inference Apple Silicon

/last30days what are people saying about [your product/niche]
```

### Cost
- ~$0.02-0.10 per research query (API credits)
- Requires OpenAI API key ($) and xAI API key ($)
- Results cached — repeat queries don't re-charge

---

## X API — Direct Access

### What it does
Direct access to X's official API for posting, reading, and custom automation.

### Tiers

**Free ($0/mo)**
- ~500 posts/month (16-17/day)
- Write-only (posting, no reading)
- Sufficient for individual creators
- No analytics access

**Basic ($200/mo)**
- 15,000 tweet reads
- Read + write access
- Needed for custom analytics (but OpenTweet is better value for this)

**Pro ($5,000/mo)**
- 1 million post reads
- Full-archive search
- Real-time filtering
- For serious automation and research

### Setup
```
/setup x-api
```

### When you need direct API access
- Custom automation beyond OpenTweet's capabilities
- Building a product that integrates with X
- Advanced search and monitoring
- Webhook-driven posting pipelines

### Recommended library
```bash
npm install twitter-api-v2
```

`twitter-api-v2` is the gold standard Node.js/TypeScript client:
- Strongly typed
- Full v1.1 and v2 support
- Media upload helpers
- Automatic pagination
- Stream support

---

## Integration Decision Tree

```
Do you want to schedule posts?
├── Yes → Install OpenTweet MCP ($5.99/mo)
└── No → Copy-paste from Claude is fine

Do you want video content?
├── Recurring/templated → Install Remotion
├── One-off screen recordings → Use QuickTime/OBS (no integration needed)
└── No video → Screenshots via macOS tools

Do you want trend research?
├── Yes → Install last30days (~$0.05/query)
└── No → /research skill uses web search (free, less depth)

Do you need raw API access?
├── Just posting → X API Free tier ($0)
├── Analytics + posting → OpenTweet ($5.99) or X Basic ($200)
└── Custom automation → X API Basic or Pro
```
