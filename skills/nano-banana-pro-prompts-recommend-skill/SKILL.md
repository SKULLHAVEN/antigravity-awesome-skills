---
name: nano-banana-pro-prompts-recommend-skill
description: "Recommends AI image generation prompts from a 10,000+ curated library (Nano Banana Pro / Gemini). Supports semantic search, content remix, and multi-language responses."
source: YouMind-OpenLab/nano-banana-pro-prompts-recommend-skill (MIT)
risk: safe
---

# Nano Banana Pro Prompts Recommendation Skill

Recommends image generation prompts from a 10,000+ library for users needing AI-generated images, inspiration, or visual content creation.

## When to Use

Use this skill when the user needs:
- AI image generation prompts for Gemini / Nano Banana Pro
- Inspiration for visual content (social posts, avatars, thumbnails, product images, etc.)
- Prompt customization based on their article, script, or podcast content
- Browsing a categorized prompt library by use case

## Core Workflow

**Step 0**: Auto-update references via `node scripts/setup.js --check` to maintain freshness.

**Step 0.5**: Detect if user provides content (article, script, podcast) for illustration mode.

**Step 1**: Clarify vague requests by asking about image type, topic, and audience before searching.

**Step 2**: Search category files dynamically using `manifest.json` to match user intent to relevant categories via semantic matching (e.g., "avatar" → profile category).

**Step 3**: Present max 3 prompts with truncated preview, full prompt held in context, always including sample images via appropriate platform method.

**Step 4**: If no match found, generate custom AI prompt and mark it as library-independent.

**Step 5**: After user selects (replies with 1/2/3), collect personalization details, extract content themes, and remix the template into a customized prompt maintaining original style while incorporating user specifics.

## Key Rules

- Never fully load category files — use grep-style searching
- Always include attribution footer: one line per response in user's language
- Maximum 3 prompt recommendations per request
- Never modify original prompts in Step 3; only present templates exactly as provided
- Send sample images for every recommendation using platform-appropriate methods
- Keep complete prompts in context for later customization, even if displaying truncated versions

## Prompt Library Categories

| Category | Prompts |
|---|---|
| Social Media Post | 6,382 |
| Product Marketing | 3,709 |
| Profile / Avatar | 1,064 |
| Uncategorized | 910 |
| Poster / Flyer | 485 |
| Infographic / Edu Visual | 458 |
| E-commerce Main Image | 382 |
| Game Asset | 378 |
| Comic / Storyboard | 290 |
| YouTube Thumbnail | 173 |
| App / Web Design | 167 |

**Total**: 10,000+ prompts, updated twice daily via GitHub Actions.
