# URL Content Reading — Shared Reference

When any skill receives a URL as input, use the appropriate tool to read its content before proceeding with the skill's normal workflow.

## Tool Selection

| URL Type | Tool | Notes |
|----------|------|-------|
| Blog post, article | WebFetch | Public content, fast |
| GitHub release page | WebFetch | Public, works reliably |
| GitHub README / repo | WebFetch | Public |
| Documentation page | WebFetch | Public |
| Changelog / release notes | WebFetch | Public |
| Product/landing page | WebFetch | Public |
| X/Twitter post (text) | WebFetch | Public post text is fetchable |
| X/Twitter post (metrics) | Chrome (`/analyze`) | Requires logged-in session for full metrics |
| X/Twitter profile/analytics | Chrome (`/analyze`, `/strategy`) | Requires auth |
| Taking a screenshot of any page | Chrome (`/media`) | Only browser can capture screenshots |
| Paywalled / authenticated content | Chrome | If user is logged in |
| Interactive / JS-heavy SPA | Chrome | WebFetch may not render JS content |

**Default to WebFetch.** Only escalate to Chrome when WebFetch can't access the content (auth required, JS-rendered, or screenshot needed).

## WebFetch Pattern

When a skill detects a URL in the input:

```
WebFetch(url: "<the_url>", prompt: "Extract the key content from this page: [specific extraction guidance based on the skill's needs]")
```

### Extraction Prompts by Content Type

**GitHub release page:**
```
prompt: "Extract the release version, date, and complete changelog. List new features, bug fixes, and breaking changes separately."
```

**Blog post / article:**
```
prompt: "Extract the title, author, main argument/thesis, and key points. Include any data, benchmarks, or specific claims with numbers."
```

**Product / landing page:**
```
prompt: "Extract the product name, tagline, key features, pricing if shown, and any specific performance claims or metrics."
```

**GitHub README:**
```
prompt: "Extract the project description, key features, installation instructions, and any benchmarks or comparisons mentioned."
```

**Documentation page:**
```
prompt: "Extract the main topic, key concepts explained, code examples, and any important caveats or notes."
```

**X/Twitter post:**
```
prompt: "Extract the post text, author username, and any visible engagement metrics (replies, reposts, likes, bookmarks, views)."
```

## Chrome Pattern (When Needed)

When WebFetch can't access the content:

1. Get browser context: `mcp__claude-in-chrome__tabs_context_mcp`
2. Create or reuse tab: `mcp__claude-in-chrome__tabs_create_mcp` or use existing
3. Navigate: `mcp__claude-in-chrome__navigate(url: "<url>", tabId: <tab>)`
4. Wait for load: `mcp__claude-in-chrome__computer(action: "wait", duration: 2, tabId: <tab>)`
5. Read content: `mcp__claude-in-chrome__get_page_text(tabId: <tab>)` for text, or `mcp__claude-in-chrome__read_page(tabId: <tab>)` for structured elements
6. Screenshot if needed: `mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)`

## URL Detection

A skill should handle URL input when:
- The argument starts with `http://`, `https://`, or `www.`
- The argument contains `github.com`, `x.com`, `twitter.com`, or common domain patterns
- The user explicitly says "read this page" or "from this URL"

When a URL is detected, read the content first, then proceed with the skill's normal workflow using the extracted content as the input material.
