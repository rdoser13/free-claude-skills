# Free Claude Skills

A library of free [Claude Skills](https://code.claude.com/docs/en/skills) I use in my own marketing work: writing, SEO, landing pages, social captions, and the quality gates I run before anything ships.

Every skill here is evergreen and brand-agnostic. Nothing is tied to my sites, my clients, or my data. Fork it, rename things, make it yours.

Skills are just markdown. When Claude gets something wrong, you open the file, fix the rule, and it stops making that mistake. That feedback loop is the whole reason the format is worth learning.

## Install

Each folder is one skill. Drop the folder into your skills directory:

```bash
git clone https://github.com/rdoser13/free-claude-skills.git

# All of them, for every project:
cp -r free-claude-skills/*/ ~/.claude/skills/

# Or just one, for a single project:
cp -r free-claude-skills/anti-slop .claude/skills/
```

Restart Claude Code, then run `/skills` to confirm they loaded.

## Try one in 30 seconds

Install `anti-slop`, paste in any AI-written paragraph, and say:

> Run anti-slop on this.

You get back every flagged word and structural tell, plus a clean rewrite. That is the shortest path to understanding what a skill actually is.

## The skills

| Skill | What it does |
|---|---|
| [`skill-creator`](skill-creator/) | The skill that writes other skills. Describe what you want and it builds a properly structured `SKILL.md` for you. Start here. |
| [`setting-up-mcps`](setting-up-mcps/) | Walks you through connecting Claude Code to external tools via MCP (GitHub, Notion, Sheets, Slack, databases) and debugs the connection when it breaks. |
| [`anti-slop`](anti-slop/) | Catches AI-generated fluff at the sentence level. Banned word lists, structural red flags, and rewrite patterns. |
| [`anti-spam`](anti-spam/) | The gate `anti-slop` cannot be. Checks a draft against your *existing* posts for scaled-content patterns that search spam policies target: duplicated skeletons, repeated heading templates, publish bursts, uniform commercial footprints. Six pass/fail gates. |
| [`landing-page-designer`](landing-page-designer/) | Builds a focused single-page landing page in deployable HTML/CSS, using a proven anatomy instead of a homepage with a button stapled on. |
| [`skill-auto-improve`](skill-auto-improve/) | Grades other skills' output against their own rules and proposes a patch to the skill file once the same failure repeats. Your usage becomes the test suite. |
| [`linkedin-profile-scraper`](linkedin-profile-scraper/) | Pulls a public LinkedIn profile's posts via Apify and exports a clean CSV with engagement scoring. Requires an Apify token. |
| [`seo-content-strategy`](seo-content-strategy/) | Builds a prioritized content plan for any site. Scores topics by intent and conversion probability, maps clusters, and tells you what to publish next. Bottom-funnel first. |
| [`social-media-manager`](social-media-manager/) | Turns one video or image into platform-optimized captions for YouTube, TikTok, Instagram, Threads, LinkedIn, X, Facebook, and Pinterest. Two-caption system with hard character-limit enforcement. Works with any scheduler. |
| [`careful-marketer`](careful-marketer/) | Not a task skill, an operating mindset. Makes the agent ground in real data before writing, verify claims before citing them, stay in scope, and stop to ask instead of guessing. |

## What each one needs from you

Nine of the ten run as-is with no account, no key, and no external service.

- **`linkedin-profile-scraper`** is the exception. It calls [Apify](https://apify.com), so it needs an API token in `$APIFY_API_TOKEN` or pasted when it asks. The profile URL you give it is sent to Apify. It is the only skill here that talks to a third party.
- **`social-media-manager`** and **`seo-content-strategy`** have `[BRACKETED_PLACEHOLDERS]` for brand voice, platforms, and audience. Fill them in once and they are yours.
- **`skill-auto-improve`** is the only skill that proposes edits to other skill files. Review its suggested patches before accepting them, and keep your skills in git so anything it touches is revertable.

## Want more?

These ten are the ones I give away. The full library I actually run my business on, 40+ skills covering SEO, YouTube, email, social, and web design, lives at [skills.ryandoser.com](https://skills.ryandoser.com).

I am [Ryan Doser](https://ryandoser.com). I make AI and marketing videos on [YouTube](https://youtube.com/@RyanDoserAI) and I use every one of these skills daily.

Found a bug or want a skill improved? [Open an issue](https://github.com/rdoser13/free-claude-skills/issues).

## License

MIT. Use them commercially, modify them, ship them in your own products. Attribution appreciated, not required.
