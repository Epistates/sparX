# Remotion Integration Guide

## What is Remotion?

Remotion lets you create videos programmatically using React. You write TypeScript components that describe each frame, and Remotion renders them into MP4/GIF files. Combined with Claude Code, you describe what you want in natural language and Claude generates the React code.

## When Remotion Makes Sense for X Content

**Use Remotion for:**
- Animated benchmark comparisons (bar charts racing, counters ticking up)
- Recurring content templates (weekly metrics, release announcements)
- Data visualizations that update with new numbers
- Branded intro/outro clips for screen recordings
- Animated code walkthroughs (syntax highlighting + line-by-line reveal)
- Side-by-side speed comparisons with progress bars

**Don't use Remotion for:**
- One-off screenshots (use macOS screenshot tools)
- Simple screen recordings (use QuickTime/OBS)
- Content where a GIF suffices (use Kap or gifify)
- Anything where the setup time exceeds the content value

## Optimal Output Specs for X

| Format | Resolution | Duration | Use Case |
|--------|-----------|----------|----------|
| MP4 (landscape) | 1920×1080 | 5-15s | Tech demos, benchmarks |
| MP4 (square) | 1080×1080 | 5-15s | General audience, announcements |
| MP4 (vertical) | 1080×1920 | 5-15s | Mobile-optimized content |
| GIF | 720×480 | 3-8s | Inline demos, quick comparisons |

## Template Ideas for X Content

### 1. Benchmark Race Animation
Two or more horizontal bars racing to completion, showing speed difference between tools/approaches. Final frame freezes with exact numbers.

```
[Tool A] ████████████████████████████ 2.3s
[Tool B] ███████████████████░░░░░░░░░ 5.1s (still going)
```

### 2. Counter Ticking Up
Start at 0, animate to the impressive number (stars, downloads, speed). Use easing for dramatic effect — slow start, accelerating, then settling.

### 3. Code Reveal
Syntax-highlighted code appearing line by line with a cursor, as if being typed. Final frame shows the complete snippet with a result annotation.

### 4. Before/After Split
Screen split in half — left shows "before" state, right shows "after" state. Can animate a sliding divider or toggle between states.

### 5. Architecture Diagram Build
Boxes and arrows appearing sequentially, building up a system diagram. Each component appears with a brief label. Good for explaining how something works.

### 6. Metrics Dashboard Animation
Numbers and charts animating from zero to their current values. Use for weekly/monthly progress updates with consistent branding.

## Working with Remotion in Claude Code

Once Remotion is set up (via `pnpm create video --blank marketing`), the workflow is:

1. The `/media` skill detects Remotion is installed (checks `marketing/remotion.config.ts`)
2. Claude `cd`s into `marketing/` (picks up Remotion agent skills)
3. Claude writes a React + Tailwind composition into `src/`
4. Claude renders with `pnpm exec remotion render` → MP4 in `out/`
5. Claude opens the `out/` directory for the user to review
6. Claude `cd`s back to sparX root, output .mp4 can be attached via `/post`

### Where to write compositions

Write new compositions into `marketing/src/`. Each composition needs:
- A React component file (e.g., `marketing/src/BenchmarkRace.tsx`)
- Registration in `marketing/src/Root.tsx` using `<Composition>`
- Tailwind classes for styling (pre-configured)

### Render commands

All commands run from inside the `marketing/` directory:

```bash
cd marketing

# Render default composition to MP4
pnpm exec remotion render

# Render a specific composition
pnpm exec remotion render BenchmarkRace

# Render to specific output path
pnpm exec remotion render BenchmarkRace out/benchmark.mp4

# Open output directory to review
open out/  # macOS (use xdg-open on Linux, start on Windows)

# Render specific frame range
pnpm exec remotion render BenchmarkRace --frames=0-150
```

## Design Guidelines for X

- **Dark theme** — X's dark mode is dominant; dark backgrounds blend better in-feed
- **Large text** — Must be readable on mobile without expanding
- **No audio dependency** — Assume muted playback; use text overlays for narration
- **Brand colors** — Use consistent colors across videos for recognition
- **First frame matters** — The thumbnail/preview frame should be compelling on its own
- **Loop-friendly** — For GIFs and short clips, design so the loop feels natural
