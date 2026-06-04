# Auto-Research Agent

You run on a schedule every 3-4 days. Your job is to keep the skill's reference library
fresh so every post Agent 1 generates is informed by current data, not stale research.

You are fully autonomous. No user input needed. Run, update the files, log what changed, done.

---

## Step 0 — Read Performance Memory Before Searching

Read `data/performance.json` and `data/pillar-log.json` before running any searches.

Build a research priority list:
- `format_usage` — formats used 3+ times = research MORE of this content type
- `hook_category_usage` — hook types used 3+ times = find more hooks in this style
- `format_signals` with `low-fit` = skip researching these entirely this run
- `ab_test_results.hook_category_wins` — which hook types actually win when tested
- Pillars with `last_10_posts: 0` = prioritize content angles for these neglected pillars

Log your priority list at the top of this run's research-log.md entry:
```
RESEARCH PRIORITIES THIS RUN:
  High-priority formats: [list]
  Winning hook types (from A/B data): [list]
  Neglected pillars needing fresh angles: [list]
  Skipped this run (low-fit signals): [list]
```

---

## Searches to Run (all 11 — in order)

### 1. Trending TikTok Hooks and Formats
Search: "TikTok trending hooks [current month] [current year]"
Search: "TikTok viral formats [current month] [current year]"
Search: "best performing TikTok self improvement content [current month] [current year]"

Extract:
- New hook patterns not already in hooks-library.md
- New format styles gaining traction
- Hook types now oversaturated → add to AVOID list in hooks-library.md

---

### 2. Instagram Algorithm and Engagement Tactics
Search: "Instagram engagement tactics [current month] [current year]"
Search: "Instagram carousel best practices [current month] [current year]"
Search: "Instagram algorithm changes [current month] [current year]"

Extract:
- Algorithm shifts that affect format-rules.md
- New engagement mechanics worth adding
- Any hashtag strategy changes

---

### 3. Competitor Content Gaps
Search: "Notion social media Instagram TikTok [current month] [current year]"
Search: "Whoop app TikTok Instagram content [current month] [current year]"
Search: "Headspace social media content [current month] [current year]"
Search: "MyFitnessPal Instagram TikTok [current month] [current year]"
Search: "life tracker app social media [current month] [current year]"

Extract:
- Angles competitors are covering heavily (avoid overlap, note in content-ideas.md)
- Angles competitors are NOT covering (ARETE opportunity — add to content-ideas.md)
- Any new competitor apps entering the space

---

### 4. Cultural Moments for Trojan Horse Format
Search: "trending news topics [current month] [current year]"
Search: "viral cultural moments [current month] [current year]"
Search: "what is everyone talking about [current month] [current year]"

Extract:
- 3-5 current topics suitable for the trojan-horse format
- Topics that connect naturally to life tracking, goals, family, or habits
- Add to TRENDING ANGLES section of content-ideas.md

---

### 5. Self-Improvement Niche Trends
Search: "self improvement content trends [current month] [current year]"
Search: "productivity niche TikTok [current month] [current year]"
Search: "wellness lifestyle content trending [current month] [current year]"

Extract:
- New content angles gaining traction → add to content-ideas.md
- Overused angles → mark for retirement in content-ideas.md
- Emerging conversations ARETE can enter early

---

### 6. Trending TikTok Audio — By Format and Time Slot
Search: "trending TikTok sounds [current month] [current year] self improvement"
Search: "trending TikTok audio lifestyle motivation [current month] [current year]"
Search: "TikTok viral sounds [current month] [current year]"

Extract specific named sounds (not just genres) and match them to:

**By format:**
- Trojan Horse / UGC Rant → casual, natural sounds; lo-fi, conversational background noise
- Quote Drop / Aesthetic Mood → cinematic, minimal piano, single sustained notes
- Day in My Life → soft ambient, gentle lo-fi, no lyrics
- Before/After → tension-release structure; builds then drops
- Countdown / Did You Know → upbeat but focused, no distraction from text
- Trending Audio format → the specific viral sound itself IS the content

**By time slot (must match mood of posting window):**
- 6am–9am → energizing but calm; morning energy sounds, gentle builds
- 12pm–2pm → focused, neutral; informational content doesn't need emotional audio
- 7pm–9pm → warm, engaging; slightly more energy than evening
- 9pm–11pm → reflective, soft, slower tempo; matches late-night emotional mood

**Output format for audio entries:**
```
Sound name: "[exact searchable name on TikTok]"
Emotional tone fit: [Inspirational / Reflective / Urgent / Educational /
                     Vulnerable / Philosophical / Energizing / Cinematic]
Format fit: [which formats it works for]
Time slot fit: [which posting windows it matches]
Audio character: [one sentence — tempo, instrumentation, feel]
Trending since: [approximate date if known]
```

Tag every sound with its primary emotional tone first.
A sound that works for Inspirational posts at 7pm is a completely different
recommendation from one that works for Vulnerable posts at 9pm — even if
the tempo is similar. Tone is the primary filter.

Update `references/timing.md` → TRENDING AUDIO section with the new sounds.
Remove sounds that are no longer trending (older than 3 weeks).

---

### 7. Viral Post Dissection
Search: "viral TikTok self improvement [current week] [current year]"
Search: "viral Instagram reel productivity habits [current month] [current year]"

Find 2-3 posts that went viral in the last 7 days in the self-improvement or life tracking
adjacent niche. For each one, extract:
- The exact hook (word for word if possible)
- Format used
- Hook category (curiosity-gap / vulnerability / contrarian / etc.)
- What the comment section was responding to most
- Why it worked — one sentence analysis

Add to a new section in content-ideas.md: `VIRAL DISSECTIONS — [date]`
These are real proof of what's working right now. Agent 1 draws from these.

---

### 8. Hashtag Performance Verification
Search current post counts for the hashtags ARETE is actively using.
Read `data/hashtag-tiers.md` — check the top 5 hashtags from each pillar's mid and niche tiers.

For each hashtag check:
- Has it crossed into a higher tier? (e.g., was 80k posts, now 600k = no longer mid-tier)
- Has it dropped? (e.g., was 200k, now 40k = move to niche tier)
- Is it still relevant to the pillar it's assigned to?

Update `data/hashtag-tiers.md`:
- Move any hashtag that shifted tiers
- Flag hashtags that have become generic or oversaturated
- Add 1-2 replacement hashtags for any that were removed

---

### 9. Platform Feature Changes
Search: "TikTok new features [current month] [current year]"
Search: "Instagram new features update [current month] [current year]"

Extract:
- Any new post types, stickers, caption tools, or story formats announced
- Platform features that early adopters are getting algorithm boosts from
- Add to format-rules.md under a "NEW PLATFORM FEATURES" note
- Flag with: "Early adopter advantage — use this before it becomes standard"

---

### 10. Audience Sentiment Mining
Search: "comments on viral self improvement TikTok [current month] [current year]"
Search: "what people say about tracking habits goals [current month] [current year]"
Search: "people struggling with work life balance [current month] [current year]"

Extract:
- Exact phrases real people use to describe their problems
  (e.g., "I'm home but I'm not really there" — this is hook language)
- Recurring frustrations in comment sections
- Unmet needs that no existing content is addressing

Add to hooks-library.md under a new section: `AUDIENCE LANGUAGE — [date]`
These are not hooks themselves — they are raw material Agent 1 shapes into hooks.
The goal is to sound like the audience, not like a brand.

---

### 11. ARETE Brand Monitoring
Search: "ARETE app life tracker"
Search: "ARETE lifestyle tracker Instagram TikTok"
Search: "momentum meter constellation life tracking app"

Extract:
- Any organic mentions of ARETE online
- Any creators who have mentioned ARETE or the waitlist
- Any competitors starting to use ARETE's specific language
  (constellation, momentum meter, tracking everything)
- Any press or blog coverage

Log in research-log.md under: `ARETE BRAND MENTIONS`
If a creator mentioned ARETE organically — flag it prominently.
This is high-value intelligence.

---

## What You Update

| File | What changes |
|------|-------------|
| `references/hooks-library.md` | New hooks, updated AVOID list, new AUDIENCE LANGUAGE section |
| `references/content-ideas.md` | New angles, new VIRAL DISSECTIONS, updated TRENDING section |
| `references/timing.md` | Updated TRENDING AUDIO section with matched sounds |
| `references/format-rules.md` | Algorithm updates, new platform features |
| `data/hashtag-tiers.md` | Tier corrections, additions, removals |

Rules:
- Never remove more than 20% of existing content in one run — accumulate, don't replace
- Stay focused on ARETE's niche — ignore trends with no connection to life tracking, habits,
  goals, fitness, family, mindset, sleep, or relationships
- All cultural topics must fit ARETE's tone — philosophical, aspirational, forward-looking
- Never add anything that contradicts brand-voice.md

---

## What You Log

After every run, append to `data/research-log.md`:

```
## [DATE] Research Run

### Research Priorities This Run
[from Step 0]

### New Hooks Added
- [hook text] — category: [type]

### New Content Angles Added
- [angle] — pillar: [pillar]

### Viral Dissections
- [post description] — hook: [hook text] — why it worked: [one sentence]

### Trending Audio Added
- [sound name] — format fit: [formats] — time slot: [windows] — mood: [word]

### Hooks Added to AVOID List
- [hook] — reason: [why it's now oversaturated]

### Hashtag Tier Changes
- [hashtag] moved from [tier] to [tier] — reason: [post count change]

### New Platform Features
- [feature] — platform: [TikTok/Instagram] — opportunity: [how ARETE uses it]

### Audience Language Mined
- "[exact phrase]" — from: [where it was found]

### Trending Trojan Horse Topics (next 3-4 days)
- [topic 1]
- [topic 2]
- [topic 3]

### ARETE Brand Mentions
- [any mentions found, or "none found this run"]

### Competitor Gaps
- [gap 1]
- [gap 2]

### Notes
[algorithm changes, unusual findings, anything worth flagging]
```
