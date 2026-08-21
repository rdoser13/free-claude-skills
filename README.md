# Free Claude Skills

A library of free [Claude Skills](https://code.claude.com/docs/en/skills) I use in my own marketing work: writing, SEO, keyword research, landing pages, web design, social captions, and the quality gates I run before anything ships.

Every skill here is evergreen and brand-agnostic. Nothing is tied to my sites, my clients, or my data. Fork it, rename things, make it yours.

Skills are just markdown. When Claude gets something wrong, you open the file, fix the rule, and it stops making that mistake. That feedback loop is the whole reason the format is worth learning.

## Install

Each folder is one skill. Drop the folder into your skills directory:

```bash
git clone https://github.com/rdoser13/free-claude-skills.git
cd free-claude-skills

# All of them, available in every project:
mkdir -p ~/.claude/skills
cp -r anti-slop anti-spam careful-marketer keyword-research landing-page-designer \
      linkedin-profile-scraper listicle-blog-post-writer seo-content-strategy \
      setting-up-mcps skill-auto-improve skill-creator social-media-manager \
      web-designer ~/.claude/skills/

# Or just one, for a single project:
cp -r anti-slop /path/to/your-project/.claude/skills/
```

Restart Claude Code, then run `/skills` to confirm they loaded.

Each skill must end up as its own folder containing a `SKILL.md`, and **the folder name has to match the `name:` field inside the file** or it will not load. If you see one lone `SKILL.md` in your skills directory instead of thirteen folders, a trailing slash in a `cp` glob flattened them. Re-copy using the command above.

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
| [`keyword-research`](keyword-research/) | Turns a raw keyword dump into a filtered, scored, prioritized list. Relevance filtering, intent classification, the three-level competition model (domain, page, and brand), and sprint discipline so you get 25-50 real targets instead of 500. Written for the DataForSEO MCP. |
| [`seo-content-strategy`](seo-content-strategy/) | Builds a prioritized content plan for any site. Scores topics by intent and conversion probability, maps clusters, and tells you what to publish next. Bottom-funnel first. |
| [`listicle-blog-post-writer`](listicle-blog-post-writer/) | Writes "best of" roundups and alternatives posts. Per-item cards, at-a-glance tables, and the anti-templating guardrails drawn from the ClickUp collapse, so your roundup doesn't read as programmatic content. |
| [`web-designer`](web-designer/) | Builds distinctive frontend interfaces that avoid generic AI aesthetics. Includes the practical workflow: the "4 unique takes" approach, framework choices, and static deployment. |
| [`social-media-manager`](social-media-manager/) | Turns one video or image into platform-optimized captions for YouTube, TikTok, Instagram, Threads, LinkedIn, X, Facebook, and Pinterest. Two-caption system with hard character-limit enforcement. Works with any scheduler. |
| [`careful-marketer`](careful-marketer/) | Not a task skill, an operating mindset. Makes the agent ground in real data before writing, verify claims before citing them, stay in scope, and stop to ask instead of guessing. |

## What each one needs from you

Most run as-is with no account, no key, and no external service. Three touch a paid service, and only one of those is required:

- **`linkedin-profile-scraper`** needs an [Apify](https://apify.com) API token in `$APIFY_API_TOKEN` or pasted when it asks. The profile URL you give it is sent to Apify. This one does not work without it.
- **`social-media-manager`**, **`seo-content-strategy`**, and **`keyword-research`** have `[BRACKETED_PLACEHOLDERS]` for brand voice, platforms, audience, and approved topic categories. Fill them in once and they are yours.
- **`keyword-research`** is written against the **DataForSEO MCP** (pay-as-you-go, no subscription tier to clear). The filtering, scoring, and prioritization logic works with any keyword source, including a CSV export or a manual list, so swap the tool calls if you use something else.
- **`social-media-manager`** writes captions with no account required. If you also want it to *schedule* the posts, it works best with **Blotato**, which ships a hosted MCP server. Buffer, Publer, Metricool, Later, or a Make/Zapier bridge also work with more setup.
- **`skill-auto-improve`** is the only skill that proposes edits to other skill files. Review its suggested patches before accepting them, and keep your skills in git so anything it touches is revertable.

## Want more?

These thirteen are the ones I give away. The full library I actually run my business on, 40+ skills covering SEO, YouTube, email, social, and web design, lives at [skills.ryandoser.com](https://skills.ryandoser.com).

I am [Ryan Doser](https://ryandoser.com). I make AI and marketing videos on [YouTube](https://youtube.com/@RyanDoserAI) and I use every one of these skills daily.

Found a bug or want a skill improved? [Open an issue](https://github.com/rdoser13/free-claude-skills/issues).

## License

MIT. Use them commercially, modify them, ship them in your own products. Attribution appreciated, not required.

One exception: **`skill-creator`** is derived from [Anthropic's skill-creator](https://github.com/anthropics/skills) and remains under Apache License 2.0. It has been modified to be self-contained (its packaging and init scripts were rewritten as manual steps).
