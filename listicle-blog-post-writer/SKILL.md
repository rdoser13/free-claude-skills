---
name: listicle-blog-post-writer
description: Write research-driven listicle blog posts - "best of" roundups, tool lists, alternatives posts, community and channel lists. Use when the user asks for a listicle, a roundup, a "best X" post, an alternatives post, or a numbered list article. Handles research, structure, per-item cards, SEO rules, and the anti-templating guardrails that keep a roundup from reading as programmatic content. Not for video-repurposed posts.
version: 1.0.0
---

# Listicle Blog Post Writer

Write research-driven, SEO-optimized listicle blog posts. Takes a topic, a list of items, and a target keyword, then produces a publish-ready article with per-item cards, honest editorial judgment, and the citable structures AI answer engines actually lift.

This skill is publishing-platform agnostic. It produces the article. How you publish it (static site, CMS, headless, paste into an editor) is yours to handle.

## Intake

Ask for whatever is missing before writing:

1. **Topic and working title** (required)
2. **Target keyword** (required). If not supplied, propose 3 options and explain the intent behind each.
3. **The list items** (required). If the user has not fixed the list, research candidates and propose one.
4. **Which items the user has personally used** (important, see the firsthand boundary below)
5. **Audience** and what their next step should be
6. **Word count or item count**, if they have a preference

Do NOT start writing until the target keyword and the list are settled. Everything downstream depends on both.

## Workflow

### Step 1: Research each list item

For every item, gather from primary sources (the item's own site and docs, not third-party summaries):

- What it actually is, in one sentence
- Pricing, with the **billing basis stated explicitly**. Most vendor pricing pages default to the ANNUAL toggle and print the annual rate with a "/month" suffix, so the headline number is frequently not the monthly price. The sub-line ("billed yearly") is the disambiguator. Check for a machine-readable rate card at `<vendor>/pricing.md` or `llms.txt` first, which settles it in one fetch.
- Free tier or trial, and what it excludes
- The genuine limitation. Every item has one.
- One specific, quotable fact (a real number, a named capability, a documented limit)

**Price the thing the post is about.** If your subject is a FEATURE of a larger product (an API, an integration, an add-on), check whether it has its own entry path separate from the parent subscription. Quoting the suite price for a feature that sells standalone is a right-number-wrong-thing error.

### Step 2: Validate list membership against the SERP

Pull the live SERP for the target keyword and read what the top pages actually list.

**A tool being good, or personally used, does not make it a category MEMBER.** If zero of the ranking pages list anything resembling one of your items, that item probably does not belong under this keyword, however much you like it. The fix is structural: demote it to its own section as a differentiated angle, or cut it. Never pad the list with untested items just to match the SERP.

Surface a genuine conflict between your tested set and searcher expectation to the user rather than resolving it silently. It changes what the post is.

### Step 3: Validate the premise

**The premise is the highest-risk claim in the post, and no quality gate checks it.**

Before writing, google the exact working title and read the top competitors. A brief asserting "nobody covers this" is a hypothesis, not a fact. Validating against the head term often proves the wrong proposition: a head term can be developer-only while a thriving cluster of posts exists one modifier away.

If the premise does not survive, say so and propose a real angle instead of writing to a brief you have disproven.

### Step 4: Competitive research

Read the top 5-10 ranking pages for the target keyword. Note:

- What structures they all share (this is the citation baseline you must at least match)
- What every one of them is missing (this is your angle)
- Their item counts and how they justify inclusion
- Whether an AI Overview appears, and which pages it cites

### Step 5: Write the post

Follow the article structure and card formats below.

### Step 6: Self-edit pass

Run these checks yourself before showing anyone:

- **Hunt absolutes.** Grep for `every|nobody|only|always|never|all of|exactly|most`. Each hit is trivially falsifiable by a reader with one search. Justify or soften every one. Replacing one absolute with another is not a fix.
- **Read only the "Bottom line" and "Best for" lines in sequence.** Cross-entry contradictions are invisible to per-item review: entry #1 claims to be "the only tool here that does X" while entry #4 also does X. Each card verifies fine alone.
- **Count the items against any number in the title.** A "7 Best" title needs exactly 7 main-list entries.
- **Cut restatement.** If a closing paragraph just repeats a Con or the Bottom line, delete it.
- **Verify every external link resolves** and is classified SOURCE or RIVAL (see External Links).

### Step 7: Verify the facts independently

Re-check every number, price, date, and named capability against the primary source, assuming the draft is wrong.

Two failure modes to plan for. An automated fact-check will produce **false positives** (flagging a proper noun as a banned word, re-flagging something you already confirmed). More dangerously, it will also **falsely CONFIRM** things. On any claim that someone *coined, founded, invented, or was first*, open the cited page and read the attribution sentence yourself. Credentialing a living person with something they explicitly disclaim is the worst error a roundup can ship, and it is invisible to every other check.

A clean second pass means the second pass was clean, not that the post is correct.

## Article Structure

Listicle posts follow this structure:

```
# [Article Title -- H1, exactly ONE per article]

[Introduction: 1-2 sentences ONLY. Primary keyword in the first sentence, bolded ONCE.]

## [Context/Problem H2 -- optional but recommended. Sets up WHY this list matters.]

[1-3 paragraphs on the problem, why most options fall short, or why this topic matters to the reader. This is where a real point of view earns its place.]

## [Main List H2 -- MUST contain the target keyword. "Best [Keyword] in 2026" format.]

[Brief intro paragraph: 1-2 sentences setting up the list criteria.]

### 1. [Item Name] (Free/Paid label if applicable)

[Screenshot in <figure> tags]

[2-3 sentence description. Who runs it, what it specializes in, why it's on the list. Include specific facts: member counts, pricing, credentials.]

### 2. [Item Name]
...continue for all items...

## [Optional: Honorable Mentions H2]

[Shorter entries for items that didn't make the main list]

## [Conclusion H2 -- name it for THIS post's subject. BANNED as a cluster footprint: any closer heading you have already used on other posts ("Final Thoughts", "The Bottom Line", "Which One Should You Pick?"). Write a closer that could not be pasted onto another post.]

[Brief summary, 50-80 words. End with a forward-looking statement or CTA.]

## [Target Keyword] FAQs

### [Question 1]
[Direct answer, 40-80 words]

### [Question 2]
[Answer]

### [Question 3]
[Answer]

[Optional: ### Question 4-5]
```

### Tool/Product Roundup Card Format (Pros/Cons + labeled fields)

For **tool, product, or software roundups** (not community/channel/newsletter lists), give every item a scannable card in this exact order and spacing. This card is dense, scannable, and quotable, which is what both readers and AI answer engines reward.

```html
<h3><strong>1. Tool Name (Best for [one-line positioning])</strong></h3>

<figure><img .../><figcaption>...</figcaption></figure>
&nbsp;

[1-2 sentence intro: what it is + a first-person take on who it fits.]

<strong>Pros:</strong>
<ul>
 	<li>...</li>
 	<li>...</li>
</ul>
<strong>Cons:</strong>
<ul>
 	<li>...</li>
 	<li>...</li>
</ul>
&nbsp;

<strong>Best for:</strong> [one line]

<strong>Pricing:</strong> [free tier + starting paid tier, with billing basis — annual vs monthly stated explicitly]

<strong>Free trial:</strong> [Yes/No + detail]

<strong>Bottom line:</strong> [1-2 sentence verdict]

[Optional closing paragraph ONLY if it delivers a NEW community receipt or fact not already in the card. If it just restates a Con or the Bottom line, cut it — see the bloat rule.]
```

**The firsthand boundary must survive three consistency checks.** When you have run some-but-not-all of the tools: (1) the stated INCLUSION CRITERION must actually distinguish ranked from unranked tools — "I won't rank software I haven't used" is false the moment the list contains untested tools; name the real criterion (SERP presence plus a priceable rate card, or whatever it actually is). (2) The bottom AFFILIATE DISCLOSURE must not say "I only recommend tools I actually use" over a list of untested tools — state which tool was run and how the rest were assessed. (3) Any FAQ answer that RECOMMENDS an untested tool must carry the boundary in the same answer ("X is the only one of these I have run; read the other two as a pricing-and-design assessment"), because FAQ chunks travel without the post's framing. Cons bullets on untested tools should read as design observations, not field reports.

**The card format triple-states facts by default, so trim in the self-edit pass.** A tool's free-tier status can land in the at-a-glance table, a Cons bullet, the Free trial field AND an FAQ. Keep the table cell and the labeled field (they serve different readers) and cut the Cons bullet or FAQ restatement unless it adds a new fact.

**Spacing that matters:** put a bare `&nbsp;` spacer line after the Cons `</ul>` so the labeled fields (Best for / Pricing / Free trial / Bottom line) visually separate from the Pros/Cons block. The `<strong>Pros:</strong>` / `<strong>Cons:</strong>` labels sit DIRECTLY above their own `<ul>` (no spacer between label and its list) — that pairing is deliberate. Every labeled field is its own line with a blank line between.

**Add these citable structures to any tool roundup** (each earns AI-search citations competitors' vendor lists can't):
- **An "at-a-glance" comparison table** right after the intro, before the deep-dives (Tool | Best for | Starts at | + 2 relevant columns). This is the single most universal element on top-ranking pages and the one most missing. State the billing basis if prices are mixed annual/monthly, or keep the table figures as clean "starts at" shorthand and carry the billing detail in each card's Pricing field. **Write every row to be quotable out of context:** an LLM lifts one row into an answer without the surrounding article, so each cell must stand alone. "Best for" = a specific persona/use case, never a bare feature. "Starts at" = a concrete figure with unit, never "affordable." A row that only makes sense after reading the intro is a wasted citation opportunity.
- **A reusable "How to Choose" criteria block** — 4-6 questions the READER applies themselves (not a pick-for-me), framed as questions you genuinely apply yourself. AI answers lift these directly.
- **A one-line sourcing signal** near the criteria block or in the closing section — one sentence naming the TRUE evidence base. If everything was tested: "Every pick here I tested myself; pricing was checked live on each tool's own page." If only some were: "I have run X on my own videos and priced the rest from their live rate cards on [date], monthly billing selected." AI engines weight visible sourcing when deciding whom to cite, and an honest split boundary IS the differentiator against vendor pages — never paper over it with a tested-everything claim the post elsewhere contradicts. Keep it to one sentence, not a methodology essay.
- **A "Which should you pick?" decision block** — tight situation → tool lookup. Keep it SHORT and do NOT re-explain the same axes the How-to-Choose block already covered (that back-to-back redundancy is the most common bloat flag on this format).
- **A one-line-each head-to-head** for the top adjacent query (e.g. "n8n vs Make vs Zapier, in one line each").
- **Own your exclusions.** If the head keyword pulls an adjacent off-ICP cluster (e.g. enterprise RPA on an "automation tools" post), add an explicit "What about [excluded category]?" section that names the big tools, links them, and says why they're deliberately out. Owning an omission reads as confidence and closes the "looks incomplete to an AI engine" flank without forcing off-ICP tools into the ranking.

### Idea/Method Roundup Card Format (side hustles, business ideas, strategies — NOT tools)

When the list items are IDEAS, not tools (side hustles, "ways to X", strategies, business models), the Pros/Cons tool card does NOT fit. Use this per-item card instead :

```
### N. [Idea Name]

**What it is:** [1-2 sentences]
**Who it fits:** [the reader persona this suits]
**Realistic income:** [honest, hedged range or the relevant metric — attribute self-reported figures]
**How to start:** [concrete first step + ONE real external example link, see below]
**The downside:** [the genuine drawback — a real cost, not a humblebrag]
```

- Keep the same citable structures as the tool format: at-a-glance table (quotable rows), reusable "How to Choose" block, sourcing signal, "own your exclusions."
- **Screenshots:** an ideas list has NO per-item UI to screenshot. Do NOT fabricate hypothetical dashboards, client results, or deliverables — that breaks the no-fabrication rule and reads as fake. Instead: (a) use 2-3 genuinely-illustrative contextual screenshots (e.g. the funnel destinations), and (b) give EVERY item one real EXTERNAL example link to a representative tool/platform/marketplace, woven into "How to start," so the reader can see the idea in action. This satisfies the value-add-external-links requirement for idea lists and scales external links up with the list (a 10-item list should not ship with only 2 external links). Where the only obvious link would be your own product or community, use a NEUTRAL third-party example instead so the post is not all self-links.
- **Vary the downside label.** Do NOT repeat one phrasing on all 10 items. A single word ("honest") repeated down the page starts carrying the whole post and reads as templated.

### Screenshot Placement

Every list item gets a screenshot placed ABOVE its description:

```html
<h3><strong>1. Item Name (Free)</strong></h3>

<figure>
  <img src="[path-or-url]" alt="[alt text]" width="1280" height="823" loading="lazy" />
  <figcaption>[One sentence describing what's shown]</figcaption>
</figure>

<p>[Description paragraph with external link...]</p>
```

---

## Voice and Style Rules

### Voice

- **Tone:** conversational and direct. Write like a knowledgeable person talking to one other person.
- **Reading level:** 8th-9th grade.
- **Perspective:** first person when sharing experience ("I tested this"), second person when advising ("You will want to").
- **Personality:** contrarian only when earned, and back it up. Honest opinions, including skepticism.
- **Address the reader directly.** Write to one person, not an audience.
- Show, don't tell. Concrete examples over abstract claims.

### Sentence and Paragraph Rules

- Short sentences: 8-15 words average
- Alternate short and long sentences for rhythm
- Short sentence after a complex idea = emphasis
- Never start 3+ consecutive sentences the same way
- Do not start any sentence with the same two words as the previous sentence
- Do not use any three-word phrase more than once in the entire article
- Do not repeat any word within eight words of its last use
- Maximum 4 sentences per paragraph
- Mix short (1-2 sentence) paragraphs with longer ones
- Active voice. Subject-verb-object.

### Em Dash Ban

**ZERO em dashes (--) in any output. Non-negotiable.**

Replace with: a period and new sentence, a comma, parentheses, or restructure.

### Punctuation Rules

- No semicolons. Ever.
- **ZERO emojis. Never use emojis anywhere in the article.**
- No excessive exclamation points

---

## SEO Rules

### Keyword Placement

- **Primary keyword must appear in the first sentence of the intro.** Bold it ONCE on that first use.
- Primary keyword 1-2 times per major H2 section (natural placement, not forced)
- 5-7 unique LSI/secondary keywords, each used 1-2 times naturally throughout
- Primary keyword in at least one H2 heading

### Blog Post Title Rules

- Place the target keyword toward the beginning
- **Up to 65 characters max.**
- Sound intriguing enough for someone to click
- Include year, parenthetical qualifiers, or list count when relevant (e.g., "10 Best AI Tools for Marketing (Free & Paid)")

### Meta Description

- UNDER 150 characters (over that truncates in the SERP)
- Primary keyword included, front-loaded
- Creates curiosity without clickbait
- The first 6 words must not match any sibling post on your site. Repeated meta openers across a cluster are a programmatic-SEO footprint.

### Permalink

Target keyword in kebab-case. "Best AI Communities" becomes `best-ai-communities`.

### Internal Links

Include 2-4 internal links to relevant articles on the same site. Pull the live sitemap before writing to get the current list rather than trusting local filenames.

- Descriptive, keyword-rich anchor text
- Vary anchor text across posts. Reusing one exact-match anchor for the same target across a cluster is itself a footprint.
- Internal links do NOT open in a new tab
- Spread naturally throughout the body

### External Links

- Each list item gets an external link to its own page (opens in new tab)
- 1-3 additional outbound links to credible sources where relevant
- All external links: `target="_blank" rel="noopener noreferrer"`
- Never use the same external URL twice
- **Classify every external link as SOURCE or RIVAL.** A source (the subject's own site, a study, a primary doc) gets a normal followed link. A RIVAL is any page competing for your target keyword. Nofollow it or unlink it, never dofollow it. This is easy to miss and no quality gate catches it.

### FAQ Rules

Include 3-5 FAQs only when they add something the body does not already answer.

- Heading: "[Target Keyword] FAQs"
- Questions written the way people actually search or ask an assistant
- Direct answer first, 40-80 words each
- Many static-site and CMS setups auto-emit FAQPage schema from a heading matching this shape, so check your build before renaming it. Anything wrong in an FAQ answer ships into structured data, which is the most extractable part of the page.


---

## Word Count Rules

- Default target: scale with list size. Rough guide:
  - 5 items: 800-1,000 words
  - 10 items: 1,200-1,500 words
  - 15+ items: 1,500-1,800 words
- Each list item description: 2-3 sentences (40-80 words)
- Context/problem section: 100-200 words
- Conclusion: 50-80 words
- FAQs: 40-80 words each
- NEVER pad with fluff to hit targets

---

## Banned Words and Phrases

### Single Words -- NEVER Use

delve, tapestry, vibrant, landscape, realm, embark, excels, vital, comprehensive, intricate, pivotal, moreover, arguably, notably, spark, sparked, supercharge, supercharged, enhance, navigate, ignite, ignited, robust, multi-faceted, solely, crucial, ensure, portray, ongoing, vigilance, intriguing, holistic, game-changer, revolutionary, unleash, cutting-edge, synergy, seamlessly, transformative, utilize, execute, facilitate, implement, optimize, leverage

### Phrases -- NEVER Use

- "Dive into..." / "Let's dive in..."
- "Unlock your potential"
- "It's important to note that..."
- "In this section..."
- "Without further ado..."
- "At the end of the day..."
- "It goes without saying..."
- "Needless to say..."
- "In today's world..."
- "As we all know..."
- "It's worth mentioning..."
- "The truth is..."
- "Many people don't realize..."
- "Great question!"
- "That's a common concern"
- "Many people ask..."
- "A testament to"
- "Silver bullet"
- "Based on the information provided"
- "The catch?"
- "Want to know the secret?"
- "The brutal truth?"
- "Here's the kicker"
- "The best part?"
- "Ready to level up?"
- "Changed everything"
- "Game-changer" / "game-changing"

### Structural Patterns to Avoid

- Binary contrast addiction ("it's not X, it's Y" overuse)
- Triple threat syndrome (grouping things in threes everywhere)
- Infomercial transitions
- Corporate verb disease
- Hedging language

---

---

## Google E-E-A-T Alignment

- **Experience:** Reference first-hand testing where it is TRUE, and say plainly where an item was assessed from its rate card and docs instead. Never assert testing you have not done. An honest "where my knowledge stops" line outperforms a fake tested-everything claim.
- **Expertise:** Include specific facts, numbers, and credentials for each item.
- **Authoritativeness:** Link to your own related published work (video, newsletter, prior posts) where it genuinely supports the point.
- **Trustworthiness:** Honest pros AND cons. Acknowledge limitations. Attribute self-reported claims.

---

## Listicle Quality Guardrails (Lessons from the ClickUp Traffic Collapse)

ClickUp lost 97.6% of blog traffic because their listicles followed identical promotional templates at scale. Their "ChatGPT alternatives" page went from 107K visits to 446 after escalating self-promotion across revisions. These rules prevent the same patterns.

### 1. Curate, Don't Pad

- **Only include items that genuinely belong on the list.** ClickUp listed 20 "ChatGPT alternatives" including SEO tools and role-play apps that weren't alternatives at all. Zapier curated 8 genuine alternatives and kept their #2 ranking.
- **Quality of curation > quantity of items.** A tight list of 8 relevant picks outranks a padded list of 20. If the supplied list is long, flag items that don't fit the keyword intent and suggest cutting them.
- **Every item must pass the intent test:** "Would someone searching this keyword genuinely consider this option?" If no, cut it.

### 2. Equal Editorial Treatment

- **Give every list item roughly equal word count and editorial depth.** ClickUp gave their own product 4.3x to 7.1x more words than competitors. Google noticed the asymmetry.
- **If your own product is on the list, treat it identically to other entries.** Same word count, same honest pros/cons, same format. No special promotional sections, pricing tables, or extra CTAs for the self-entry.
- **Place your own entry based on merit, not marketing.** ClickUp always ranked themselves #1 regardless of relevance. If your entry belongs at #3, put it at #3. Zapier placed themselves at #3 and #7 and still ranked #2 for the keyword.

### 3. Honest Editorial Voice

- **Include genuine editorial opinions.** Zapier's writer said "I find it very funny that Grok is on this list" and described Claude as responding "more empathetically." That editorial personality is what separates ranking content from templated content.
- **Give specific, fair criticism of every item, including your own.** ClickUp gave competitors vague two-sentence criticisms while their own section had zero real limitations. Readers and algorithms both detect this.
- **Close with a reader recommendation, not a branded CTA.** Zapier ended with "give a few of them a go and find out" and linked to comparative analyses. ClickUp ended with promotional CTAs.

### 4. No Templated Structure at Scale

- **Vary the structure between listicles.** ClickUp used the identical skeleton across 7,000+ pages. Google applied a section-level quality classifier that destroyed the entire blog section (97.6% decline) while the rest of the domain declined only 27%.
- **Vary description formats.** Not every item needs the same intro-features-pricing-verdict structure. Some items deserve a story. Others deserve a quick take. Match the format to the item.

### 5. Technical Hygiene

- **Verify structured data resolves correctly.** ClickUp had literal `[year]` template variables in their JSON-LD schema across thousands of pages. Always verify schema output matches actual content.

---

---

## SEO in the AI Era: Reputation Over Optimization

SEO is no longer primarily a technical discipline. AI-powered search (ChatGPT, Gemini, Perplexity, AI Overviews) decides what to surface based on brand reputation and web-wide presence, not just on-page signals. A crawler checking keyword density is being replaced by a model asking: "Is this person credible? Are they being cited elsewhere?"

**What this means for every listicle we publish:**

- **Brand mentions matter.** When AI models see your name or domain cited across YouTube, Reddit, newsletters, podcasts, and third-party blogs, that builds the association. Write articles that are specific and citable, not generic. A post that gives a real stat, a real opinion, or a real workflow will get linked and quoted. A vague overview won't.
- **Be the curator with an opinion, not just a list maker.** AI models pull from sources with original insight. If this listicle just restates what three other "best of" articles say, it won't get cited. Every item description should include a specific reason for the recommendation, based on actual use rather than marketing copy lifted from the item's own website.
- **Write for humans reading, AI models referencing.** Structure answers cleanly. Use direct, declarative sentences. If someone asked an AI "what are the best X?" and the answer pulled from this article, would it make sense? If yes, the writing is in the right shape.
- **Credibility signals compound.** A channel, a newsletter, a community, podcast appearances and guest posts together create a web of presence that models read as authority. Link out to your own platforms where relevant and, where possible, to third-party coverage of you.
- **Quoted facts > vague claims.** AI models extract specific, quotable facts. "Community has 12,000 members and focuses on..." is citeable. "A great community with lots of content" is not. Always anchor item descriptions in verifiable specifics.

The technical fundamentals (keyword in title, proper headings, fast load times) still matter as a baseline. But the ceiling is now set by how credible and present the brand is across the entire web, not how perfectly a page is optimized.

## Presenting the finished post

Deliver:

1. The full article
2. **5 title options and 3 meta description options.** Writers almost always want to pick their own, so lead with a recommendation but offer the choice.
3. A list of what you could NOT verify, stated plainly
4. Any premise or membership conflicts you surfaced along the way

---

## Lessons that generalize

Hard-won failure patterns worth carrying into any roundup:

- **On a pricing roundup, compute the full crossover sequence before writing the thesis.** Derive every item's cost at every unit count from the published tiers with a short script, then read off where the cheapest option changes. Flat plans have tier cliffs, so the answer often changes more times than a hand-written thesis assumes, and a thesis that contradicts its own table is the most embarrassing way to be wrong.
- **When two of a vendor's own surfaces disagree on a number, do not assert either.** Write around it ("fewer than X reaches") so you neither inherit their inconsistency nor go stale when they fix it.
- **When two of your own posts make the same claim, diff them before cross-linking.** Adding an internal link puts any contradiction one click apart. Grep both for shared entities (pricing, tiers, counts) and reconcile against the live source.
- **A first-person title claim must match the narrowest true version of the experience.** If you tested all of them but use two daily, "Tools I Use" overclaims. The title has to carry the weaker tier.
- **When a restructure changes the item count, fix the title and body in the same pass.** A title promising 8 over a section reading "the 4 I actually publish through" reads as bait.
- **Verify a fix on the live page it affects,** not the page you edited. Index pages, cards, and feeds frequently render from different fields than the post itself.

---

## Quality checklist

Before delivering, every item must pass:

- [ ] Intro is 1-2 sentences with the primary keyword bolded once
- [ ] Primary keyword in at least one H2
- [ ] Conclusion H2 is post-specific and could not be pasted onto another post
- [ ] Item count matches any number in the title
- [ ] Title under 65 characters
- [ ] Meta description under 150 characters, first 6 words unique vs siblings
- [ ] ZERO em dashes, banned words, emojis, semicolons
- [ ] No sentence starts with the same two words as the previous one
- [ ] Premise validated against the live SERP and the exact working title
- [ ] List membership validated. No item included purely because it is good.
- [ ] Absolutes hunted and justified
- [ ] "Bottom line" lines read in sequence for cross-entry contradictions
- [ ] Every external link classified SOURCE or RIVAL, rivals nofollowed or unlinked
- [ ] Every "coined / founded / invented / first" claim traced to the source's own attribution sentence, read personally
- [ ] Pricing carries an explicit billing basis, checked against the monthly toggle
- [ ] Every item has a genuine, specific limitation
- [ ] Your own entry (if present) gets equal word count and honest criticism
- [ ] For tool roundups: at-a-glance table, "How to Choose" block, sourcing signal, per-item cards
- [ ] Restatement and bloat cut

**0 failures:** ship it. **1-2:** fix and re-check. **3+:** rewrite the affected sections and run the full list again.
