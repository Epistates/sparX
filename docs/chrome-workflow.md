# Browser Workflow — End-to-End with claude-in-chrome

## Overview

Three skills connect sparX directly to X through your Chrome browser:

| Skill | Direction | Confirmation | Requires Auth |
|-------|-----------|-------------|---------------|
| `/post` | sparX → X | Yes, before every post | Must be logged in |
| `/analyze` | X → sparX | No (read-only) | Must be logged in |
| `/engage` | Both | Yes, before every reply | Must be logged in |

**All three require [claude-in-chrome](https://github.com/anthropics/claude-in-chrome).** You must be logged into X in your Chrome browser — the skills never handle passwords or authentication.

## The Full Loop

```
/compose [topic]           Draft an optimized post
       ↓
/post last                 Publish to X via browser (with confirmation)
       ↓
       ⏳ 30-60 minutes
       ↓
/engage [post URL]         Reply to comments (75-150× multiplier)
       ↓
       ⏳ 24 hours
       ↓
/analyze [post URL]        Read real metrics, run Phoenix analysis
       ↓
/compose [next topic]      Informed by what worked → repeat
```

This loop is the core sparX workflow. Each cycle teaches you what resonates with your audience, and the skills get better at optimizing for your specific niche.

## /post — Publishing

### Single Post
```
/compose announcement: our CLI now deploys in 3 seconds
# Claude drafts an optimized post
/post last
```

What happens:
1. Claude opens X in Chrome (or uses an existing tab)
2. Navigates to x.com/compose/post
3. Types your content into the compose box
4. **Takes a screenshot** showing exactly what will be posted
5. **Asks: "Should I post this?"**
6. Only after you say yes, clicks Post
7. If there's a link reply, posts that as a follow-up

### Thread
```
/thread deep dive on our new caching architecture
# Claude drafts a 7-tweet thread
/post last
```

What happens:
1. Opens compose, types tweet 1
2. Clicks the + button to add each subsequent tweet
3. **Screenshots the full thread** for your review
4. **Asks: "Post this [N]-tweet thread?"**
5. After approval, clicks "Post all"

### With Media
If your post includes an image reference, `/post` will attempt to upload it via the media button in the compose dialog.

## /analyze — Reading Metrics

### Specific Post
```
/analyze https://x.com/yourname/status/123456789
```

What happens:
1. Navigates to the post in Chrome
2. Reads engagement metrics (views, replies, reposts, likes, bookmarks)
3. Runs Phoenix score analysis:
   - Maps each metric to algorithm weights
   - Calculates key ratios (reply-to-like, bookmark-to-like)
   - Assesses conversation velocity
4. Produces diagnosis and recommendations

### Recent Posts
```
/analyze recent
```

What happens:
1. Navigates to your X profile
2. Reads metrics from your last 3-5 posts
3. Ranks them by engagement rate
4. Identifies patterns (what formats, topics, times work best)
5. Recommends what to post next

### Analytics Dashboard (Premium)
```
/analyze dashboard
```

If you have X Premium, navigates to x.com/analytics for deeper data: impressions over time, follower growth, and top-performing content.

## /engage — Reply Management

### On a Specific Post
```
/engage https://x.com/yourname/status/123456789
```

What happens:
1. Navigates to the post
2. Reads all replies
3. Prioritizes by conversation value:
   - **High**: Questions, substantive disagreements, replies from larger accounts
   - **Medium**: Shared experiences, additional insights
   - **Low**: Simple agreement, spam
4. For each high-priority reply, drafts a response:
   ```
   Replying to @developer_jane ("Is this faster than the Go implementation?"):
   "Benchmarked against the Go version last week — 1.4× faster on M3.
    The Metal kernels skip the CGo overhead entirely. What workload are you running?"

   Post this reply? (yes / edit / skip)
   ```
5. After your approval, posts each reply
6. Summarizes: "Posted 5 replies, created 5 conversation threads (75–150× multiplier each)"

### Notifications Mode
```
/engage notifications
```

Reviews all recent notifications — replies to your posts, mentions, quote tweets. Prioritizes the most valuable engagement opportunities across all your recent content.

### Reply Farming
```
/engage farm developer tools
```

Before posting your own content, engage in your niche's conversations:
1. Searches X for recent posts about the topic
2. Finds posts with active engagement you could add value to
3. Drafts thoughtful replies (no self-promotion)
4. Posts with your approval

This warms up the algorithm's model of your interests and makes you visible to potential audience members before you publish.

## Timing Your Workflow

### Posting Day (30-45 min total)

| Time | Action | Duration |
|------|--------|----------|
| Before posting | `/engage farm [niche]` — warm up with 10 replies | 10 min |
| Post time | `/compose` → `/post last` | 5 min |
| +30 min | `/engage [post URL]` — first reply wave | 10 min |
| +60 min | `/engage [post URL]` — second reply wave | 5 min |

### Review Day (10 min)

| Action | Duration |
|--------|----------|
| `/analyze recent` — check last 3-5 posts | 5 min |
| `/compose` next post based on findings | 5 min |

## Safety & Confirmation

Every skill that writes to X requires explicit confirmation:

- `/post` screenshots the compose dialog and asks before publishing
- `/engage` shows each drafted reply and asks before posting
- `/analyze` is read-only — no confirmation needed

If anything looks wrong (wrong account, unexpected page state, X UI change), the skills stop and tell you what happened rather than proceeding blindly.

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "Not logged in" | Log into X in Chrome manually, then retry |
| Can't find compose button | Skill will try navigating to x.com/compose/post directly |
| Metrics not loading | Wait 3-5 seconds — X lazy-loads engagement counts |
| Reply box not found | Click on the comment first to expand it, then retry |
| X shows error page | Wait 30 seconds, refresh, retry once |
| claude-in-chrome not responding | Check the extension is installed and enabled in Chrome |
