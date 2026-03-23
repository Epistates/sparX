---
name: test
description: Verify sparX setup is working correctly. Use when the user wants to check their installation, test skills, or troubleshoot setup issues.
argument-hint: "[all | skills | browser | remotion]"
---

# Test sparX Setup

Quick verification that everything is wired up correctly. Runs a series of checks and reports status.

## Process

Run all checks (or a subset if the user specifies). Present results as a checklist.

### 1. Core Setup

```
✅ / ❌  CLAUDE.md loaded — check that Phoenix algorithm context is available
✅ / ❌  Reference docs exist — check reference/scoring.md, reference/penalties.md, etc.
✅ / ❌  Skills discovered — list all skills Claude can see (should be 15)
```

**How to verify:**
- Read `CLAUDE.md` and confirm it contains "Phoenix Algorithm"
- Check that `reference/scoring.md` exists
- List available skills and count them

### 2. Skill Smoke Test

Run a quick `/hooks` generation to prove the content pipeline works:

```
Generate 3 hooks for: "a new open-source developer tool"
```

**Pass criteria:**
- Produces 3 distinct hooks
- Each is under 280 characters
- No engagement bait phrases
- Phoenix Score block appears

```
✅ / ❌  Skill pipeline — /hooks produced scored output
```

### 3. Remotion (optional)

Check if the Remotion project exists:

```bash
ls marketing/remotion.config.ts 2>/dev/null
```

```
✅ / ❌  Remotion project — marketing/ directory with remotion.config.ts
✅ / ❌  Remotion skills — marketing/.claude/skills/remotion-best-practices/SKILL.md
✅ / ❌  Tailwind configured — marketing/tailwind.config.ts or similar
```

If not installed:
```
⬜  Remotion not installed — run: pnpm create video --blank marketing
```

### 4. Browser Integration (optional)

Check if claude-in-chrome is available by attempting to get tab context:

```
mcp__claude-in-chrome__tabs_context_mcp()
```

```
✅ / ❌  Chrome connection — claude-in-chrome responds
✅ / ❌  Can create tab — tabs_create_mcp succeeds
```

If not available:
```
⬜  Chrome not connected — install claude-in-chrome extension
```

### 5. Optional Integrations

Check environment for optional integrations:

```
✅ / ❌ / ⬜  OpenTweet MCP — check if opentweet tools are available
✅ / ❌ / ⬜  last30days — check if ~/.claude/skills/last30days/SKILL.md exists
✅ / ❌ / ⬜  X API — check if TWITTER_API_KEY env var is set
```

### Output

Present a summary dashboard:

```
sparX Setup Report
══════════════════

Core
  ✅ CLAUDE.md loaded (Phoenix algorithm context)
  ✅ Reference docs (6/6 files)
  ✅ Skills discovered (15/15)
  ✅ Skill pipeline (hooks generated successfully)

Remotion
  ✅ Project exists (marketing/)
  ✅ Agent skills installed
  ✅ Tailwind configured

Browser (claude-in-chrome)
  ✅ Chrome connected
  ✅ Tab creation works

Optional Integrations
  ⬜ OpenTweet MCP (not configured — run /setup opentweet)
  ⬜ last30days (not installed — run /setup last30days)
  ⬜ X API (not configured — run /setup x-api)

Status: Ready to go! Core + Remotion + Browser all working.
```

Use ✅ for pass, ❌ for fail (with fix suggestion), ⬜ for not installed (optional).
