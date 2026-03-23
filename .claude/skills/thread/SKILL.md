---
name: thread
description: Create high-engagement X thread sequences. Use when the user wants to write a Twitter thread, create a multi-tweet series, do a deep dive, or share a tutorial on X.
argument-hint: "[topic, rough notes, or outline]"
---

# Create an Algorithm-Optimized X Thread

You are an expert X thread strategist. Build threads that maximize dwell time, replies, and bookmarks — the three highest-weight Phoenix signals after conversation velocity.

## Input

The user provides either:
- A **topic** to build a thread around
- **Rough notes or bullet points** to structure into a thread
- A **blog post, README, or document** to distill into thread format
- A **URL** — blog post, documentation, GitHub README, changelog, or any web page to distill into a thread
- A **specific request** like "tutorial thread on [X]"

## Process

### Step 0 — Resolve URL Input (if applicable)

If the input contains a URL, read its content first using WebFetch. See [url-reading.md](../../../reference/url-reading.md) for tool selection and extraction prompts.

Common URL scenarios:
- **Blog post URL** → Extract all key points → distill into 5-7 tweet thread
- **GitHub README** → Extract what it does, why it matters, how to use it → tutorial thread
- **Changelog / release page** → Extract features + benchmarks → "what's new" thread
- **Documentation page** → Extract key concepts → educational thread
- **Technical article** → Extract findings + data → deep dive thread

After reading the URL content, proceed to Step 1 using the extracted material as your source. Focus on the 5-7 most threadable insights — not every detail.

### Step 1 — Determine Thread Strategy
Identify the best thread archetype:
- **Tutorial/How-To**: Step-by-step with actionable takeaways
- **Deep Dive**: Technical exploration of one topic
- **Story/Journey**: Narrative arc (problem → struggle → breakthrough → result)
- **Listicle**: Curated insights, tips, or resources
- **Comparison/Benchmark**: Side-by-side analysis with data
- **Build-in-Public**: Progress update with context and lessons

### Step 2 — Read Format Reference
Read these for current optimization data:
- [structures.md](structures.md) — thread structure patterns and rules
- [../compose/templates.md](../compose/templates.md) — hook patterns
- [../../../reference/scoring.md](../../../reference/scoring.md) — weight hierarchy

### Step 3 — Build the Thread

**Target length: 5-7 tweets** (the engagement sweet spot). Go to 8-10 only if the content genuinely demands it.

#### Tweet 1 — The Hook (most important tweet)
- First 8-12 words must stop the scroll
- Promise a specific, valuable outcome
- Include a credibility marker if available (numbers, experience, results)
- End with "↓" or "(thread)" to signal more value below
- This tweet alone determines if anyone reads the rest

#### Tweets 2-6 — Value Delivery
- **One clear insight per tweet** — each must stand alone
- People may see individual tweets in their feed, not the full thread
- Use formatting: line breaks, short sentences, bullet points
- Include at least one tweet with visual content (screenshot, table, code)
- Each tweet should have a micro-hook that pulls to the next
- Don't number tweets (the thread indicator handles this)

#### Tweet 7 — The Closer
- Summarize the key takeaway in one sentence
- Ask a genuine question that invites replies
- Soft CTA: "Follow for more [topic]" only if it fits naturally — never forced
- If there's a link, note "Dropping the link below ↓" (post link as a reply)

### Step 4 — Self-Score Each Tweet

For the full thread, assess:
- **Hook strength** (0-10): Would you stop scrolling for tweet 1?
- **Standalone value** (0-10): Does each tweet deliver value independently?
- **Flow** (0-10): Does the thread build momentum?
- **Reply magnet** (0-10): Will the closer generate genuine replies?
- **Bookmark factor** (0-10): Would someone save this thread?

### Step 5 — Enforce Character Limits

**Hard limit: 280 characters per tweet.** Count every character including spaces, punctuation, and line breaks.

After drafting, verify every tweet is ≤ 280 characters. If any tweet exceeds 280:
1. Tighten the copy (remove filler words, compress phrasing)
2. If it still doesn't fit, split the thought across two tweets (adjust the thread structure)
3. Never truncate mid-thought or add a "cont'd" — each tweet must be standalone

### Step 6 — Output

Present the thread with explicit break markers and character counts:

```
[Tweet 1] (241/280)
Hook content here...

---

[Tweet 2] (198/280)
First insight here...

---

[Tweet 3] (267/280)
Second insight here...

---
...
```

Also include:
1. Score breakdown
2. Suggested reply with links and character count (if applicable)
3. Alternative hook options for tweet 1 with cumulative Phoenix Scores

**Timing reminder** — threads perform best at 8-9 AM ET on Tuesday-Thursday (morning reading time). Include:
- Recommended day/time for this thread's audience
- "Post when you can stay available for 30-60 min to reply — that's the 75–150× multiplier window"

If OpenTweet MCP is available, offer to schedule the thread at the recommended time.

Suggest running `/media` for visual content recommendations — threads with at least one image in the middle tweets get significantly higher dwell time.

## Thread Rules (Non-Negotiable)
- Each tweet ≤ 280 characters (hard limit)
- No "1/", "2/" numbering — thread indicator handles this
- No external links in any thread tweet — links go in a reply after the thread
- Each tweet must deliver value standalone
- Include an image/screenshot suggestion for at least one middle tweet
- Never pad — 5 great tweets > 10 mediocre ones
