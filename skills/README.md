# ARETE Skills

Claude Code skills shared across the ARETE team.

## Installation (one-time per person)

1. Clone this repo
2. Find your Claude Code skills folder:
   - **Windows:** `C:\Users\[yourname]\AppData\Roaming\Claude\skills\`
   - **Mac:** `~/.claude/skills/`
3. Copy any skill folder from `skills/` into that directory
4. Restart Claude Code — the skill is now available

## Available Skills

### `social-ideas` ⭐ Primary skill
Generates ready-to-post Instagram and TikTok content for ARETE using a 3-agent pipeline.

**Commands:**
```
/social-ideas [topic] --instagram N --tiktok N --format [type]
/social-ideas series "[concept]" --parts N --platform [instagram/tiktok/both]
/social-ideas arc "[goal]" --weeks N --instagram N/week --tiktok N/week
/social-ideas repurpose "[post]" --from [format] --to [format]
/social-ideas comments --platform [tiktok/instagram] --count N
/social-ideas calendar --weeks N --instagram N/week --tiktok N/week
```

**What it does:**
- 20 post formats (trojan horse, carousels, slideshows, ads, scripts, and more)
- 3-agent pipeline: Ideator → Critic → Compiler
- Full design specs for every visual post (font, size, color, position — everything)
- A/B hook variants per post
- 3-tier hashtag strategy per post
- Engagement reply templates
- Performance memory (learns your preferences over time)
- Content pillar balancer (tracks which life areas you've covered)
- Auto-research agent refreshes hooks and trends every 3 days

### `docx` — Word document creation
### `pdf` — PDF reading and manipulation  
### `pptx` — PowerPoint creation and editing
### `xlsx` — Excel/spreadsheet work

## Updating skills

When the `social-ideas` skill is updated (new hooks, trends, formats), pull the latest from this repo and re-copy the folder to your Claude Code skills directory.

The auto-research agent commits updates to this repo every 3 days automatically — so pulling regularly keeps your skill fresh.

## Questions

Contact Akhil or open an issue in this repo.
