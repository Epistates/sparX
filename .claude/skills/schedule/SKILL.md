---
name: schedule
description: Get optimal posting times and schedule content for X. Use when the user asks when to post, wants scheduling advice, or wants to queue up content at optimal times.
argument-hint: "[content type] [audience] [timezone]"
---

# Intelligent Posting Schedule

Provide data-driven posting time recommendations and help schedule content for maximum first-hour engagement velocity.

## Input

The user may ask:
- "When should I post this?"
- "Build me a weekly posting schedule"
- "What's the best time for [content type] aimed at [audience]?"
- Or provide content ready to schedule

## Process

### Step 1 — Load Timing Data
Read [../../../reference/timing.md](../../../reference/timing.md) for the complete timing reference.

### Step 2 — Gather Context

Determine:
- **Content type**: Post, thread, poll, announcement, etc.
- **Target audience**: Developers, general tech, consumers, specific niche
- **Author's timezone**: For converting recommendations
- **Posting history**: Any known patterns or constraints
- **Urgency**: Time-sensitive content vs. evergreen

### Step 3 — Generate Recommendation

**For a single post:**
- Recommend the top 3 posting windows with rationale
- Account for content type × timing matrix
- Consider the day of week
- Note: "Be available to reply for 30-60 min after posting" for every recommendation

**For a weekly schedule:**
Build a 5-day plan:

```
Monday:    [Content type] at [time] — [rationale]
Tuesday:   [Content type] at [time] — [rationale]
Wednesday: [Content type] at [time] — [rationale] ← peak day
Thursday:  [Content type] at [time] — [rationale]
Friday:    [Content type] at [time] — [rationale] (lighter content)
```

- 3-5 posts per week for quality-focused accounts
- Space posts minimum 2 hours apart on multi-post days
- Threads on Tuesday-Thursday mornings (highest dwell time)
- Lighter content (polls, questions) on Monday/Friday

**For a content calendar:**
Build a 2-4 week plan mixing:
- 1-2 threads per week (highest engagement format)
- 2-3 single posts per week (insights, tips, observations)
- 1 poll per week (engagement boost)
- Daily reply/engagement time (15-30 min)

### Step 4 — MCP Integration

If OpenTweet MCP is available:
- Offer to schedule content directly
- Use `opentweet_batch_schedule` for weekly plans
- Suggest adding high-performers to the evergreen queue

### Step 5 — Output

Present:
1. **Recommendation** with specific times (converted to user's timezone)
2. **Rationale** for each slot
3. **Engagement reminders** (reply windows, availability needed)
4. **Content type suggestions** for each slot if doing a weekly plan

## Key Rules
- Always specify timezone
- Wednesday is the peak day — schedule best content here
- Avoid weekends unless the audience is consumer/hobby
- Never schedule without a reply plan — posting and disappearing wastes the first-hour window
- If user can't be available to reply, schedule for the next available window where they can be present
