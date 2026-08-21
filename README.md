# Free Claude Marketing Skills

**13 free Claude marketing skills for Claude Code**, covering SEO, keyword research, content strategy, listicles, landing pages, web design, social captions, and the quality gates that catch AI slop before it ships.

Every skill is a single markdown file. No accounts, no build step, no vendor lock-in. They work in Claude Code, and anywhere else that reads the [Agent Skills format](https://code.claude.com/docs/en/skills).

Built and used daily by [Ryan Doser](https://ryandoser.com), an AI-first marketer running SEO and content for real clients. These are the actual files, not demos.

## Why these are different

Most free marketing skill packs are prompt collections with a new name. These carry the operating rules that come from shipping client work:

- **`anti-spam`** checks a draft against your *existing* posts for the scaled-content patterns search engines penalize. Almost nothing else does cluster-level checks.
- **`keyword-research`** treats a zero-volume result as an index gap rather than a verdict, and separates domain, page, and **brand** competition, the third of which decides AI visibility.
- **`listicle-blog-post-writer`** encodes the guardrails from ClickUp's 97.6% traffic collapse so your roundups don't read as templated.
- **`careful-marketer`** is a disposition, not a task: verify before claiming, stay in scope, stop and ask.

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

Each skill must end up as **its own folder containing a `SKILL.md`**. The folder name becomes the command you type, so `anti-slop/SKILL.md` gives you `/anti-slop`. If you see one lone `SKILL.md` in your skills directory instead of thirteen folders, a trailing slash in a `cp` glob flattened them. Re-copy using the command above.

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

## Free Claude Marketing Skills FAQs

### What are Claude marketing skills?

Claude marketing skills are markdown files that give Claude specialized marketing knowledge and workflows. Each skill is a folder containing a `SKILL.md` with YAML frontmatter describing when to use it. When a request matches that description, Claude loads the file and follows its rules. Unlike a saved prompt, a skill is versioned, editable, and reusable across every project.

### Are Claude skills free?

The skill format is free and open, and the 13 in this repo are free under the MIT license. What costs money is the Claude plan you run them on. Skills work in Claude Code, which requires a paid plan: Pro at $20/month billed monthly ($17 on annual), or Max from $100/month. Verified against Claude's pricing page in August 2026, so check it for current figures.

### Can I use Claude skills on the free plan?

Not in Claude Code. Claude's Free tier does not include Claude Code, so it will not run these. The skill files themselves cost nothing to download, read, and adapt, and the frameworks inside them are readable by a human regardless of plan.

### How do I install Claude marketing skills?

Copy each skill folder into `~/.claude/skills/` to use it in every project, or into `.claude/skills/` inside a single project. Restart Claude Code and run `/skills` to confirm they loaded. Each skill has to keep its own folder, because the folder name becomes the command you type. Full commands are in the Install section above.

### Can I use Claude for marketing?

Yes, and skills are what make it reliable. Out of the box Claude gives generic marketing advice and will state things confidently that are not true. A skill supplies the frameworks, the banned-word lists, the verification steps, and the quality gates, so the output follows a process instead of guessing. The gate skills here (`anti-slop`, `anti-spam`) exist specifically to catch what the model gets wrong.

### Which free AI is best for marketing?

For skill-based marketing work, Claude Code is the strongest option because the skill format lets you correct the model permanently instead of re-prompting. ChatGPT and Gemini have their own custom-instruction systems but do not read the Agent Skills format natively. That said, no model is a silver bullet, and any marketing output still needs a human review pass.

### Do these work with Cursor, Codex, or other agents?

They are plain markdown following the Agent Skills format, so any agent that reads that format can use them. They were written and tested against Claude Code, so treat other agents as untested rather than guaranteed.

### Can I use these commercially or in client work?

Yes. MIT licensed, so you can use them commercially, modify them, and ship them inside your own products. `skill-creator` is the one exception, derived from Anthropic's original and licensed Apache 2.0. Attribution is appreciated but not required.


## Want more?

These thirteen are the ones I give away. The full library I actually run my business on, 40+ skills covering SEO, YouTube, email, social, and web design, lives at [skills.ryandoser.com](https://skills.ryandoser.com).

I am [Ryan Doser](https://ryandoser.com). I make AI and marketing videos on [YouTube](https://youtube.com/@RyanDoserAI) and I use every one of these skills daily.

Found a bug or want a skill improved? [Open an issue](https://github.com/rdoser13/free-claude-skills/issues).

## License

MIT. Use them commercially, modify them, ship them in your own products. Attribution appreciated, not required.

One exception: **`skill-creator`** is derived from [Anthropic's skill-creator](https://github.com/anthropics/skills) and remains under Apache License 2.0. It has been modified to be self-contained (its packaging and init scripts were rewritten as manual steps).
