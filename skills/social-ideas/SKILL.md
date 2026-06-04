---
name: social-ideas
description: Generate ready-to-post Instagram and TikTok content for ARETE, the AI-powered life tracker. Use this skill whenever the user wants to create social media posts, content ideas, captions, scripts, carousels, slideshows, ad concepts, or any Instagram or TikTok content for ARETE. Also triggers for repurpose mode, content calendars, series arcs, launch sequences, cross-platform adaptation, and comment strategy. Invoke proactively whenever the user mentions posting, content, social media, Instagram, TikTok, hooks, captions, ads, series, or engagement in the context of ARETE.
---

# ARETE Social Content Skill

You are the orchestrator for a 3-agent content generation pipeline. Your job is to receive the user's command, check performance memory and pillar balance, then pass everything to Agent 1 → Agent 2 → Agent 3 in sequence.

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

## Step 2 — Route the command

| Command pattern | Route to |
|----------------|----------|
| Standard `/social-ideas` | Agent 1 → 2 → 3 pipeline |
| `series` | Read `references/series-mode.md`, then Agent 1 → 2 → 3 |
| `arc` | Read `references/story-arc.md`, then Agent 1 → 2 → 3 |
| `repurpose` | Read `references/cross-platform.md`, then Agent 1 → 2 → 3 |
| `comments` | Read `agents/comment-strategist.md`, execute directly |
| `calendar` | Read `references/series-mode.md` + `references/best-time-to-post.md`, Agent 1 → 2 → 3 |

## Step 3 — Check Performance Memory (Adaptive)

Read `data/post-log.json`. This is NOT a simple "use what's popular" system.

### What to pass to Agent 1:
- Which formats have been used and how often
- Which hook categories have been chosen
- Any skip reasons logged (format_skips, hook_skips)
- Any format signals built from previous skip reasons

### After output is delivered — ask about skips:
If the user doesn't use one of the generated posts or formats, ask:

> "I noticed you didn't use the [format] post — any reason? 
> (e.g., wrong topic for it, doesn't suit ARETE, just didn't need it today)"

Wait for their answer. Then log it:
- "wrong topic / timing" → tag as `situational` — still show this format, just pair it better
- "doesn't suit ARETE" or "off brand" → tag as `low-fit` — show less often, never remove entirely
- "just didn't need it today" or no clear reason → tag as `neutral` — no change
- "I hate this format" → tag as `low-fit`

**Never fully remove a format from suggestions.** Every format has a use case.
The goal is to understand the WHY, not just count the skips.

Update `data/post-log.json` with the reason under `skip_reasons.format_skips`
and update `format_signals.signals` accordingly.

## Step 4 — Check Pillar Balance

Read `data/pillar-log.json`. If any pillar has 0 posts in last 10, flag it:
> "Note: You haven't posted about [PILLAR] recently. Want me to work it in?"

Pillars: FITNESS · FAMILY · GOALS · FINANCE · HABITS · MINDSET · SLEEP · RELATIONSHIPS

## Step 5 — Run the pipeline

Pass to agents in sequence. Each agent reads their own instruction file:
- Agent 1: `agents/ideator.md`
- Agent 2: `agents/critic.md`
- Agent 3: `agents/compiler.md`

For `comments` command: execute `agents/comment-strategist.md` directly, skip pipeline.

## Step 6 — Update logs after output

Append to `data/post-log.json` and `data/pillar-log.json` with what was generated.

## Slide Count Rule (hard constraint at every stage)
- Default: 5-7 slides
- Absolute maximum: 10 slides, only when format research strongly supports it
- Never exceed 10. If content needs more, split into two posts.
