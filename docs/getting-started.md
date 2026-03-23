# Getting Started with sparX

## Your First Post in 5 Minutes

### Step 1: Open Claude Code in the sparX directory

```bash
cd path/to/sparX
claude
```

Claude Code automatically loads sparX's CLAUDE.md context and all 11 skills.

### Step 2: Draft your first post

```
/compose I just shipped a new feature that makes batch processing 3× faster
```

Claude will:
1. Analyze your topic against the Phoenix algorithm scoring model
2. Draft an optimized post with a strong hook, proof points, and reply trigger
3. Score the draft against engagement signals (dwell, reply potential, bookmark appeal)
4. Suggest alternative hooks and a follow-up reply for links

### Step 3: Optimize (optional)

If you already have a draft you want to improve:

```
/optimize We just released v2.0 with faster processing. Check it out: https://example.com
```

Claude will identify issues (link in body = 30-50% reach penalty), score the draft, and rewrite it for maximum algorithm performance.

### Step 4: Post it

**Without MCP**: Copy the optimized post and paste into X directly.

**With OpenTweet MCP**: Claude will offer to schedule it at the optimal time. Run `/setup opentweet` to set this up.

---

## Your First Thread

```
/thread 5 lessons I learned building a high-performance Rust library
```

Claude builds a 5-7 tweet thread with:
- A scroll-stopping hook (tweet 1)
- One clear insight per tweet, each standalone
- Visual content suggestions for middle tweets
- A reply-triggering closer

---

## Your First Content Strategy

```
/strategy developer tools niche, 200 followers, want to reach 1K in 90 days
```

Claude produces:
- Account stage assessment
- 3-5 content pillars for your niche
- Weekly posting calendar with specific times
- Growth tactics tailored to your stage
- 10 specific post ideas to start with

---

## Skill Cheat Sheet

| You want to... | Run... |
|-----------------|--------|
| Write a tweet | `/compose [topic or rough draft]` |
| Write a thread | `/thread [topic or outline]` |
| Improve a draft | `/optimize [your draft]` |
| Get hook ideas | `/hooks [topic]` |
| Know when to post | `/schedule [audience] [timezone]` |
| Find content ideas | `/research [niche topic]` |
| Review post performance | `/review [data or URL]` |
| Plan a content calendar | `/strategy [niche] [goals]` |
| Reformat content | `/repurpose [content] [target format]` |
| Add visuals to a post | `/media [post content]` |
| Publish to X via browser | `/post [content]` or `/post last` |
| Read real analytics from X | `/analyze recent` or `/analyze [post URL]` |
| Reply to comments via browser | `/engage [post URL]` or `/engage notifications` |
| Set up integrations | `/setup [remotion\|opentweet\|last30days\|x-api]` |

---

## What Happens Behind the Scenes

When you invoke a skill, Claude:

1. **Loads the CLAUDE.md** — Core algorithm context is always present (Phoenix scoring weights, critical rules, content standards)
2. **Reads the skill's SKILL.md** — Step-by-step instructions for the specific task
3. **Progressively loads reference docs** — Deep algorithm data from `reference/` only when needed (scoring weights, timing data, penalty lists)
4. **Reads supporting files** — Templates, patterns, examples, checklists specific to the skill
5. **Executes the workflow** — Follows the skill's process to produce optimized output

This progressive disclosure keeps context efficient while giving Claude access to deep reference material when it matters.

---

## Next Steps

- **Read the [Skills Guide](skills-guide.md)** for detailed usage of each skill with real examples
- **Read the [Algorithm Guide](algorithm-guide.md)** to understand why the optimizations work
- **Read the [Media Strategy](media-strategy.md)** for visual content guidance
- **Run `/setup`** to install optional integrations (Remotion, OpenTweet, trend research)
- **Start posting** — consistency matters more than perfection
