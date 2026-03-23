---
name: setup
description: Interactively install and configure optional sparX integrations. Use when the user wants to set up Remotion video generation, OpenTweet MCP for scheduling/analytics, last30days trend research, or X API direct access.
argument-hint: "[remotion | opentweet | last30days | x-api | all]"
---

# Interactive Setup for sparX Integrations

Walk the user through setting up optional integrations that enhance sparX skills. Each integration is independent — install only what you need.

## Available Integrations

Present this menu if no specific integration is requested:

```
Which integration would you like to set up?

1. Remotion     — Programmatic video/GIF generation for posts
2. OpenTweet    — Direct posting, scheduling, analytics, voice learning via MCP
3. last30days   — Real-time trend research across X, Reddit, HN, YouTube
4. X API        — Direct X/Twitter API access for custom workflows
5. All          — Set up everything

Type a number or name to get started.
```

## Integration: Remotion

### Prerequisites Check
```bash
node --version   # 18+ required
pnpm --version   # must be available
```

### Installation Steps

**This is an interactive install — the user must run it themselves.**

Tell the user:

> Run this in your terminal:
> ```
> pnpm create video --blank marketing
> ```
>
> When prompted, answer **Yes** to all three questions:
> 1. **Continue inside existing Git repo?** → Yes
> 2. **Add TailwindCSS?** → Yes
> 3. **Add agent skills?** → Yes
>
> For the skills installer, choose:
> - **Claude Code** as the agent
> - **Project** scope
> - **Symlink** (recommended)
>
> After it finishes, run:
> ```
> cd marketing && pnpm i && pnpm run dev
> ```
> This opens the Remotion preview studio in your browser.

**Do NOT attempt to run `pnpm create video` yourself** — it's interactive and requires user input at multiple prompts.

### Post-Install

The installer creates:
- `marketing/` — Remotion project with blank canvas
- `marketing/.agents/skills/remotion-best-practices` — agent skills (symlinked to Claude Code)
- Tailwind CSS pre-configured for styling compositions

Key commands:
```bash
cd marketing
pnpm run dev              # Preview in browser (hot-reloads)
pnpm exec remotion render # Render to MP4
```

**Do NOT attempt to run `pnpm create video` yourself** — it requires interactive input (prompts for styling choice, etc.) that cannot be automated.

4. **Create X-optimized templates directory**:
```bash
mkdir -p marketing/src/templates
```

### Post-Setup

After installation, the `/media` skill will detect Remotion and offer to generate video compositions. Common workflows:

- `/compose [topic]` → draft post → `/media` → generate complementary video
- `/media benchmark animation comparing [A] vs [B]` → generates and renders
- Edit templates in `marketing/src/templates/` for recurring content

### Template Starter

Create a base dark-theme composition that matches X's aesthetic. After setup, try:
```
Create a Remotion composition for a 10-second benchmark bar race animation
with a dark background (#15202b) using X's color scheme
```

---

## Integration: OpenTweet MCP

### Prerequisites
- Node.js 18+
- X/Twitter account

### Installation Steps

1. **Create OpenTweet account**:
   Direct the user to sign up at opentweet.io (7-day free trial, $5.99/mo after)

2. **Get API key**:
   Dashboard → Developer → API Key → Copy

3. **Add MCP server to Claude Code**:
```bash
claude mcp add opentweet -- npx -y @opentweet/mcp-server
```

4. **Set API key** (add to shell profile for persistence):
```bash
echo 'export OPENTWEET_API_KEY="PASTE_KEY_HERE"' >> ~/.zshrc
source ~/.zshrc
```

5. **Verify**: Restart Claude Code and ask "What OpenTweet tools are available?"

### Post-Setup

- `/compose` and `/thread` will offer to schedule content directly
- `/review` can auto-fetch analytics
- `/schedule` can batch-schedule a week of content
- Activate **Voice Learning** in the OpenTweet dashboard to match your writing style

### Voice Learning Setup
1. Go to OpenTweet Dashboard → Settings → Voice Learning
2. Enable — it analyzes your last 10-50 tweets to build a style profile
3. Takes ~30 seconds to process
4. All AI-generated content will match your voice

---

## Integration: last30days

### Prerequisites
- OpenAI API key (for Reddit search via Responses API)
- xAI API key (for X/Twitter search via Responses API)

### Installation Steps

1. **Get API keys**:
   - OpenAI: https://platform.openai.com/api-keys
   - xAI: https://console.x.ai

2. **Install the skill**:
```bash
cd ~/.claude/skills
git clone https://github.com/mvanhorn/last30days-skill.git last30days
```

3. **Set environment variables**:
```bash
echo 'export OPENAI_API_KEY="your-openai-key"' >> ~/.zshrc
echo 'export XAI_API_KEY="your-xai-key"' >> ~/.zshrc
source ~/.zshrc
```

4. **Verify**: Restart Claude Code and run `/last30days test query`

### Post-Setup

The `/research` skill will leverage last30days for real-time data when available. Use it to:
- Find what's trending in your niche right now
- Discover what prompts and techniques people are discussing
- Surface content opportunities from across Reddit, X, HN, YouTube, and more

### Cost Awareness
- Each research query uses API credits from OpenAI and xAI
- A typical query costs $0.02-0.10 depending on depth
- Results are cached — repeated queries for the same topic don't re-query

---

## Integration: X API Direct Access

### Prerequisites
- X/Twitter account
- Developer account application

### Tier Selection

| Tier | Cost | Read | Write | Best For |
|------|------|------|-------|----------|
| Free | $0/mo | 0 | ~500 posts/mo | Posting only (16/day limit) |
| Basic | $200/mo | 15K reads | 15K writes | Analytics + posting |
| Pro | $5,000/mo | 1M reads | 300K writes | Serious automation |

**Recommendation**: Start with Free tier for posting. Use OpenTweet ($5.99/mo) instead of Basic ($200/mo) for analytics — dramatically better value.

### Installation Steps

1. **Apply for developer access**: https://developer.x.com/en/portal/dashboard

2. **Create a Project and App** in the developer portal

3. **Generate credentials**:
   - OAuth 2.0 Client ID and Secret (recommended)
   - Or OAuth 1.0a API Key + Secret + Access Token + Access Secret

4. **Install the TypeScript client**:
```bash
cd path/to/sparX
npm init -y
npm install twitter-api-v2
```

5. **Create credentials file** (NEVER commit this):
```bash
echo 'TWITTER_API_KEY=your-key
TWITTER_API_SECRET=your-secret
TWITTER_ACCESS_TOKEN=your-token
TWITTER_ACCESS_SECRET=your-token-secret' > .env
echo '.env' >> .gitignore
```

6. **Verify with a test script**:
```typescript
import { TwitterApi } from 'twitter-api-v2';

const client = new TwitterApi({
  appKey: process.env.TWITTER_API_KEY!,
  appSecret: process.env.TWITTER_API_SECRET!,
  accessToken: process.env.TWITTER_ACCESS_TOKEN!,
  accessSecret: process.env.TWITTER_ACCESS_SECRET!,
});

const me = await client.v2.me();
console.log('Connected as:', me.data.username);
```

### Post-Setup

Direct API access enables custom workflows beyond what OpenTweet provides:
- Custom analytics dashboards
- Automated posting pipelines
- Webhook-driven content triggers
- Advanced search and monitoring

---

## Verification

After setting up any integration, verify it works:

```
/compose test post about setting up sparX
```

If MCP is configured, you should see scheduling options. If Remotion is installed, the `/media` skill will offer video generation.

## Notes
- All integrations are optional — sparX works fully without any of them
- API keys are stored locally and never committed (remind user about .gitignore)
- OpenTweet is the best value for most users ($5.99/mo vs $200/mo for X Basic API)
- Remotion is free for personal use, paid for commercial ($)
