---
name: engage
description: Manage replies and conversations on X via browser automation. Surfaces comments worth replying to, drafts optimized replies, and posts them with your approval. Activates the 75-150x conversation velocity multiplier. Requires claude-in-chrome.
argument-hint: "[post URL to engage on, or 'notifications' for recent mentions]"
allowed-tools: mcp__claude-in-chrome__tabs_context_mcp, mcp__claude-in-chrome__tabs_create_mcp, mcp__claude-in-chrome__navigate, mcp__claude-in-chrome__read_page, mcp__claude-in-chrome__find, mcp__claude-in-chrome__form_input, mcp__claude-in-chrome__computer, mcp__claude-in-chrome__javascript_tool, mcp__claude-in-chrome__get_page_text, AskUserQuestion, Read, Grep, Glob
---

# Engage — Conversation Velocity via Browser

Manage replies on your X posts to activate the 75–150× author reply conversation multiplier. This skill surfaces comments worth replying to, drafts high-quality replies, and posts them with your approval.

**Why this matters:** Author replies to comments create conversation threads — the single highest-weight signal in the Phoenix algorithm at 75–150× a like. A post with 5 author reply threads massively outperforms one with none.

## Input

The user provides one of:
- **A post URL** — engage with replies on that specific post
- **"notifications"** — review recent mentions and replies across all posts
- **"replies"** — same as notifications, focused on reply tab
- **Nothing** — defaults to notifications

## Process

### Step 1 — Get Browser Context

```
mcp__claude-in-chrome__tabs_context_mcp(createIfEmpty: true)
```

### Step 2 — Navigate

**For a specific post:**
```
mcp__claude-in-chrome__navigate(url: "<post_url>", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

**For notifications:**
```
mcp__claude-in-chrome__navigate(url: "https://x.com/notifications", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

Take a screenshot to verify state:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

If not logged in, stop and tell the user to log in manually.

### Step 3 — Collect Comments / Mentions

**On a specific post:**

1. Scroll through the replies section below the post:
```
mcp__claude-in-chrome__get_page_text(tabId: <tab>)
```

2. Use JavaScript to extract reply content:
```
mcp__claude-in-chrome__javascript_tool(action: "javascript_exec", text: "
  const articles = document.querySelectorAll('article');
  const replies = Array.from(articles).slice(1).map((article, i) => {
    const text = article.innerText;
    const ariaLabels = Array.from(article.querySelectorAll('[aria-label]'))
      .map(el => el.getAttribute('aria-label'));
    return { index: i, text: text.substring(0, 300), meta: ariaLabels.slice(0, 5) };
  });
  JSON.stringify(replies.slice(0, 15), null, 2);
", tabId: <tab>)
```

3. Scroll to load more replies if needed:
```
mcp__claude-in-chrome__computer(action: "scroll", coordinate: [640, 400], scroll_direction: "down", scroll_amount: 5, tabId: <tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 2, tabId: <tab>)
```

**On notifications page:**

1. Read the notifications:
```
mcp__claude-in-chrome__get_page_text(tabId: <tab>)
```

2. Identify which notifications are replies to your posts (vs. likes, follows, etc.)

3. Filter for actionable notifications:
   - Replies to your posts (highest priority — reply to create conversation)
   - Quote tweets of your posts (reply to amplify)
   - Mentions in others' posts (engage if relevant)

### Step 4 — Prioritize Comments for Reply

Categorize each comment by reply value:

**High Priority (reply immediately):**
- Genuine questions about your content
- Substantive disagreements or alternative perspectives
- Replies from accounts with larger followings (amplification potential)
- Comments that add valuable context (quote-tweet candidates)
- First few replies on a fresh post (within the 30-90 min critical window)

**Medium Priority (reply when time allows):**
- Agreement with additional insight ("exactly, and also...")
- Personal experience sharing
- Feature requests or suggestions (if relevant to your product)

**Low Priority (optional):**
- Simple agreement ("great post!", "so true")
- Off-topic replies
- Spam or bot replies

Present the prioritized list to the user:
> Found [N] replies. Here are the ones worth responding to, ranked by conversation velocity impact:
>
> 1. **[Username]**: "[Reply preview]" — [why this is high priority]
> 2. **[Username]**: "[Reply preview]" — [why]
> ...

### Step 5 — Draft Replies

For each high-priority comment, draft a reply that:

1. **Adds value beyond "thanks"** — The algorithm weights substantive replies higher
2. **Extends the conversation** — Ask a follow-up question to encourage another reply
3. **Is concise** — 1-3 sentences max for replies
4. **Maintains the author's voice** — Match the tone of the original post

**Reply templates by comment type:**

| Comment Type | Reply Strategy |
|-------------|----------------|
| Question | Direct answer + "curious, have you tried [related thing]?" |
| Disagreement | Acknowledge the point + share your reasoning + "what's your experience with [specific]?" |
| Personal experience | Validate + relate to your own experience + ask for detail |
| Feature request | Thanks + honest status/timeline + "what's the use case?" |
| Added context | Amplify their point + tag relevant people if appropriate |

Present drafted replies using AskUserQuestion for each high-priority comment:

```
AskUserQuestion:
  "Replying to @username:
  They said: \"[their comment]\"

  My draft: \"[your drafted reply]\"

  ✅ 'post' — send this reply
  ✏️ Reply with changes — I'll revise (e.g., 'make it shorter', 'add a question')
  ⏭️ 'skip' — skip this one
  ❌ 'stop' — done replying for now"
```

**Handle the response:**

- **"post" / "yes" / "send it"** → Proceed to post this reply (Step 6)
- **User requests changes** (e.g., "more casual", "ask about their setup") → Revise the draft and present again. Loop until approved or skipped.
- **"skip"** → Move to the next comment
- **"stop" / "done"** → End the engagement session, skip to summary

### Step 6 — Post Approved Replies

For each approved reply:

1. Navigate to the comment (if on notifications, click through to the post):
```
mcp__claude-in-chrome__find(query: "reply button for this comment", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

2. Wait for reply compose to open:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 1, tabId: <tab>)
```

3. Type the reply:
```
mcp__claude-in-chrome__computer(action: "type", text: "<reply_content>", tabId: <tab>)
```

4. Take a screenshot for verification:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

5. The user already approved this reply in Step 5's review loop, so proceed to post. If the screenshot shows something unexpected (wrong reply box, different content), pause and re-confirm.

6. After confirmation, click the Reply button:
```
mcp__claude-in-chrome__find(query: "reply post button or submit reply button", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

7. Wait for the reply to post:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 2, tabId: <tab>)
```

### Step 7 — Reply Farming (Optional)

If the user wants to build visibility before posting their own content:

1. Ask: "Want me to find posts in your niche to engage with? This warms up the algorithm before your next post."

2. If yes, search for relevant posts:
```
mcp__claude-in-chrome__navigate(url: "https://x.com/search?q=[niche_topic]&f=live", tabId: <tab>)
```

3. Find posts with active engagement that the user could add value to.

4. Draft thoughtful replies (no self-promotion — genuine value only).

5. Present for approval and post as in Step 6.

### Step 8 — Summary

After the engagement session, summarize:

1. **Replies posted**: [N] replies across [N] posts
2. **Conversation threads created**: [N] (each = 75–150× multiplier)
3. **Estimated impact**: Based on reply count and conversation depth
4. **Pending**: Any comments you skipped that might be worth revisiting
5. **Time spent**: Help the user calibrate their daily engagement routine

## Rate Limiting

- **Wait 3-5 seconds between posting each reply** — rapid-fire replies look automated
- **Maximum 10 replies per /engage session** — stop and summarize after 10
- **If X shows a rate limit or error**, screenshot it, inform the user, and stop immediately

## Dry-Run Mode

If the user says "dry run" or "just draft":
- Read comments, prioritize, draft replies — but **do not open any reply boxes or post anything**
- Present all drafted replies at once for review
- The user can then run `/engage` again without dry-run to post the approved drafts

## Critical Rules

1. **NEVER post a reply without explicit user confirmation.** Always show the draft and ask first.
2. **NEVER handle authentication.** If not logged in, tell the user to log in manually.
3. **Quality over speed.** A thoughtful reply that extends conversation is worth 100 "thanks!" replies.
4. **No self-promotion in replies.** Replies to others' posts should add genuine value — no links to your stuff unless directly asked.
5. **Stay on-topic.** Only engage with content in the user's niche.
6. **If rate-limited or blocked by X**, stop immediately and inform the user.
7. **Respect boundaries.** If a user indicates they don't want engagement, respect that.
8. **X may detect automation.** Space replies naturally. If X presents a CAPTCHA or challenge, stop and inform the user.

## Troubleshooting

- **Reply button not found**: Try clicking on the comment/post first to expand it, then look for the reply icon
- **Can't type in reply box**: Click directly on the text area, try using `find` for "reply text input"
- **Notifications not loading**: Try refreshing the page or navigating to `x.com/notifications/mentions`
- **Too many notifications**: Focus on the most recent 10-15, prioritize replies to your own posts
