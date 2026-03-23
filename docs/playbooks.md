# Playbooks — End-to-End Workflows

Step-by-step walkthroughs for common content scenarios. Each playbook chains multiple sparX skills into a complete workflow.

---

## Playbook: Ship a Product Announcement

You've just released a new version and want maximum visibility.

### Step 1: Research the landscape
```
/research [your product niche] — what conversations are happening right now?
```
Find the conversations your announcement can plug into. Note trending topics and pain points your release addresses.

### Step 2: Draft the announcement post
```
/compose [product] v2.0: [headline feature]. [Specific benchmark vs alternative]. [Key differentiator].
```
Give Claude the raw materials — version number, features, benchmarks, comparisons. It handles the hook, structure, and link placement.

### Step 3: Create supporting visual
```
/media benchmark comparison showing [old version] vs [new version] performance
```
The skill recommends the right format. For benchmarks, it's usually a screenshot of a table or a Remotion bar race animation.

### Step 4: Draft a companion thread
```
/thread deep dive on what's new in v2.0 — the technical decisions behind [headline feature]
```
The thread goes deeper than the announcement post. Post the thread 1-2 days after the announcement.

### Step 5: Score and optimize both pieces
```
/optimize [paste announcement post]
/optimize [paste thread opener]
```
Catch any reach killers before publishing.

### Step 6: Schedule
```
/schedule announcement post for tech developers, EST timezone, this week
```
Post the announcement on Tuesday-Thursday at 9-10 AM ET. Thread the next day.

### Step 7: Post-launch engagement
- Reply to every comment within the first hour (75-150× multiplier)
- Quote-tweet interesting replies with additional context
- Drop the link in a reply to the announcement (not in the body)

### Step 8: Review performance (next day)
```
/review [paste engagement data from both posts]
```
Extract lessons for the next release announcement.

---

## Playbook: Weekly Content Pipeline

Sustainable 5-post-per-week workflow with 30-45 minutes of daily effort.

### Sunday evening (15 min): Plan the week
```
/strategy plan this week's content. Niche: [your niche]. Current goals: [goals].
```
Get 5 post ideas across your content pillars with suggested formats and timing.

### Monday (10 min): Research + hot take
```
/research what happened in [niche] over the weekend
/compose [hot take based on research findings]
```
Monday posts should be reactive — comment on something that happened over the weekend.

### Tuesday (15 min): Thread day
```
/thread [topic from weekly plan — deep dive or tutorial]
/media what visual should I include in this thread
```
Tuesday morning is prime thread time. Include at least one image in the thread.

### Wednesday (10 min): Quick tip
```
/compose quick actionable tip about [topic from weekly plan]
```
Wednesday is peak engagement day. Short, punchy, immediately actionable.

### Thursday (10 min): Community post
```
/compose poll or question about [niche topic from weekly plan]
```
OR quote-tweet someone in your niche with added insight.

### Friday (10 min): Build-in-public update
```
/compose weekly progress update: [what you shipped, learned, or struggled with]
```
Friday is lower engagement, which is fine for personal updates.

### Daily (5-10 min): Reply farming
- Reply to 10-15 posts in your niche before and after posting
- Reply to all comments on your own posts
- This is non-negotiable — it's the highest-leverage activity

---

## Playbook: Grow from 0 to 1,000 Followers

A 90-day structured growth plan for new accounts.

### Phase 1: Foundation (Days 1-14)
```
/strategy launch phase, [niche], 0-50 followers, goal: establish presence
```

**Daily actions:**
- Reply to 20-30 posts in your target niche (visibility building)
- Post 1 quality piece per day (use `/compose`)
- Follow 10-20 relevant accounts (peers, not celebrities)
- No self-promotion yet — earn attention through value

**Content focus:**
- Quick tips and observations (low-effort, high-value)
- Reply to popular posts with genuine insight (piggyback on their distribution)
- Use `/hooks` to nail the opening lines (critical at this stage)

### Phase 2: Consistency (Days 15-45)
```
/strategy growth phase, [niche], 50-200 followers, posting daily
```

**Weekly cadence:**
- 2-3 single posts per week (tips, observations, opinions)
- 1 thread per week (deeper content that demonstrates expertise)
- 15-30 minutes daily reply farming
- Start tracking what formats perform best (`/review`)

**Content leveling up:**
- Add screenshots/images to 50% of posts (`/media`)
- Start using `/optimize` on every draft before posting
- Begin repurposing: `/repurpose` best-performing posts into threads

### Phase 3: Authority (Days 46-90)
```
/strategy scale phase, [niche], 200-500 followers, building authority
```

**Weekly cadence:**
- Full weekly pipeline (see Weekly Content Pipeline playbook)
- `/research` weekly to stay on top of trending topics
- `/review` weekly to refine strategy based on data
- Start a recurring content series ("Weekly [Topic] Digest" or "[Day] Tips")

**Growth tactics:**
- Quote-tweet peers with added value (builds relationships + visibility)
- Cross-post threads to Reddit, HN, LinkedIn (drive external traffic)
- Collaborate: co-threads or shout-outs with similar-sized accounts
- Install OpenTweet (`/setup opentweet`) for scheduling and analytics

### Milestones to track
| Day | Target Followers | Target Avg Impressions |
|-----|-----------------|----------------------|
| 14 | 50-75 | 200-500 per post |
| 30 | 100-200 | 500-1,500 per post |
| 60 | 300-500 | 1,500-5,000 per post |
| 90 | 700-1,000 | 5,000-15,000 per post |

---

## Playbook: Repurpose a Blog Post

Turn one blog post into a week of X content.

### Step 1: Distill into a thread
```
/repurpose [paste blog post] → thread
```
The thread captures the 5-7 most compelling points from the blog.

### Step 2: Extract single-post angles
```
/repurpose [paste blog post] → give me 5 different single-post angles
```
Each post takes one insight from the blog and frames it uniquely:
- The insight (straight delivery)
- The contrarian (challenges conventional wisdom)
- The question (turns it into a discussion)
- The tip (frames as actionable advice)
- The story (frames as personal experience)

### Step 3: Create visual content
```
/media what visuals should I create from this blog post: [key findings]
```
Identify 2-3 images: a key chart/table, a before/after, a code snippet.

### Step 4: Schedule the content
```
/schedule I have 1 thread and 5 posts from a blog. Plan the week.
```
Suggested cadence:
- **Day 1**: Thread (the main piece)
- **Day 3**: Strongest single-post angle
- **Day 5**: Second angle
- **Day 8**: Third angle
- **Day 10+**: Remaining angles

### Step 5: Review and iterate
After the first 2-3 pieces are published:
```
/review how did the thread and first post perform? What angle resonated most?
```
Double down on the angle that performed best — create a follow-up thread or expanded post on that specific subtopic.

---

## Playbook: Recover from a Slump

Engagement has dropped. Posts are underperforming. What to do.

### Step 1: Diagnose
```
/review here are my last 10 posts with engagement data: [data]
```
Look for patterns:
- Did engagement drop suddenly (one bad post) or gradually (content drift)?
- Are reply rates low (weak CTAs) or impressions low (distribution penalty)?
- Have you been posting at different times?

### Step 2: Check for penalties
```
/optimize [paste your most recent post]
```
Check for reach killers you might have introduced:
- Links in body?
- Engagement bait?
- Off-topic content?
- Posting too frequently or at bad times?

### Step 3: Reset with high-quality content
Take 2-3 days off from posting. Then:
```
/compose [your strongest topic — the thing you know best]
```
Come back with your absolute best content. No promotion, no links, just pure value.

### Step 4: Rebuild with reply farming
For 2 weeks:
- 20-30 genuine replies per day in your niche
- 1 high-quality post every other day (quality > quantity)
- Reply to every comment on your posts
- Use `/optimize` on every draft — no post goes out without scoring 60+

### Step 5: Re-establish strategy
```
/strategy recovery mode, [niche], [current followers], rebuilding engagement
```
Get a fresh weekly plan focused on the content types that historically performed best for you.

---

## Playbook: Create Visual Content with Remotion

Generate programmatic video for recurring content.

### Step 1: Set up Remotion
```
/setup remotion
```

### Step 2: Define your template needs
Common templates for X content:
- **Benchmark race**: Animated bars showing speed comparison
- **Counter animation**: Number ticking up to impressive metric
- **Code reveal**: Syntax-highlighted code appearing line by line
- **Metrics dashboard**: Animated chart for weekly updates
- **Before/after split**: Visual transformation comparison

### Step 3: Create your first composition
```
/media create a Remotion benchmark race showing [Tool A] completing in [X]s vs [Tool B] in [Y]s, dark theme
```

Claude generates the React + Tailwind composition, you preview and render:
```bash
cd marketing
pnpm run dev              # Preview in browser (hot-reloads)
pnpm exec remotion render # Output to MP4
```

### Step 4: Create a template for recurring content
If you do weekly benchmark updates:
```
/media create a reusable Remotion template for weekly benchmark comparisons. Input: tool names and times. Output: 10-second bar race animation.
```

Save the template in `marketing/src/templates/` for reuse.

### Step 5: Integrate with posting workflow
```
/compose weekly benchmark update: [tool A] vs [tool B], new results
# Claude drafts the post
# Render the Remotion animation with new data
# Attach video to the post
```
