---
name: post
description: Post content directly to X via browser automation. Use when the user wants to publish a composed post or thread to X/Twitter without copy-pasting. Requires claude-in-chrome.
argument-hint: "[post content or 'last' to use previous compose/thread output]"
allowed-tools: mcp__claude-in-chrome__tabs_context_mcp, mcp__claude-in-chrome__tabs_create_mcp, mcp__claude-in-chrome__navigate, mcp__claude-in-chrome__read_page, mcp__claude-in-chrome__find, mcp__claude-in-chrome__form_input, mcp__claude-in-chrome__computer, mcp__claude-in-chrome__javascript_tool, mcp__claude-in-chrome__upload_image, mcp__claude-in-chrome__get_page_text, AskUserQuestion
---

# Post to X via Browser

Publish a post or thread directly to X using chrome browser automation.

## Input

The user provides one of:
- **Post content** directly as the argument
- **"last"** to use the output from a previous `/compose` or `/thread` invocation in this session
- **A thread** as numbered tweets or clearly separated tweets
- **Media to attach** — a file path (image, GIF, video), a screenshot taken this session, or a request to screenshot a URL first via `/media`

If the content includes a **link reply** (a separate reply containing a URL), handle that as a follow-up reply after the main post.

## Pre-Flight

Before doing anything:
1. Parse the input to determine: **single post** vs **thread** vs **post + link reply** vs **post + media**
2. Validate character counts (each tweet ≤ 280 characters)
3. If any tweet exceeds 280 characters, stop and ask the user to revise — do NOT truncate
4. If media is referenced, determine the media type and upload path (see Step 5)

## Process

### Step 1 — Get Browser Context

```
mcp__claude-in-chrome__tabs_context_mcp(createIfEmpty: true)
```

Check if there's an existing tab on x.com. If yes, use it. If not, create a new tab.

### Step 2 — Navigate to X

```
mcp__claude-in-chrome__navigate(url: "https://x.com", tabId: <tab>)
```

Wait for the page to load. Take a screenshot to verify you're on X and logged in.

```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

**If not logged in**: Stop and tell the user they need to log in manually. Do NOT attempt to handle authentication.

### Step 3 — Open Compose

Navigate directly to the compose URL (most reliable):
```
mcp__claude-in-chrome__navigate(url: "https://x.com/compose/post", tabId: <tab>)
```

Wait for the compose dialog to fully load:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 2, tabId: <tab>)
```

### Step 4a — Single Post

1. Find the text input area in the compose dialog:
```
mcp__claude-in-chrome__find(query: "tweet text input area", tabId: <tab>)
```

2. Click on it to focus:
```
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

3. Type the post content:
```
mcp__claude-in-chrome__computer(action: "type", text: "<post_content>", tabId: <tab>)
```

4. If media needs to be attached, do Step 5 now (before the review loop).

5. **Enter the Review Loop** (see Review Loop section below).

### Step 4b — Thread

1. Open compose and type the **first tweet** (same as 4a steps 1-3).

2. To add the next tweet, find and click the "Add another post" button (the + icon):
```
mcp__claude-in-chrome__find(query: "add another tweet button or plus button to add to thread", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

3. Type the next tweet's content in the new text area:
```
mcp__claude-in-chrome__find(query: "empty tweet text input", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "type", text: "<tweet_content>", tabId: <tab>)
```

4. Repeat steps 2-3 for each subsequent tweet in the thread.

5. If media needs to be attached to any tweet, do Step 5 for that tweet.

6. **Enter the Review Loop** (see Review Loop section below).

### Step 4c — Link Reply (after posting)

If the original content included a link that should go in a reply:

1. After the main post is published, wait for it to appear:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

2. Find the just-published post and click the reply icon:
```
mcp__claude-in-chrome__find(query: "reply button on the latest post", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

3. Type the link reply content:
```
mcp__claude-in-chrome__computer(action: "type", text: "<link_reply_content>", tabId: <tab>)
```

4. Take a screenshot and **enter the Review Loop** for the reply too.

---

## Review Loop

This is the critical confirmation flow. **Every post and reply goes through this loop before publishing.**

### 1. Screenshot the current state

```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

For threads, scroll through to capture all tweets if needed.

### 2. Present the review to the user

Use AskUserQuestion to present the post and collect feedback:

```
AskUserQuestion:
  "Here's your [post/thread/reply] ready to publish:

  [Show the full text of what will be posted]

  ✅ 'post' — publish now
  ✏️ Reply with changes — I'll revise and show you again
  ❌ 'cancel' — abort without posting"
```

### 3. Handle the response

**If the user says "post", "yes", "go", "send it", or similar affirmative:**
→ Proceed to click the Post button:
```
mcp__claude-in-chrome__find(query: "post button or tweet button", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

Wait for publish:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

Take confirmation screenshot:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

**If the user requests changes** (e.g., "make the hook stronger", "remove the last line", "add a question at the end"):
→ Apply the requested changes:
1. Select all text in the compose box (triple-click or Cmd+A)
2. Delete it
3. Type the revised content
4. **Loop back to step 1** — screenshot and present the revision for review

The loop continues until the user approves or cancels. There is no limit on revision rounds.

**If the user says "cancel", "abort", "nevermind":**
→ Close the compose dialog (press Escape or navigate away)
→ Confirm: "Post cancelled. The draft is still available if you want to revise it."

---

## Step 5 — Media Attachment

Media attachment happens BEFORE the review loop, so the user sees the full post with media in the screenshot.

### Path A: Screenshot from this session

If the media is a screenshot captured during this Claude Code session (e.g., from `/media` taking a screenshot of a webpage):

1. Find the media upload button in compose:
```
mcp__claude-in-chrome__find(query: "add photo or media button in compose", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

2. Find the file input element:
```
mcp__claude-in-chrome__find(query: "file input for media upload", tabId: <tab>)
```

3. Upload via the ref:
```
mcp__claude-in-chrome__upload_image(imageId: "<screenshot_id>", ref: "<file_input_ref>", tabId: <tab>)
```

4. Wait for the upload to process:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)
```

### Path B: Local file (Remotion video, image, GIF)

For local files on disk (e.g., a Remotion-rendered .mp4 at `marketing/out/video.mp4`):

The chrome `upload_image` tool cannot directly access local filesystem files. Use this approach:

1. Find the media upload button and click it:
```
mcp__claude-in-chrome__find(query: "add photo or media button in compose", tabId: <tab>)
mcp__claude-in-chrome__computer(action: "left_click", ref: "<ref_id>", tabId: <tab>)
```

2. **This opens a native file picker dialog.** Tell the user:

```
AskUserQuestion:
  "I've opened the media upload dialog. Please select your file:

  📁 [file path, e.g., marketing/out/video.mp4]

  Navigate to this file in the picker and click Open.
  Let me know once the file is selected and uploading."
```

3. After the user confirms the file is selected, wait for processing:
```
mcp__claude-in-chrome__computer(action: "wait", duration: 5, tabId: <tab>)
```

4. Take a screenshot to verify the media attached correctly:
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)
```

5. If the media looks wrong, ask the user if they want to remove it and try again.

### Path C: URL screenshot (inline)

If the user wants to screenshot a webpage to attach:

1. Navigate to the URL in a separate tab:
```
mcp__claude-in-chrome__tabs_create_mcp()
mcp__claude-in-chrome__navigate(url: "<url>", tabId: <new_tab>)
mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <new_tab>)
```

2. Take a screenshot (this creates an imageId):
```
mcp__claude-in-chrome__computer(action: "screenshot", tabId: <new_tab>)
```

3. Switch back to the X compose tab and use Path A to upload the screenshot.

### Media Compatibility

| Format | X Support | Notes |
|--------|-----------|-------|
| .png, .jpg, .gif | Yes | Images up to 5MB, GIFs up to 15MB |
| .mp4 | Yes | Video up to 512MB, 2:20 max duration |
| .mov | Yes | Converted to MP4 by X |
| .webp | Limited | Convert to PNG/JPG first |

---

## Post-Publish

After successful posting:

1. Take a confirmation screenshot showing the published post
2. If there's a link reply, proceed to Step 4c
3. Remind the user:

```
"Posted! 🎯

Remember: reply to every comment in the first hour — that's the 75–150× conversation velocity multiplier.

Run /engage on this post in 30-60 minutes to manage replies."
```

## Dry-Run Mode

If the user says "dry run", "preview only", or "don't actually post":
- Complete the entire flow up through the Review Loop (navigate, compose, type, screenshot)
- **Stop before clicking Post.** Show the screenshot and say: "Dry run complete — here's what would be posted. Nothing was published."
- This lets users test the full pipeline without risk.

## Rate Limiting

- **Wait 3-5 seconds between any two posting actions** (post → link reply, or thread → next action)
- **Never post more than 5 times in a single /post invocation** (threads count as 1)
- **If X shows an error or rate limit message**, screenshot it, inform the user, and stop. Do not retry.

## Critical Rules

1. **Every post goes through the Review Loop.** No exceptions.
2. **The user can request unlimited revisions.** Loop until they approve or cancel.
3. **NEVER handle authentication.** If not logged in, tell the user to log in manually.
4. **NEVER exceed 280 characters per tweet.** Validate before typing.
5. **If anything goes wrong** (element not found, page not loading, unexpected state), take a screenshot, describe what you see, and ask the user how to proceed. Do not retry blindly.
6. **For local file uploads**, always tell the user the exact file path so they can find it in the picker.
7. **X may detect automation.** Browser automation leaves different fingerprints than manual use. Always review screenshots before confirming. If X presents a CAPTCHA or verification challenge, stop and inform the user.

## Troubleshooting

- **Can't find compose button**: Navigate directly to `x.com/compose/post`
- **Can't find post button**: Take a screenshot, look for the button visually, use coordinates
- **Thread + button not found**: Look for icon buttons near the compose area, may be labeled differently
- **Page loads slowly**: Use `wait` with 2-3 seconds between navigation and interaction
- **Content has special characters**: Type content carefully; if emojis fail, try `javascript_tool` to set the value directly via DOM
- **Media upload stuck**: Take a screenshot to check status, wait up to 10 seconds for video processing
- **File picker won't close**: The user may need to manually dismiss it; ask them
- **Video too large**: X accepts up to 512MB / 2:20 duration — suggest trimming with ffmpeg if needed
