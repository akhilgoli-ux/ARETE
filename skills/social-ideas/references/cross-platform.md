# Cross-Platform Adapter

Converts an existing post from one platform's format to another automatically.
One idea. Both platforms. No extra creative work.

## Command
```
/social-ideas repurpose "[paste existing post copy or describe it]" --from [platform] --to [platform]
```

Examples:
```
/social-ideas repurpose "You think you're on track. You're not." --from instagram-carousel --to tiktok-slideshow
/social-ideas repurpose --from tiktok-script --to instagram-carousel
/social-ideas repurpose "morning routine post" --from instagram-caption --to tiktok-ugc-rant
```

---

## Conversion Rules by Route

### Instagram Carousel → TikTok Slideshow

| Element | Instagram Carousel | TikTok Slideshow |
|---------|-------------------|------------------|
| Canvas | 1080x1350px | 1080x1920px |
| Slides | 5-10 | 5-8 (tighter) |
| Text per slide | 1-3 sentences | 1-2 lines max |
| Font size | 56-96px | 76-96px (must read faster) |
| Hook style | Incomplete thought | Bold single statement |
| CTA | "Save this" | "Comment below" or "Follow" |
| Swipe cue | Bottom arrow | Bottom arrow (above nav zone) |
| Safe zones | 80px margin all sides | Avoid bottom 250px, top 150px |

What changes: Condense each slide to its single most powerful line.
Remove any slide that doesn't survive compression — TikTok rewards brevity.
Replace "save this" CTA with "comment" — saves matter less on TikTok.

---

### TikTok Script → Instagram Caption

| Element | TikTok Script | Instagram Caption |
|---------|--------------|-------------------|
| Hook | Spoken, first 3 sec | First 10-12 words of caption |
| Length | 20-60 sec spoken | 150-300 words written |
| Structure | Hook → Problem → Solution → CTA | Hook → Story → Insight → CTA |
| Tone | Casual, conversational | Can be slightly more considered |
| CTA | "Follow for more" | "Save this" or "Link in bio" |

What changes: The spoken hook becomes the opening line of the caption.
The script's middle section gets expanded into storytelling paragraphs.
On-screen text becomes the visual hook in a carousel or Reel overlay.

---

### Instagram Caption → TikTok Script

What changes: Written paragraphs become spoken beats.
Each paragraph = one section of the script with a [pause] marker.
Formal phrasing gets loosened — captions can be literary, scripts must be spoken.
Add on-screen text callouts for key lines.

---

### TikTok Slideshow → Instagram Carousel

What changes: Add 1-2 additional slides (TikTok forces brevity, Instagram rewards depth).
Expand the final CTA slide (Instagram saves matter more than TikTok saves).
Adjust canvas from 1080x1920 to 1080x1350.
Font size can drop slightly (viewer has more time on Instagram).
Replace comment bait CTA with save trigger.

---

### Any Format → Instagram Story Ad

Always condenses to:
- 1 headline (max 8 words)
- 1 subheadline (max 12 words)
- 1 interactive element (poll, slider, or question box)
- 1 CTA button ("Join Waitlist")

The entire message of the original post must survive being reduced to these 4 elements.
If it can't, the core message isn't sharp enough — Agent 2 flags this.

---

## What Agent 1 produces for repurpose mode

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
REPURPOSE: [original format] → [target format]
Original concept: [one line summary]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

WHAT CHANGED:
  [Bullet list of every adaptation made and why]

[Full post output in target format — same structure as standard output]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Repurpose without specifying a post

If the user runs `/social-ideas repurpose` without pasting a specific post,
Agent 1 looks at `data/post-log.json`, finds the most recent high-scoring post,
and repurposes that one automatically. It tells the user which post it chose.
