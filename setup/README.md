# sparX Setup Guide

## Quick Start

sparX works out of the box with zero configuration. Open Claude Code in the `sparX/` directory and use any skill:

```bash
cd path/to/sparX
claude

# Then use any skill:
/compose My new feature ships 3× faster batch processing
/thread 5 things I learned building LLM infrastructure
/optimize [paste your draft]
/hooks local AI inference on consumer hardware
/schedule tech audience, EST timezone
/research developer tools trending topics
/review [paste engagement data]
/strategy rust developer tools, 500 followers, growth mode
/repurpose [paste blog post]
```

## Optional: OpenTweet MCP Integration

OpenTweet adds direct posting, scheduling, analytics, and voice learning to your skills.

### Setup

1. **Create an OpenTweet account**: https://opentweet.io (7-day free trial, then $5.99/mo)

2. **Get your API key**: Dashboard → Developer → API Key

3. **Add MCP server to Claude Code**:
```bash
claude mcp add opentweet -- npx -y @opentweet/mcp-server
```

4. **Set your API key**:
```bash
export OPENTWEET_API_KEY="your-key-here"
```
Add to your shell profile (~/.zshrc) for persistence.

5. **Verify**: Start Claude Code and ask "What OpenTweet tools are available?"

### What MCP Unlocks

| Feature | Without MCP | With MCP |
|---------|------------|----------|
| Drafting posts | Yes | Yes |
| Scoring/optimization | Yes | Yes |
| Scheduling | Manual copy-paste | Direct scheduling |
| Analytics | Manual input | Auto-fetch from X |
| Voice learning | N/A | Learns your writing style |
| Evergreen queue | N/A | Auto-recycles top performers |
| Batch scheduling | N/A | Schedule a week at once |

### MCP Tools Available

Once configured, these OpenTweet tools become available:
- `opentweet_create_tweet` — Post immediately
- `opentweet_schedule_tweet` — Schedule for specific time
- `opentweet_create_thread` — Post a thread
- `opentweet_batch_schedule` — Schedule multiple posts
- `opentweet_get_analytics` — Fetch engagement data
- `opentweet_evergreen_add` — Add to recycling queue
- `opentweet_voice_learn` — Train voice model on your existing tweets

## Optional: Remotion Video Generation

For creating programmatic video content (demos, benchmark visualizations, animated announcements):

### Setup

1. **Install Remotion skills**:
```bash
# Agent skills are installed by the interactive installer above — no separate step needed
```

2. **Create a Remotion project** (if you want to generate video):
```bash
pnpm create video --blank
```

3. **Use with sparX**: When composing posts, you can ask Claude to generate a short video clip:
```
/compose announcement for v2.0 — include a 15-second benchmark animation
```

### When to Use Video

Per the algorithm data:
- Text outperforms video by ~30% on X (unique to this platform)
- **Best combo**: Text post + short video/GIF attached (maximizes both text scoring and dwell time)
- Keep videos under 45 seconds for high completion rates
- Screen recordings and benchmark animations perform best in tech niches

## Optional: Trend Research Enhancement

For deeper trend research, install the last30days skill:

### Setup

1. **Get API keys**:
   - OpenAI API key (for Reddit search): https://platform.openai.com
   - xAI API key (for X search): https://console.x.ai

2. **Install the skill**:
```bash
cd ~/.claude/skills
git clone https://github.com/mvanhorn/last30days-skill.git last30days
```

3. **Set environment variables**:
```bash
export OPENAI_API_KEY="your-key"
export XAI_API_KEY="your-key"
```

4. **Use with sparX**: The `/research` skill will automatically leverage last30days when available for real-time trend data across Reddit, X, Hacker News, YouTube, and more.

## X API Direct Access (Advanced)

For developers who want to build custom integrations:

### Free Tier ($0/mo)
- ~500 posts/month (~16-17/day)
- Write-only (posting only)
- Sufficient for most individual creators

### Basic Tier ($200/mo)
- 15,000 tweet reads
- Read + Write access
- Needed for analytics without OpenTweet

### Setup
1. Apply for developer access: https://developer.x.com
2. Create a project and app
3. Generate OAuth 2.0 credentials
4. Use `twitter-api-v2` npm package for TypeScript integration

## File Structure

```
sparX/
├── .claude/
│   ├── skills/
│   │   ├── compose/        — /compose: Draft optimized posts
│   │   ├── thread/         — /thread: Create threads
│   │   ├── optimize/       — /optimize: Score & rewrite drafts
│   │   ├── hooks/          — /hooks: Generate opening lines
│   │   ├── schedule/       — /schedule: Posting times
│   │   ├── research/       — /research: Topic research
│   │   ├── review/         — /review: Performance analysis
│   │   ├── strategy/       — /strategy: Content planning
│   │   ├── repurpose/      — /repurpose: Format transformation
│   │   ├── media/          — /media: Visual content strategy
│   │   ├── post/           — /post: Publish to X via browser
│   │   ├── analyze/        — /analyze: Read analytics via browser
│   │   ├── engage/         — /engage: Reply management via browser
│   │   └── setup/          — /setup: Integration installation
│   └── agents/
│       └── scorer.md       — Phoenix score simulation agent
├── reference/
│   ├── algorithm.md        — Phoenix pipeline deep dive
│   ├── scoring.md          — Signal weights & multipliers
│   ├── content-formats.md  — Format-specific guidance
│   ├── timing.md           — Optimal posting times
│   └── penalties.md        — What kills reach
├── docs/
│   ├── getting-started.md  — Quick start guide
│   ├── skills-guide.md     — Detailed skill usage & examples
│   ├── algorithm-guide.md  — Creator-friendly algorithm explainer
│   ├── media-strategy.md   — Visual content strategy
│   ├── integrations.md     — Optional integration setup
│   └── playbooks.md        — End-to-end workflow walkthroughs
├── setup/
│   └── README.md           — This file
└── CLAUDE.md               — Core project context (always loaded)
```
