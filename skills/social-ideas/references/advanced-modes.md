# Advanced Modes — Series, Arc, Repurpose

Three special command modes beyond standard post generation.
SKILL.md routes to this file when it detects `series`, `arc`, or `repurpose` in the command.

---

## MODE 1 — SERIES
Connected multi-part posts released over consecutive days. Each post stands alone but rewards followers who watch the full arc. Builds return viewers and gives people a reason to follow.

**Command:**
```
/social-ideas series "[concept]" --parts N --platform [instagram/tiktok/both] --format [type]
```

**Arc structure (adapt based on part count):**
- Part 1: PROBLEM — name the pain, make them feel seen
- Part 2: AGITATION — deepen the stakes
- Part 3+: PROOF — what the solution looks like across different pillars
- Second-to-last: TURN — the shift in perspective
- Final: CALL — quiet invitation to act ("join the waitlist")

**Every part must:**
- Work completely standalone (score 7+ out of 10 on standalone rating)
- Contain a forward teaser: "Tomorrow: [what's next]"
- Contain a subtle callback to the previous part for returning viewers

**Naming convention for ARETE:** Use thematic titles, not numbered parts — they feel like a collection, not a checklist.
Example: "The star you forgot about" / "The star going dark" / "The star that feeds all the others"

**Series output includes per post:**
- All standard fields (hooks, copy, design, hashtags, audio)
- Series metadata block:
```
SERIES METADATA:
  Series: [name]
  Part: [N] of [total]
  Release day: Day [N]
  Connects to previous: [how]
  Forward teaser: [exact text]
  Standalone rating: [1-10]
```
- Full posting schedule at the end

**Design consistency across all parts:** Same background, font system, accent color, brand tag position, and a small series marker element (e.g., ✦✦✦ star count incrementing per part).

---

## MODE 2 — STORY ARC (LAUNCH SEQUENCE)
Multi-week narrative campaign building toward a specific moment — waitlist push, feature reveal, or milestone.

**Command:**
```
/social-ideas arc "[goal]" --weeks N --instagram N/week --tiktok N/week
```

**Standard 4-week arc:**

**Week 1 — Problem Awareness**
Goal: Make the audience feel the pain without mentioning the solution.
Tone: Empathetic, observational, "you're not alone."
Best formats: ugc-rant, vulnerability caption, trojan-horse, quote-drop
CTA: None, or very soft ("does this resonate?")

**Week 2 — Agitation**
Goal: Deepen the stakes. Show the cost of not solving the problem.
Tone: Honest, slightly uncomfortable.
Best formats: did-you-know, carousel (list), countdown, before-after
CTA: "Something is coming. Follow to see it first."

**Week 3 — Solution Hint**
Goal: Tease without fully revealing. Create anticipation.
Tone: Mysterious, confident.
Best formats: founder-story, aesthetic-mood, voiceover-broll, pov
CTA: "Waitlist is opening soon. Link in bio."

**Week 4 — Reveal & Push**
Goal: Full reveal. Drive waitlist signups. Exciting but still philosophical.
Best formats: did-you-know (features), carousel (product intro), ugc-rant, quote-drop
CTA: "Join the waitlist. Link in bio." — every single post.

**2-week version:** Compress Weeks 1+2 into Week 1, compress Weeks 3+4 into Week 2. Use for feature announcements.

**Arc output format:**
```
STORY ARC: [name]
Goal: [what this is building toward]
Duration: [N] weeks

WEEK 1 — [THEME]
  Monday:    [Post title] — [Platform] — [Format]
  Wednesday: [Post title] — [Platform] — [Format]
  ...

[Full post output for each]

ARC NARRATIVE THREAD:
  [One paragraph: emotional journey, how weeks connect, what follower feels by the end]
```

---

## MODE 3 — REPURPOSE (CROSS-PLATFORM ADAPTER)
Takes existing content and converts it to another platform's format. One idea, both platforms, no extra creative work.

**Command:**
```
/social-ideas repurpose "[paste post copy or describe it]" --from [format] --to [format]
```

If no post specified, find the most recent high-scoring post in `data/performance.json` and repurpose that. Tell the user which post was chosen.

**Conversion rules:**

### Instagram Carousel → TikTok Slideshow
- Canvas: 1080x1350 → 1080x1920
- Slides: may reduce by 1-2 (TikTok needs faster pace)
- Text per slide: condense to single most powerful line
- CTA: "Save this" → "Comment below" or "Follow"
- Remove any slide that doesn't survive compression

### TikTok Script → Instagram Caption
- Spoken hook → opening 10-12 words of caption
- Script middle → storytelling paragraphs (150-300 words)
- On-screen text → carousel overlay or Reel text
- CTA: "Follow" → "Save this" or "Link in bio"

### Instagram Caption → TikTok Script
- Written paragraphs → spoken beats with [pause] markers
- Formal phrasing loosened for speech
- Add on-screen text callouts for key lines

### TikTok Slideshow → Instagram Carousel
- Canvas: 1080x1920 → 1080x1350
- Add 1-2 slides (Instagram rewards more depth)
- Expand final CTA slide
- Replace comment bait with save trigger

### Any Format → Instagram Story Ad
Always condenses to: 1 headline (8 words max) + 1 subheadline (12 words max) + 1 interactive element + 1 CTA button ("Join Waitlist"). If the core message can't survive this reduction, flag it — the message isn't sharp enough.

**Repurpose output format:**
```
REPURPOSE: [original format] → [target format]
Original concept: [one line]

WHAT CHANGED:
  [Bullet list of every adaptation made and why]

[Full post output in target format]
```
