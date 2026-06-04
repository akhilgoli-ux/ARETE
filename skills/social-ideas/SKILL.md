---
name: social-ideas
description: Generate ready-to-post Instagram and TikTok content for ARETE, the AI-powered life tracker. Use this skill whenever the user wants to create social media posts, content ideas, captions, scripts, carousels, slideshows, ad concepts, or any Instagram or TikTok content for ARETE. Also triggers for repurpose mode, content calendars, series arcs, launch sequences, cross-platform adaptation, and comment strategy. Invoke proactively whenever the user mentions posting, content, social media, Instagram, TikTok, hooks, captions, ads, series, or engagement in the context of ARETE.
---

# ARETE Social Content Skill

You are the orchestrator for a 3-agent content generation pipeline. Your job is to receive the user's command, run pre-flight checks, then pass everything to Agent 1 → Agent 2 → Agent 3 in sequence.

## Commands

```
# Standard post generation
/social-ideas [topic] --instagram N --tiktok N --format [type or number]

# Series (connected multi-part posts)
/social-ideas series "[concept]" --parts N --platform [instagram/tiktok/both] --format [type]

# Launch arc (multi-week narrative campaign)
/social-ideas arc "[goal]" --weeks N --instagram N/week --tiktok N/week

# Repurpose existing content across platforms
/social-ideas repurpose "[post copy or description]" --from [format] --to [format]

# Organic comment strategy
/social-ideas comments --platform [tiktok/instagram] --count N

# Content calendar
/social-ideas calendar --weeks N --instagram N/week --tiktok N/week
```

---

## Step 1 — Show Format Menu (if --format missing or user types --format ?)

```
┌─────────────────────────────────────────────────────────────┐
│  SELECT A FORMAT                                            │
│                                                             │
│  ── NARRATIVE ──────────────────────────────────────────    │
│  1.  trojan-horse      Trending topic → casual product drop │
│  2.  ugc-rant          Phone-quality rant, zero polish      │
│  3.  story-time        Emotional narrative arc, 45-60 sec   │
│  4.  founder-story     Why ARETE exists, personal/human     │
│                                                             │
│  ── LIFESTYLE ──────────────────────────────────────────    │
│  5.  day-in-my-life    Real day slideshow, app shown nat.   │
│  6.  voiceover-broll   No face, lifestyle footage + narr.   │
│  7.  before-after      15 sec split, subtle transformation  │
│                                                             │
│  ── EDUCATIONAL ────────────────────────────────────────    │
│  8.  did-you-know      Stat drop → problem → ARETE fix      │
│  9.  myth-vs-reality   Common assumption flipped on head    │
│  10. countdown         Numbered list, one point per slide   │
│                                                             │
│  ── REACTION / COMMENTARY ──────────────────────────────    │
│  11. green-screen      React to real stat/headline/tweet    │
│  12. comment-reply     TikTok reply to a real comment       │
│                                                             │
│  ── ENGAGEMENT-FIRST ───────────────────────────────────    │
│  13. pov               "POV: you finally track your life"   │
│  14. duet-bait         Ends on open Q, designed to stitch   │
│                                                             │
│  ── AUDIO / VISUAL ─────────────────────────────────────    │
│  15. trending-audio    Text timed to trending TikTok sound  │
│  16. quote-drop        Philosophical fade-in, pure black    │
│  17. aesthetic-mood    No copy, pure brand visual identity  │
│                                                             │
│  ── STATIC / DESIGNED ──────────────────────────────────    │
│  18. carousel          Instagram, 5-7 slides (max 10)       │
│  19. static-ad         Poster/Story, full design spec       │
│                                                             │
│  ── SMART ──────────────────────────────────────────────    │
│  20. auto              Agent 1 picks best format for topic  │
└─────────────────────────────────────────────────────────────┘
```

---

## Step 2 — Route the command

| Command pattern | Route to |
|----------------|----------|
| Standard `/social-ideas` | Steps 3-6, then pipeline |
| `series` / `arc` / `repurpose` | Read `references/advanced-modes.md`, then pipeline |
| `comments` | Read `agents/comment-strategist.md`, execute directly, skip pipeline |
| `calendar` | Read `references/advanced-modes.md` + `references/timing.md`, then pipeline |

---

## Step 3 — Performance Memory Check (Adaptive)

Read `data/performance.json`.

**Pass to Agent 1:**
- Format usage counts and format signals (situational / low-fit / neutral)
- Hook category usage and A/B test results (which hook categories win most per format)
- Feed rhythm data (last 10 formats, hook categories, emotional tones, pillars)

**A/B tracker — ask after output:**
After delivering posts, ask once:
> "When you use these — let me know which hook variant (A, B, or C) you went with.
> I'll log it to sharpen future suggestions."

When they answer, update `ab_test_results` in performance.json:
- Increment `variant_chosen.[A/B/C]`
- Identify the hook category of the chosen variant
- Increment `hook_category_wins.[category]`
- Increment `format_hook_wins.[format].[category]`

**Skip tracking — ask if a post goes unused:**
> "I noticed you didn't use the [format] post — any reason?"

Log the response:
- "wrong topic / timing" → `situational` — still show, pair better next time
- "doesn't suit ARETE" / "off brand" → `low-fit` — show less, never remove
- "just didn't need it" → `neutral` — no change
- "I hate this" → `low-fit`

Never fully remove a format. The goal is to understand WHY, not just count skips.

---

## Step 4 — Feed Rhythm Check

Read `performance.json` → `feed_rhythm.last_10_formats` and `last_10_hook_categories`.

Flag and tell the user if:
- Same format appears 3+ times in last 10 → "Your last few posts have been heavy on [format] — mixing in a [different format] would balance the feed."
- Same hook category appears 4+ times in last 10 → "You've been leading with [hook type] a lot — consider a [different hook type] for variety."
- Same emotional tone 3+ times in row → "Feed is running [tone] heavy — a [contrasting tone] post would give it breathing room."
- Same pillar 3+ times in last 5 → "ARETE's brand covers everything — you've been in [pillar] a lot. Consider [neglected pillar]."

Don't block generation — just flag it and let the user decide.

---

## Step 5 — Pillar Balance Check

Read `data/pillar-log.json`. If any pillar shows `last_10_posts: 0`, flag it:
> "Note: You haven't posted about [PILLAR] recently. Want me to work it into one of today's posts?"

20 pillars across 5 groups:
BODY: FITNESS · NUTRITION · SLEEP · HEALTH
MIND: MINDSET · LEARNING · CREATIVITY · MENTAL_HEALTH
SOUL: GRATITUDE · PRESENCE · SPIRITUALITY · PURPOSE
PEOPLE: FAMILY · RELATIONSHIPS · COMMUNICATION · SERVICE
LIFE: GOALS · FINANCE · HABITS · ENVIRONMENT

---

## Step 6 — Seasonal Check

Read `references/timing.md` → seasonal calendar.
If any seasonal moment is within 14 days, tell Agent 1 to include one seasonally-aware post option in the batch. Label it `SEASONAL: [moment name]` in metadata.

---

## Step 7 — Run the pipeline

- Agent 1: `agents/ideator.md`
- Agent 2: `agents/critic.md`
- Agent 3: `agents/compiler.md`

---

## Step 8 — Update logs after output

Update `data/performance.json` → feed_rhythm arrays (shift new entries in, drop oldest if over 10).
Update `data/pillar-log.json` → increment pillars used, update last_10_posts counts.

---

## Slide Count Rule (enforced at every stage)
- Default: 5-7 slides
- Absolute maximum: 10 slides, only when format research strongly supports it
- Never exceed 10. Split into two posts instead.
