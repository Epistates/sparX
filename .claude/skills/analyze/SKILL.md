---
name: analyze
description: Read real engagement analytics from X via browser automation. Use when the user wants to check how their posts are performing, review analytics, or get real engagement data without manual entry. Requires claude-in-chrome.
argument-hint: "[post URL or 'recent' for latest posts]"
allowed-tools: mcp__claude-in-chrome__tabs_context_mcp, mcp__claude-in-chrome__tabs_create_mcp, mcp__claude-in-chrome__navigate, mcp__claude-in-chrome__read_page, mcp__claude-in-chrome__find, mcp__claude-in-chrome__computer, mcp__claude-in-chrome__javascript_tool, mcp__claude-in-chrome__get_page_text, Read, Grep, Glob
---

# Analyze X Post Performance via Browser

Read real engagement data directly from X's interface and run Phoenix scoring analysis — no manual data entry needed.

## Input

The user provides one of:
- **A post URL** — analyze that specific post
- **"recent"** — analyze the most recent posts from their profile
- **Their X username** — navigate to their profile to analyze recent posts
- **Nothing** — ask what they want to analyze

## Process

### Step 1 — Get Browser Context

```
mcp__claude-in-chrome__tabs_context_mcp(createIfEmpty: true)
```

Create a new tab or reuse an existing x.com tab.

### Step 2 — Navigate to the Content

**For a specific post URL:**
```
mcp__claude-in-chrome__navigate(url: "<post_url>", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

**For recent posts (navigate to profile):**
```
mcp__claude-in-chrome__navigate(url: "https://x.com", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 2, tabId: <tab>)
```

Find and click on the user's profile:
```
mcp__claude-in-chrome__find(query: "profile link or avatar in sidebar", tabId: <tab>)
```

**Verify logged-in state** — take a screenshot:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

If not logged in, stop and tell the user to log in first.

### Step 3 — Read Post Metrics

#### For a specific post:

Navigate to the post and read its engagement metrics. X shows metrics below each post (replies, reposts, likes, bookmarks, views).

1. Read the page to find metric elements:
```
mcp__claude-in-chrome__read_page(tabId: <tab>, filter: "all", depth: 10)
```

2. Or use JavaScript to extract metrics from the post detail page:
```
mcp__claude-in-chrome__javascript_tool(action: "javascript_exec", text: "
  // Extract metrics from post detail page
  const metrics = {};
  const groups = document.querySelectorAll('[role=\"group\"]');
  const ariaLabels = Array.from(document.querySelectorAll('[aria-label]'))
    .map(el => el.getAttribute('aria-label'))
    .filter(label => label && (
      label.includes('repl') || label.includes('repost') ||
      label.includes('like') || label.includes('bookmark') ||
      label.includes('view') || label.includes('impression')
    ));
  JSON.stringify(ariaLabels);
", tabId: <tab>)
```

3. If metrics aren't visible or parseable, try clicking the post's analytics/stats icon:
```
mcp__claude-in-chrome__find(query: "view post analytics or post stats icon", tabId: <tab>)
```

4. Take a screenshot of the metrics for reference:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

#### For recent posts on profile:

1. Read the profile timeline to get recent posts:
```
mcp__claude-in-chrome__get_page_text(tabId: <tab>)
```

2. For each of the last 3-5 posts, extract visible metrics (views, replies, reposts, likes, bookmarks).

3. Use JavaScript to collect metrics from timeline items:
```
mcp__claude-in-chrome__javascript_tool(action: "javascript_exec", text: "
  const articles = document.querySelectorAll('article');
  const posts = Array.from(articles).slice(0, 5).map((article, i) => {
    const text = article.innerText.substring(0, 100);
    const ariaLabels = Array.from(article.querySelectorAll('[aria-label]'))
      .map(el => el.getAttribute('aria-label'))
      .filter(label => label && /\\d/.test(label));
    return { index: i, preview: text, metrics: ariaLabels };
  });
  JSON.stringify(posts, null, 2);
", tabId: <tab>)
```

4. Scroll down if needed to load more posts:
```
mcp__claude-in-chrome__computer(action: "scroll", coordinate: [640, 400], scroll_direction: "down", scroll_amount: 3, tabId: <tab>)
```

### Step 4 — Access Post Analytics Detail (if available)

X Premium users have detailed analytics. Try navigating to the analytics dashboard:

```
mcp__claude-in-chrome__navigate(url: "https://x.com/analytics", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

If analytics is available, extract:
- Impressions over time
- Engagement rate
- Top performing posts
- Follower growth

If not available (not Premium), work with the per-post metrics gathered in Step 3.

### Step 5 — Phoenix Score Analysis

With the collected metrics, run the full analysis from the `/review` skill framework:

Read reference material:
- [../../reference/scoring.md](../../reference/scoring.md)

For each post analyzed, produce:

**Performance Table:**

| Metric | Value | Algorithm Interpretation |
|--------|-------|------------------------|
| Views/Impressions | ? | Distribution reach |
| Replies | ? | 13–27× weight |
| Reposts | ? | ~20× weight |
| Likes | ? | 1× baseline |
| Bookmarks | ? | ~10× weight |
| Engagement rate | ? | (total engagements / impressions) × 100 |

**Key Ratios:**
- **Impressions / followers**: >2× means algorithm is amplifying
- **Reply-to-like ratio**: >0.15 = strong conversation driver
- **Bookmark-to-like ratio**: >0.10 = high-quality content signal

**Conversation Velocity Assessment:**
- Did the author reply to comments? (check reply threads on the post)
- How many author reply threads exist?
- Were replies substantive or just "thanks"?

**Diagnosis:**
- Why did this post perform as it did?
- What specific elements drove engagement (or didn't)?
- What would you change for next time?

### Step 6 — Comparative Analysis (if multiple posts)

If analyzing multiple recent posts, produce:

1. **Ranked performance table** — posts sorted by engagement rate
2. **Pattern identification** — what formats/topics/times performed best
3. **Trend line** — are things improving, declining, or flat?
4. **Top recommendation** — one specific action to improve the next post

### Step 7 — Output

Present:
1. **Raw metrics** collected from X (with screenshot reference)
2. **Phoenix score analysis** per post
3. **Key ratios** with benchmarks
4. **Diagnosis** — why each post performed as it did
5. **Recommendations** — specific actions for the next post
6. **Suggested next content** — based on what's working, suggest the next post topic/format

Offer to run `/compose` on the suggested next content.

## Tips

- X shows different metric granularity based on Premium status
- The analytics page (x.com/analytics) requires Premium
- Per-post metrics (reply/repost/like/bookmark counts) are visible to everyone
- View counts are visible on most posts
- For the most accurate data, analyze posts that are at least 24 hours old (let the distribution curve complete)

## Troubleshooting

- **Metrics not loading**: Wait longer (3-5 seconds), X lazy-loads engagement counts
- **Can't find metrics**: Take a screenshot and visually identify where numbers appear
- **Analytics page redirects**: User may not have Premium — fall back to per-post metrics
- **JavaScript extraction fails**: Fall back to `read_page` with `filter: "all"` and search for numeric elements
- **Rate limiting**: If X shows "something went wrong", wait 30 seconds and retry once
