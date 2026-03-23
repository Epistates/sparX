---
name: repurpose
description: Transform content across X formats. Convert posts to threads, threads to posts, blog posts to threads, announcements to multiple angles, etc. Use when the user wants to repurpose, convert, reformat, or get more mileage from existing content.
argument-hint: "[content to repurpose] [target format]"
---

# Repurpose Content Across X Formats

Maximize content ROI by transforming a single piece of content into multiple algorithm-optimized formats for X.

## Input

The user provides:
- **Source content**: A post, thread, blog post, README, changelog, talk transcript, or any text
- **A URL** — blog post, GitHub page, documentation, article, or any web page to repurpose into X content
- **Target format** (optional): If not specified, suggest the best transformations

### URL Resolution

If the input contains a URL, read its content first using WebFetch. See [../../../reference/url-reading.md](../../../reference/url-reading.md) for tool selection and extraction prompts. Then proceed with the extracted content as your source material.

## Transformations Available

### Post → Thread
Expand a single high-performing post into a deep-dive thread:
1. Use the post's core insight as the thread hook
2. Break the supporting points into individual tweets
3. Add proof/examples that didn't fit in the original
4. Add a CTA closer
5. Read [../thread/structures.md](../thread/structures.md) for structure patterns

### Thread → Post
Distill a thread into a single punchy post:
1. Extract the single most shareable insight
2. Compress proof into one line
3. Add a hook and reply trigger
4. Good for re-posting thread content weeks later

### Blog Post / README → Thread
Transform long-form content into X threads:
1. Identify the 5-7 most compelling points
2. Lead with the most surprising finding
3. Translate written style to X conversational style
4. Add visual suggestions for screenshots from the content
5. Remove all links (save for reply)

### Changelog / Release → Announcement Post
Transform a technical changelog into an engaging announcement:
1. Lead with the user benefit, not the feature name
2. Add a specific benchmark or comparison
3. Frame in terms of the audience's workflow
4. Remove internal jargon
5. Read [../compose/templates.md](../compose/templates.md) for announcement templates

### Single Insight → Multiple Angles
Take one core idea and produce 3-5 different posts, each with a unique angle:
1. **The insight** (straight delivery)
2. **The contrarian** (frame as challenging conventional wisdom)
3. **The question** (turn it into a discussion prompt)
4. **The tip** (frame as actionable advice)
5. **The story** (frame as a personal experience)

### Video/Demo Script → Post + Thread
Create both a short post and a companion thread from video content:
1. Post: Hook + key result + "full breakdown below"
2. Thread: Step-by-step walkthrough of what the video shows
3. Suggest timestamps for key moments if applicable

## Process

### Step 1 — Analyze Source Content
- What is the core message?
- What are the supporting points?
- What proof/data exists?
- What is the target audience?

### Step 2 — Select Transformations
If the user specified a target format, use that. Otherwise, recommend the 2-3 most valuable transformations based on the source content.

### Step 3 — Execute Each Transformation
Apply the relevant transformation rules above. For each output:
- Apply Phoenix scoring principles (read CLAUDE.md for hierarchy)
- Run through the optimization checklist mentally
- Ensure each piece stands alone (don't assume the reader saw the original)

### Step 4 — Enforce Character Limits

**Hard limit: 280 characters per tweet.** Every output must include character counts.

- Single posts: show `(count/280)` — tighten if over
- Threads: show `[Tweet N] (count/280)` with `---` separators — each tweet must be ≤ 280
- Link replies: show count separately

### Step 5 — Output
For each transformation, present:
1. The format and rationale
2. The complete content with character counts per tweet (ready to copy-paste)
3. Phoenix Score for each piece
4. Suggested posting schedule (stagger different formats across days, with specific day/time from `reference/timing.md`)
5. Brief note on which audience segment each angle targets
6. Timing reminder: "Post when you can stay available for 30-60 min to reply — that's the 75–150× multiplier window"

## Rules
- Each repurposed piece must stand alone — don't reference the original
- Vary hooks across formats (don't reuse the same opening)
- Space repurposed content at least 2-3 days apart
- The thread version should add value beyond the post version (not just longer)
- Preserve the author's voice across all transformations
