# Free Claude Marketing Skills for Claude Code

**15 free Claude marketing skills for Claude Code**, covering SEO, keyword research, content strategy, CRO, landing pages, web design, short-form video, social captions, and the quality gates that catch AI slop before it ships.

Every skill is one folder with a `SKILL.md` file inside. No build step, no vendor lock-in, and only one skill needs a third-party account to work. They follow the [Agent Skills format](https://code.claude.com/docs/en/skills) and were built and tested in Claude Code.

Built by [Ryan Doser](https://ryandoser.com), an AI-first marketer who runs SEO and content for real clients. These are public versions of skills from that workflow, with placeholders where your own brand details go.

## At a glance

| | |
|---|---|
| Skills | 15 (SEO, content, CRO, social, video, web design, quality gates) |
| Cost | Free, MIT license (`skill-creator` keeps Anthropic's Apache 2.0 license) |
| Works in | Claude Code. Any Agent Skills reader should work, untested outside Claude Code |
| Needs a third-party account | Only `linkedin-profile-scraper` (an Apify token, and Apify's free tier covers small runs). `keyword-research` is written for DataForSEO but works with a CSV |
| Install time | About 30 seconds if Claude Code is already installed |

## Install in 30 seconds

**Easiest:** open Claude Code and paste this:

> Install the skills from https://github.com/rdoser13/free-claude-skills into ~/.claude/skills/, one folder per skill.

**Or by hand:**

```bash
git clone https://github.com/rdoser13/free-claude-skills.git
cd free-claude-skills

# All of them, available in every project:
mkdir -p ~/.claude/skills
cp -r anti-slop anti-spam careful-marketer cro-audit keyword-research \
      landing-page-designer linkedin-profile-scraper listicle-blog-post-writer \
      seo-content-strategy setting-up-mcps short-form-video-scripts \
      skill-auto-improve skill-creator social-media-manager web-designer \
      ~/.claude/skills/

# Or just one, for a single project:
mkdir -p /path/to/your-project/.claude/skills
cp -r anti-slop /path/to/your-project/.claude/skills/
```

Start a new Claude Code session, then run `/skills` to confirm they loaded.

Each skill must end up as **its own folder containing a `SKILL.md`**. The folder name becomes the command you type, so `anti-slop/SKILL.md` gives you `/anti-slop`. (`skill-auto-improve` is the exception: it runs in the background and has no command.) If you see one lone `SKILL.md` in your skills directory instead of fifteen folders, a trailing slash in a `cp` glob flattened them. Re-copy using the command above.

### Try one first

Install `anti-slop`, paste in any AI-written paragraph, and say:

> Run anti-slop on this.

You get back every flagged word and structural tell, plus a clean rewrite. That is the shortest path to understanding what a skill actually is.

## What's inside

| Skill | Category | What it does |
|---|---|---|
| [`keyword-research`](keyword-research/) | SEO | Turns a raw keyword dump into a filtered, scored, prioritized list. Relevance filtering, intent classification, a three-level competition model (domain, page and brand), and sprint discipline so you get 25-50 real targets instead of 500. Written for the DataForSEO MCP. |
| [`seo-content-strategy`](seo-content-strategy/) | SEO | Builds a prioritized content plan for any site. Scores topics by intent and conversion probability, maps clusters, and tells you what to publish next. Bottom-funnel first. |
| [`listicle-blog-post-writer`](listicle-blog-post-writer/) | SEO | Writes "best of" roundups and alternatives posts. Per-item cards, at-a-glance tables, and anti-templating guardrails drawn from the analysis of ClickUp's blog traffic collapse. |
| [`anti-slop`](anti-slop/) | Quality gate | Catches AI-generated fluff at the sentence level. Banned word lists, structural red flags and rewrite patterns. |
| [`anti-spam`](anti-spam/) | Quality gate | Checks a draft against your *existing* posts for scaled-content warning signs: duplicated skeletons, repeated heading templates, publish bursts, uniform commercial footprints. Six pass/fail gates, with thresholds I use as an editorial rule of thumb. |
| [`cro-audit`](cro-audit/) | Quality gate | A 25-point conversion audit for any landing page, sales page, form or pricing page. Works as an audit on a live page or a pre-ship gate on a new one, with five non-negotiables that block shipping. |
| [`careful-marketer`](careful-marketer/) | Quality gate | An operating mindset, not a task. Makes the agent ground in real data before writing, verify claims before citing them, stay in scope, and stop to ask instead of guessing. |
| [`short-form-video-scripts`](short-form-video-scripts/) | Video and social | Reels, Shorts and TikTok scripts on a Hook, Truth, Do This Instead, CTA structure, plus matching captions. |
| [`social-media-manager`](social-media-manager/) | Video and social | Turns one video or image into captions for YouTube, TikTok, Instagram, Threads, LinkedIn, X, Facebook and Pinterest, trimmed to each platform's character limit. Copy them into any scheduler, or chain it to one that has an MCP or API. |
| [`linkedin-profile-scraper`](linkedin-profile-scraper/) | Video and social | Pulls a public LinkedIn profile's posts via Apify and exports a clean CSV with engagement scoring. Requires an Apify token. |
| [`landing-page-designer`](landing-page-designer/) | Build and ship | Builds a focused single-page landing page in deployable HTML/CSS, built around one goal per page. |
| [`web-designer`](web-designer/) | Build and ship | Builds distinctive frontend interfaces that avoid the generic AI look. Includes the "4 unique takes" approach, framework choices and static deployment. |
| [`skill-creator`](skill-creator/) | Meta | The skill that writes other skills. Describe what you want and it builds a properly structured `SKILL.md`. Start here if you want your own. |
| [`setting-up-mcps`](setting-up-mcps/) | Meta | Walks you through connecting Claude Code to outside tools via MCP (GitHub, Notion, Sheets, Slack, databases) and debugs the connection when it breaks. |
| [`skill-auto-improve`](skill-auto-improve/) | Meta | Runs in the background, grades other skills' output against their own rules, and after 3+ similar failures proposes a one-line fix to that skill, applied only when you say yes. Your usage becomes the test suite. |

## Why these are different

These carry operating rules from shipping client work:

- **`anti-spam`** checks a new draft against your *existing* posts, at the cluster level, so you catch template patterns across a whole site, not just in one draft.
- **`keyword-research`** treats a zero-volume result as a reason to check other demand signals, not a verdict, and separates domain, page and **brand** competition. Brand strength matters a lot for AI visibility.
- **`listicle-blog-post-writer`** encodes the guardrails from ClickUp's traffic collapse so your roundups don't read as templated.
- **`cro-audit`** is a pass/fail scorecard, so it works as a gate you run before shipping, not just an opinion.

Skills are just markdown. When Claude gets something wrong, you open the file and fix the rule, and the same mistake gets much rarer. That feedback loop is the whole reason the format is worth learning.

## What each one needs from you

Most run as-is. Three touch a paid service, and only one of those requires it:

- **`linkedin-profile-scraper`** needs an [Apify](https://apify.com) API token in `$APIFY_API_TOKEN`, or pasted when it asks. Apify's free tier covers small runs. The profile URL you give it is sent to Apify, and it does not work without a token.
- **`keyword-research`** is written against the **DataForSEO MCP** (pay-as-you-go, no subscription). The filtering, scoring and prioritization logic works with any keyword source, including a CSV export or a manual list.
- **`social-media-manager`** writes captions with no account. To also *schedule* posts, it works best with **Blotato**, which ships a hosted MCP server. Buffer, Publer, Metricool, Later or a Make/Zapier bridge also work with more setup.
- **`social-media-manager`**, **`short-form-video-scripts`** and **`keyword-research`** have `[BRACKETED_PLACEHOLDERS]` for brand voice, platforms, your CTA and topic categories. Fill them in once and they are yours. `seo-content-strategy` asks for your business details in conversation instead.
- **`skill-auto-improve`** proposes edits to your other skill files and applies them only after you approve. Keep your skills in git anyway, so any approved change is easy to revert.

## Common questions

### What are Claude marketing skills?

Claude marketing skills are markdown files that give Claude specialized marketing knowledge and workflows. Each skill is a folder containing a `SKILL.md` with YAML frontmatter describing when to use it. When a request matches that description, Claude loads the file and follows its rules. Unlike a prompt you paste in, Claude finds and loads a skill on its own when your request matches its description.

### Are these Claude skills free?

Yes. All 15 are free under the MIT license (with `skill-creator` under Apache 2.0). What costs money is how you run Claude Code, which needs a paid Claude plan or Anthropic API billing. Check [Claude's pricing page](https://claude.com/pricing) for current plans.

### Can I use Claude skills on the free plan?

Not in Claude Code, because Claude's free plan does not include it. The files themselves cost nothing to download, read and adapt, and the frameworks inside are readable by a person on any plan.

### How do I install Claude marketing skills?

Paste the repo link into Claude Code and ask it to install the skills into `~/.claude/skills/`, or copy each folder there yourself. Start a new session and run `/skills` to confirm they loaded. Each skill has to keep its own folder, because the folder name becomes the command you type.

### Can I use Claude for marketing?

Yes, and skills make it far more consistent. Without them, Claude tends toward generic marketing advice and can state things confidently that are not true. A skill supplies the frameworks, banned-word lists, verification steps and quality gates, so the output follows a process. You still review it before it ships. The gate skills here (`anti-slop`, `anti-spam`) exist to catch what the model gets wrong.

### Do these work with Cursor, Codex or other agents?

They are plain markdown in the Agent Skills format, so any agent that reads that format can load them. They were written and tested against Claude Code, so treat other agents as untested rather than guaranteed.

### Can I use these commercially or in client work?

Yes. MIT licensed, so you can use them commercially, modify them and ship them inside your own products, as long as you keep the license notice. `skill-creator` is the one exception, derived from Anthropic's original and licensed Apache 2.0.

### What are the best GitHub repos for marketing besides this one?

Corey Haines' [marketingskills](https://github.com/coreyhaines31/marketingskills) is the biggest marketing library on my list, and Anthropic's [skills repo](https://github.com/anthropics/skills) has frontend-design and the document skills. I ranked ten, with costs and setup effort for each, in my list of the [best GitHub repos for marketing](https://ryandoser.com/best-github-repos-for-marketing/) (this repo is #3 there, so read that ranking knowing it's mine).

## Learn more

- [How to use GitHub as a non-coder](https://ryandoser.com/how-to-use-github/)
- [How to create Claude skills](https://ryandoser.com/claude-skills/)
- [7 best free Claude skill repos on GitHub](https://ryandoser.com/best-free-claude-skill-repos/)

## Want more?

These fifteen are the ones I give away.

The full library is **[the Claude Skills Stack](https://skills.ryandoser.com)**: 40+ skills, one-time price, lifetime updates. What is in there and deliberately not here:

- **YouTube SEO Packaging**: title formulas, thumbnail text strategy, title-thumbnail pairing, first-10-second hooks, description templates, tags and timestamps. The packaging system from a 40K-subscriber channel.
- **YouTube Thumbnail Designer** and **Infographic Generator**: the image pipelines, not just the copy
- **Local SEO Strategist**: Google Business Profile, the map pack, review velocity
- **Email Newsletter Writer**, **Email Sequence Builder**, **Lead Magnet Creator**
- **GEO / AI Search Optimizer**, **Internal Linking Architect**, **Comparison Writer**
- **Paid Ads**, **Personal Brand Website**, **Brand Kit Builder**
- Plus the setup video, a Start Here guide, and my personal `AGENTS.md`

I'm [Ryan Doser](https://ryandoser.com). I make AI and marketing videos on [YouTube](https://youtube.com/@RyanDoserAI).

Found a bug or want a skill improved? [Open an issue](https://github.com/rdoser13/free-claude-skills/issues).

## License

MIT. Use them commercially, modify them, ship them in your own products. Keep the license notice. Credit is appreciated, not required.

One exception: **`skill-creator`** is derived from [Anthropic's skill-creator](https://github.com/anthropics/skills) and remains under Apache License 2.0. It has been modified to be self-contained (its packaging and init scripts were rewritten as manual steps).
