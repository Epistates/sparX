# Media Strategy — Visual Content for X

## The X Media Paradox

X is the only major platform where text outperforms video by ~30%. Yet the **highest-performing posts combine text + visual media**. The reason: text carries the algorithm score (reply triggers, dwell from reading), while visuals extend dwell time and create bookmark appeal.

**The strategy is not "always add media."** It's **"add media when it amplifies the message."**

## When to Add Visuals (and When Not To)

### Add visuals when:
- You have **benchmark data or comparisons** → screenshot or chart
- You're showing **something working** → GIF or short screen recording
- You have **before/after results** → side-by-side images
- You're explaining **architecture or flow** → diagram
- You're sharing **code** → syntax-highlighted screenshot
- You're doing a **build-in-public update** → metrics screenshot

### Skip visuals when:
- The post is a **hot take or opinion** — text is the native format for debate
- You're asking a **question or poll** — visuals can distract from the CTA
- The insight is **self-contained in text** — don't illustrate for decoration
- Adding media would **delay posting** a time-sensitive piece

## The Media Tier System

### Tier 1: Screenshots & Static Images
**Effort**: 5 minutes | **Impact**: 1.5-2× engagement vs text-only

The workhorse of X visual content. Used in the majority of high-performing tech posts.

**Best practices:**
- Dark theme screenshots (matches X dark mode — blends naturally in feed)
- Crop to the relevant area (no browser chrome, no desktop clutter)
- Add red arrows or highlight boxes to draw attention to key areas
- Use readable font sizes — test on your phone before posting
- Include alt text (indexed for search, required for accessibility)

**Tools:**
- macOS: Cmd+Shift+4 (area), Cmd+Shift+5 (window/screen)
- CleanShot X: Annotations, highlights, scrolling capture
- Carbon: Beautiful code screenshots (carbon.now.sh)
- Excalidraw: Hand-drawn style diagrams
- Mermaid: Code-based diagrams (renders in GitHub, many tools)

**Recommended dimensions:**
| Format | Size | Use |
|--------|------|-----|
| Single landscape | 1200×675px | Default for screenshots |
| Single square | 1080×1080px | Infographics, standalone images |
| Pair | 700×800px each | Before/after, comparisons |
| Four-grid | 600×335px each | Multi-step sequences |

### Tier 2: GIFs & Short Animations
**Effort**: 15-30 minutes | **Impact**: High for demos, speed comparisons

GIFs loop automatically in-feed, creating persistent visual interest without requiring the user to press play.

**Best practices:**
- 3-10 seconds (loops should feel natural)
- Under 15MB file size (otherwise slow loading degrades experience)
- Start with the most interesting moment (first frame = thumbnail)
- No audio dependency (GIFs are silent by nature)
- Optimized palette (fewer colors = smaller file = faster load)

**Tools:**
- Kap: macOS screen recording → GIF with one click
- LICEcap: Lightweight GIF recording directly
- gifify: Convert video files to GIF via command line
- macOS QuickTime → ffmpeg: `ffmpeg -i recording.mov -vf "fps=15,scale=720:-1" output.gif`

**Best use cases:**
- Quick CLI demos (type command → see result)
- UI interaction demos (click → animation → result)
- Speed comparisons (side-by-side running processes)
- Before/after toggles

### Tier 3: Short Video
**Effort**: 30-60 minutes | **Impact**: High when done right, risky when too long

Video requires pressing play, so there's a conversion barrier. But completion rate is a powerful signal.

**Best practices:**
- **15-45 seconds** is the sweet spot
- First 3 seconds = the hook (no intros, no logos, start with action)
- Captions/subtitles mandatory (80%+ of video watched on mute)
- End with a clear takeaway or call-to-action overlay
- Landscape (16:9) for tech content, square (1:1) for broader audience

**Tools:**
- OBS Studio: Free, professional screen recording
- QuickTime: Built into macOS, simple and reliable
- Loom: Screen recording + face cam + instant sharing
- ScreenFlow: macOS screen recording with editing
- Descript: AI-powered video editing with auto-captions

**Duration guidelines:**
| Length | Completion Rate | Best For |
|--------|----------------|----------|
| 5-15s | Very high (~80%) | Quick demos, one feature |
| 15-30s | High (~60%) | Short tutorials, benchmarks |
| 30-45s | Moderate (~40%) | Multi-step demos |
| 45-60s | Lower (~25%) | Complex tutorials (risky) |
| 60s+ | Low (<15%) | Avoid unless compelling narrative |

### Tier 4: Remotion — Programmatic Video
**Effort**: Higher setup, low per-video | **Impact**: Specialized but powerful

Remotion generates video from React code. Ideal for templated, repeatable, or data-driven content.

**When Remotion shines:**
- **Recurring content**: Weekly benchmark updates, metrics dashboards
- **Data visualization**: Animated charts that update with new numbers
- **Branded content**: Consistent visual identity across all video posts
- **Batch creation**: Generate 10 variations from one template
- **Benchmark races**: Animated bar charts showing speed comparisons

**Setup**: Run `/setup remotion` in Claude Code.

**Workflow:**
1. Describe the video in natural language
2. Claude generates the React composition using Remotion Agent Skills
3. Preview in browser with `cd marketing && pnpm run dev`
4. Render to MP4 with `pnpm exec remotion render`
5. Attach to your post

**X-optimized Remotion settings:**
- Background: #15202b (X dark mode background)
- Text: #e7e9ea (X dark mode text)
- Accent: #1d9bf0 (X blue) or your brand color
- Duration: 150-450 frames at 30fps (5-15 seconds)
- Resolution: 1920×1080 or 1080×1080

See `.claude/skills/media/remotion-guide.md` for templates and design guidelines.

## Media Workflow by Content Type

| Post Type | Recommended Media | Why |
|-----------|------------------|-----|
| Benchmark comparison | Screenshot of table + optional bar race GIF | Numbers in images create long dwell |
| Code tip | Carbon screenshot of code | Developers bookmark these |
| Product announcement | 5-10s GIF demo | Shows it working without commitment |
| Tutorial thread | Screenshot per step | Each image re-engages mid-thread |
| Build-in-public | Metrics dashboard screenshot | Real data = authenticity |
| Architecture explainer | Excalidraw diagram | Complex visuals = extended dwell |
| Speed/performance | Side-by-side GIF | Visual proof > stated numbers |
| Recurring metrics | Remotion animated chart | Templated, consistent, updatable |
| Hot take / opinion | No media | Text is the native debate format |
| Question / poll | No media (or minimal) | Don't distract from the CTA |

## Alt Text: The Free SEO Boost

X indexes alt text for search. Every image should have descriptive alt text that includes relevant keywords.

**Bad**: "Screenshot"
**Good**: "Terminal output showing pMetal v0.4 fine-tuning a 7B LLM model in 12 minutes on M3 Max, 2.3× faster than MLX"

Alt text also makes your content accessible to screen reader users — a non-trivial portion of the developer audience.

## Using /media in Practice

The `/media` skill integrates into your posting workflow:

```
# Draft your post first
/compose announcing our new CLI tool for automated deploys

# Then ask for visual guidance
/media what visual should I add to a post about a fast CLI deploy tool

# Or ask for Remotion generation
/media create a 10-second Remotion animation showing deploy time going from 45s to 3s
```

The skill recommends the tier that maximizes impact for your specific content, provides exact specifications, and guides creation step by step.
