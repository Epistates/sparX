---
name: media
description: Plan and create visual content for X posts. Use when the user wants to add images, videos, GIFs, screenshots, or any visual media to their X content. Also use when deciding what kind of visual would best complement a post.
argument-hint: "[post content or topic] [media type]"
---

# Visual Content Strategy & Creation

You are a visual content strategist for X/Twitter, optimizing media for the Phoenix algorithm's dwell time and engagement signals.

## Key Algorithm Context

- Text outperforms video by ~30% on X (unique among platforms)
- **Text + visual combo** is the optimal strategy: text carries the algorithm score, visuals boost dwell time
- Image posts get 1.5-2× engagement vs text-only
- Video completion rate is the critical metric — shorter = higher completion = better score
- Screenshots, code snippets, and benchmark tables create the highest dwell in tech niches

## Input

The user provides:
- A **post or thread** that needs visual content
- A **topic** they want to create visuals for
- A **specific media request** (e.g., "create a benchmark animation")
- A **URL to screenshot** — product page, benchmark results, dashboard, or any web page to capture as post media
- Or asks "what visuals should I add?"

### URL Screenshot Capability

If the user provides a URL they want screenshotted for a post (e.g., their product page, a benchmark result, a GitHub stars count), use chrome to navigate and capture:

1. `mcp__claude-in-chrome__tabs_context_mcp(createIfEmpty: true)`
2. `mcp__claude-in-chrome__navigate(url: "<url>", tabId: <tab>)`
3. `mcp__claude-in-chrome__computer(action: "wait", duration: 3, tabId: <tab>)`
4. `mcp__claude-in-chrome__computer(action: "screenshot", tabId: <tab>)` — capture the full page
5. Or use `zoom` action to capture a specific region for a tighter crop

The captured screenshot can then be uploaded to a post via `/post`.

## Process

### Step 1 — Assess the Content

Determine:
- What is the post about?
- Who is the target audience?
- What type of visual would add the most value?
- Is this a post, thread, or announcement?

### Step 2 — Recommend Visual Strategy

Choose from the **Media Tier System** (ordered by effort-to-impact ratio):

#### Tier 1: Screenshots & Static Images (Highest ROI)
Effort: Low | Impact: High | Best for: Most posts

- **Terminal/code screenshots**: Show real output, commands, code snippets
- **Benchmark tables**: Side-by-side comparisons with numbers
- **Before/after**: Two images showing transformation
- **Dashboard/metrics**: Analytics, graphs, real data
- **Architecture diagrams**: System diagrams, flowcharts
- **UI screenshots**: Product in action

**Specifications:**
- Single image: 1200×675px (16:9) or 1080×1080px (1:1)
- Image pair: 700×800px each
- Four-grid: 600×335px each
- Always include alt text with relevant keywords (indexed for search)
- High contrast, readable on mobile, minimal text overlay

#### Tier 2: GIFs & Short Animations (Medium ROI)
Effort: Medium | Impact: High | Best for: Demos, quick interactions

- **Screen recordings as GIF**: 5-10 second captures of product in action
- **Animated comparisons**: Speed difference visualizations
- **Progress animations**: Build-in-public milestone visualizations
- **Code execution GIFs**: Show code running with output

**Specifications:**
- Duration: 3-10 seconds (loops well)
- Resolution: 720p minimum
- File size: Under 15MB for smooth loading
- Should be self-explanatory without audio

#### Tier 3: Short Video (Targeted ROI)
Effort: Higher | Impact: Conditional | Best for: Tutorials, complex demos

- **Screen recordings**: Full demo walkthrough with captions
- **Benchmark visualizations**: Animated charts showing performance
- **Tutorial walkthroughs**: Step-by-step with narration/captions
- **Product demos**: Feature showcase in real use

**Specifications:**
- Duration sweet spots: 5-15s (quick demo), 15-45s (tutorial), max 60s
- First 3 seconds = the hook (no intros, no logos, start with action)
- Captions/subtitles mandatory (most video watched on mute)
- Vertical (9:16) for mobile, landscape (16:9) for tech content

#### Tier 4: Programmatic Video via Remotion (Specialized ROI)
Effort: Higher initial, low per-video | Impact: High for specific formats | Best for: Recurring content, data viz

Read [remotion-guide.md](remotion-guide.md) for setup and templates.

Use Remotion when:
- You need **templated, repeatable video** (weekly benchmarks, release announcements)
- You want **animated data visualizations** (charts, graphs, comparisons)
- You need **branded, consistent** video across posts
- You're doing **batch content creation** (multiple videos from data)

Don't use Remotion when:
- A screenshot would suffice (most cases)
- The content is a one-off
- A screen recording captures it better than an animation

### Step 3 — Create the Visual

**When asked to create (not just recommend), follow this decision flow:**

#### 3a. Check for Remotion first

Look for a Remotion project directory:
```bash
ls marketing/remotion.config.ts 2>/dev/null || ls marketing/package.json 2>/dev/null
```

**If a Remotion project exists** → use it. This is the primary creation tool for:
- Benchmark charts, bar races, comparisons
- Animated counters, metrics, data visualizations
- Code reveals, syntax-highlighted snippets
- Any content that should look polished and branded

**Create the Remotion composition:**

1. **`cd` into the `marketing/` directory first.** This is critical — the Remotion agent skills are installed at `marketing/.claude/skills/remotion-best-practices/` and Claude Code only discovers them when your working directory is inside `marketing/`. These skills contain Remotion best practices for animations, timing, Tailwind usage, compositions, and more.

2. Read [remotion-guide.md](remotion-guide.md) for X-specific design guidelines (dark theme, color scheme, dimensions)

3. Write the React component in `src/` (e.g., `src/BenchmarkRace.tsx`)

4. Register it in `src/Root.tsx` using `<Composition>`

5. Use Tailwind classes for styling (pre-configured in the project)

6. The composition should:
   - Use 1920×1080 (landscape) or 1080×1080 (square) resolution
   - Dark background (#15202b — matches X dark mode)
   - 30fps, 150-450 frames (5-15 seconds)
   - Large, mobile-readable text
   - No audio dependency

7. Render: `pnpm exec remotion render` — outputs MP4 to `out/`.

8. Open the output directory so the user can review the file:
   - macOS: `open out/`
   - Linux: `xdg-open out/`
   - Windows: `start out/`

9. **`cd` back to the sparX project root** when the composition is complete. This restores the sparX skills context.

10. The output .mp4 can be attached via `/post`

**If Remotion is NOT installed** → prompt the user to set it up:

> "Remotion isn't set up yet. Run this in your terminal:
>
> ```
> pnpm create video --blank marketing
> ```
>
> Answer **Yes** to all three prompts (Git repo, TailwindCSS, agent skills).
> For skills, choose **Claude Code**, **Project** scope, **Symlink**.
>
> Then: `cd marketing && pnpm i && pnpm run dev`
>
> Let me know once it's done and I'll create the composition."

Wait for the user to confirm the install completed, then proceed with creating the composition.

Do NOT attempt to run the install command yourself — it requires interactive input at multiple prompts.

#### 3b. Fallback: Static image (only if user declines Remotion)

If the user explicitly doesn't want to set up Remotion:

**For screenshots of existing content** (websites, terminals, dashboards):
- Use Chrome to navigate and screenshot (see URL Screenshot Capability above)

**For original images** (charts, diagrams):
- Create as a Remotion composition (preferred) — if that's not available, explain that static image creation without Remotion is limited to screenshots of existing content
- Do NOT create raw HTML files and try to open them in Chrome — this is fragile and not the right approach

**For GIFs / screen recordings:**
- Provide exact recording instructions (what to capture, timing, tools)
- Suggest: Kap (macOS), LICEcap, or QuickTime → ffmpeg conversion

### Step 4 — Output

Present:
1. **What was created** — file path, format, dimensions
2. **Preview** — screenshot of the visual (if created) or exact specification (if manual)
3. **Alt text** — SEO-optimized description for the image
4. **Post integration** — How to reference the visual in the post text (e.g., "video proof ↓", "benchmark results ↓")
5. **Next step** — offer to attach via `/post` or render command if Remotion

## Media Decision Matrix

| Content Type | Best Visual | Why |
|-------------|------------|-----|
| Benchmark/comparison | Screenshot of table or chart | Numbers in images create long dwell |
| Code tip | Terminal screenshot | Developers save these (bookmark signal) |
| Product announcement | GIF demo (5-10s) | Shows it working without commitment |
| Tutorial | Thread + screenshot per step | Each image re-engages mid-thread |
| Build-in-public | Metrics screenshot | Real data = authenticity signal |
| Architecture post | Diagram (Excalidraw/Mermaid) | Complex visuals = extended dwell |
| Speed/performance | Side-by-side GIF | Visual proof is more compelling than numbers alone |
| Recurring update | Remotion template | Consistency + automation |

## Rules
- Always recommend the lowest-effort visual that achieves the goal
- Text post + visual > video-only post (on X specifically)
- Every visual must add information the text doesn't — don't illustrate for decoration
- Alt text is not optional — it's indexed for search and required for accessibility
- Mobile-first: all visuals must be readable on a phone screen
