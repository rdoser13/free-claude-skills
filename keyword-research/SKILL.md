---
name: keyword-research
description: Filters, scores, and prioritizes keyword research into an actionable target list. Retrieves search data (monthly search volume, keyword difficulty, CPC, competition, trends, live SERPs) via the DataForSEO MCP where available, or works from any keyword source including a manual export. Use when the user asks to research keywords, find keyword opportunities, analyze search volume, check keyword difficulty, get keyword suggestions, find related keywords, identify SERP competitors, or do any SEO keyword analysis. Also triggers on phrases like "topical map", "keyword gap", "content gap", "search volume", or "keyword ideas".
---

# Keyword Research

Turn raw keyword data into a filtered, scored, prioritized target list.

**The data source is swappable. The judgment is the skill.** The retrieval steps below are written against the **DataForSEO MCP**, but everything that matters here (relevance filtering, intent classification, opportunity scoring, the three-level competition model, sprint discipline) works with any keyword source: a different provider's MCP, a CSV export, Search Console, or a manual list. If you use a different tool, skip to **Relevance Filtering** and feed it whatever data you have.

## Setup

**With the DataForSEO MCP:** connect it once and the tool calls below work. DataForSEO is pay-as-you-go rather than subscription, so there is no plan tier to clear, but calls do cost credits. Batch your lookups rather than calling one keyword at a time.

**Without it:** bring keywords and whatever metrics you have. Volume and difficulty are useful but not required. Several of the highest-value checks below (live SERP intent, AI-surface citation, existing position) do not come from a keyword tool at all.

**Missing metrics are not a blocker.** Score what you can, mark the rest unknown, and lean harder on the live SERP.

## Core Workflow

### Single keyword research

1. **Keyword overview:** `dataforseo_labs_google_keyword_overview` for volume, difficulty, CPC, competition, and intent on a seed term
2. **Keyword ideas:** `dataforseo_labs_google_keyword_ideas` to expand into the broader topic space
3. **Keyword suggestions:** `dataforseo_labs_google_keyword_suggestions` for long-tail variants containing the seed
4. **Related keywords:** `dataforseo_labs_google_related_keywords` for semantically adjacent terms

### Batch volume lookup

`kw_data_google_ads_search_volume` accepts a list of keywords and returns Google Ads volume for all of them in one call. This is the cheapest way to price a large candidate set.

### Keyword difficulty

`dataforseo_labs_bulk_keyword_difficulty` scores many keywords at once.

### Trend and history

`dataforseo_labs_google_historical_keyword_data` returns the monthly curve. **Always pull the curve, never just the 12-month average.** A term at healthy current volume can be 80% off its peak and still falling, and a post takes 30-60 days to mature, landing on numbers lower again.

`kw_data_google_trends_explore` gives relative interest over time as a cross-check.

### Search intent

`dataforseo_labs_search_intent` returns a model-classified intent per keyword. Treat it as an input to the classification below, not a replacement for reading the live SERP.

### Existing rankings and competitors

- `dataforseo_labs_google_ranked_keywords` for what a domain already ranks for. **Run this on your own domain first.** Existing position 2-15 is the highest-value work available.
- `dataforseo_labs_google_competitors_domain` and `dataforseo_labs_google_serp_competitors` to find who actually owns the space.

### The live SERP (do not skip this)

`serp_organic_live_advanced` returns the live result page: who ranks, and which SERP features are present.

**Index data alone is not the landscape.** Pull the live SERP before characterizing any keyword's difficulty or value. It is the only way to see that a query is owned by the vendor's own documentation, that half of page one is a different intent entirely, or that six SERP features are eating the clicks.

**Known limitation:** `serp_organic_live_advanced` does NOT return AI Overview citation contents. The AIO comes back as a stub with no references. An empty AIO block from this tool means "not loaded," never "no citations." To check citation status, use the AI-optimization/LLM-response tools or pull the page in a browser. Reporting the stub as "no citations" is a false negative on the question that matters most.

### Tool discovery

If a tool name does not resolve, run `/mcp` and look for the closest match under the `mcp__dataforseo__` prefix. The MCP surface is large and changes; the names above were current at time of writing.


## Relevance Filtering (REQUIRED)

Every keyword MUST pass relevance filtering before being shown to the user. Volume without relevance is worse than no keyword at all: it produces traffic that bounces and content nobody in your audience wanted.

**Set this up once.** Before the first run, ask the user for (or read from their brand guide):

1. **Approved topic categories** — the 5-10 subject areas they publish in
2. **Their audience** — who they want arriving, and what that person's next step is
3. **Their offers** — what a visitor could eventually buy, join, or subscribe to

Record the answers at the top of this file (or in a sibling `niche.md`) so later runs reuse them. Everything below operates against that list.

### Approved Topic Categories

`[APPROVED_CATEGORIES — list the 5-10 topic areas this brand publishes in. Only return keywords that fall inside them.]`

### Auto-Reject Filters

Automatically DROP any keyword matching these patterns. Do not show them:

- **Brand navigational queries** (e.g. "chatgpt login", "canva pricing") unless it is the user's own brand
- **Pure definition queries** with no depth angle ("what is SEO" at 200K MSV is vanity, not actionable)
- **Off-niche topics** — anything outside the approved categories above, however high the volume
- **Tool queries with no angle into the niche** — a generic "how to use Excel" is not a marketing keyword unless tied to a marketing workflow
- **Extremely broad vanity terms** — single-word head terms like "marketing", "AI", "SEO". Unwinnable and untargetable.
- **News/trending-only queries** — a spike with no sustained volume. Check the trend: if 80%+ of volume came from one month, flag and likely drop.
- **Queries with no commercial or educational path** — if the searcher would never become a reader, subscriber, or customer, drop it
- **Generic top-of-funnel informational queries** — "what is [tool]", "[tool] explained", where the searcher is browsing. Keep informational keywords only when the searcher is actively trying to DO something (build a workflow, solve a problem, compare options). The test: *would this person's next step be to try what the brand teaches, or close the tab?*

### Relevance Scoring

After the auto-reject pass, score each surviving keyword:

| Signal | Points |
|--------|--------|
| Directly matches an approved topic category | +3 |
| Searcher could realistically become a subscriber or follower | +2 |
| Searcher could realistically become a customer | +2 |
| Keyword aligns with content the brand could credibly create | +1 |
| Brand has existing content or authority in this subtopic | +1 |
| Commercial, transactional, or hands-on "how to build/use" intent | +2 |
| Generic top-of-funnel "what is" or overview intent | -2 |

**Minimum relevance score to show: 5/11.** Below that, drop it silently.

**Traffic quality rule:** no more than 30% of the final list should be pure informational intent. If results skew informational, cut the weakest until the ratio holds.

The gut check that resolves most edge cases: *"Would this brand actually publish something for this query?"* If no, cut it.

### How to Present Filtered Results

- Show ONLY keywords that passed both filters
- Add a one-line summary at the bottom: "Filtered X keywords for niche relevance (Y removed as off-topic or low-intent)"
- If the seed keyword yields mostly irrelevant results, say so directly and suggest a better seed


## Output Format

Present results to the user in a clean table. Always include these columns when available:

| Keyword | MSV | KD | CPC | Competition | Intent | Relevance | SEO Title |
|---------|-----|-----|-----|-------------|--------|-----------|-----------|
| ai marketing tools | 2,400 | 45 | $12.50 | HIGH | Commercial | 9/9 | AI Marketing Tools: The Only Ones Worth Using in 2026 |

- **MSV**: Monthly search volume (format with commas)
- **KD**: Keyword difficulty 0-100 (0-30 = Easy, 31-60 = Medium, 61-80 = Hard, 81-100 = Very Hard)
- **CPC**: Cost per click in USD
- **Competition**: LOW / MEDIUM / HIGH
- **Intent**: Classify using the guide below
- **Relevance**: Niche relevance score out of 9 (only show keywords scoring 5+)
- **SEO Title**: An SEO-optimized blog post title for the keyword. Follow the SEO Blog Post Writer skill rules: ~55-65 characters, primary keyword front-loaded toward the beginning, enticing but not clickbait. Use the full character budget when it helps. Include the character count in parentheses.

### Trend Indicator

When monthly search data is available, note the trend direction:
- **Up Trending up**: Last 3 months average > previous 3 months average
- **Down Trending down**: Last 3 months average < previous 3 months average
- **Stable**: Within 15% variance

## Search Intent Classification

Classify every keyword into one of four intent types. Use keyword modifiers and SERP context as signals:

**Informational (I)** -- User wants to learn something
- Signals: "how to", "what is", "guide", "tutorial", "tips", "why", "examples"
- Content format: Blog post, guide, tutorial, explainer

**Commercial (C)** -- User is researching before a decision
- Signals: "best", "vs", "review", "comparison", "top", "alternative to", "features"
- Content format: Comparison page, review, listicle, buyer's guide

**Transactional (T)** -- User is ready to act
- Signals: "buy", "price", "pricing", "discount", "free trial", "sign up", "demo", "near me"
- Content format: Landing page, product page, pricing page

**Navigational (N)** -- User wants a specific site/brand
- Signals: Brand names, product names, "[brand] login", "[brand] support"
- Content format: Usually not worth targeting unless it's your own brand

When intent is ambiguous, check the actual SERP. If top results are product pages -> Transactional. If top results are blog posts -> Informational. If top results are comparison articles -> Commercial.

## Keyword Opportunity Scoring

After gathering data, score each keyword opportunity to help prioritize:

```
Priority Score = Volume + Difficulty + Intent + Position + CPC + SERP-Feature Tax

Volume:      MSV > 1000 = 3pts | 100-1000 = 2pts | < 100 = 1pt (see Demand below -- a zero is not a 0)
Difficulty:  KD < 30 = 3pts    | 30-60 = 2pts    | > 60 = 1pt
Intent:      Commercial = 3pts | Transactional = 3pts | Informational (hands-on tutorial/workflow) = 2pts | Informational (definition/overview) = 1pt
Position:    already ranking 2-15 = +3pts | 16-49 = +1pt | 50+ or unranked = 0 (new page required)
CPC:         >$10 = +2pts | $2-10 = +1pt | $0 with no advertisers = -1pt (see CPC rule below)
SERP tax:    count live SERP features; -1pt per feature beyond two (AIO, ads block, PAA, local pack, shopping, video carousel)
```

**Position beats everything else on ties.** A page already ranking 2-15 is the highest-priority
work available -- moving 5 to 2 is a bigger visibility gain than building a new asset from zero,
for a fraction of the effort. Always sort the set by existing position before sorting by volume.

**Prioritize buyer and builder intent.** Commercial and transactional keywords bring people who are comparing, deciding, or ready to act -- these convert. Informational keywords only score well when the searcher is hands-on (building a workflow, following a tutorial, solving a specific problem). Generic "what is" and overview queries drive vanity traffic that bounces. When in doubt, favor keywords where the searcher's next step is to DO something, not just learn something.

- **Score 7-9**: High priority -- pursue immediately
- **Score 4-6**: Medium priority -- build into content calendar
- **Score 1-3**: Low priority -- only if topical authority demands it

Quick wins = High volume + Low difficulty keywords. Flag these explicitly.

## AI Overview Impact Assessment

For each keyword, note if it's likely to trigger an AI Overview based on these patterns:

**High AIO risk** (likely reduced CTR):
- Pure informational "what is" / "how to" queries
- Definition-style queries
- Simple factual questions

**Medium AIO risk**:
- "Best of" lists and comparisons
- Multi-step how-to guides

**Low AIO risk** (safer for organic traffic):
- Transactional/purchase-intent queries
- Local service queries ("near me")
- Brand-specific queries
- Complex, nuanced topics requiring depth
- Tool/calculator queries

Flag high-risk keywords so the user can weigh traffic expectations accordingly.

## Advanced Workflows

### Competitor Gap Analysis

1. Identify 3-5 competitors (ask user or find via Site Explorer)
2. For each competitor, use their domain to find ranking keywords
3. Compare against user's current rankings
4. Flag keywords where competitors rank but user doesn't (gaps)
5. Prioritize gaps by opportunity score

### Keyword Clustering

After gathering a large keyword set, group them into clusters:
1. Group by semantic similarity (keywords that would rank on the same page)
2. Assign each cluster a primary keyword (highest volume)
3. Classify cluster intent
4. Map clusters to content types (pillar, cluster, supporting)

### Topical Map Creation

For building a complete topical map from keyword research:
1. Run broad research on seed topics
2. Cluster keywords into topic groups
3. Organize into hub-and-spoke architecture:
   - **Pillar pages** (hubs): Broad topic, high-volume primary keyword
   - **Cluster pages** (spokes): Specific subtopics, long-tail keywords
   - **Supporting pages**: Tangential topics that strengthen authority
4. Define internal linking structure (every spoke links to hub, hubs link to all spokes)
5. Prioritize into growth phases (Phase 1: quick wins, Phase 2: medium difficulty, Phase 3: competitive terms)

## Troubleshooting

- **MCP tools not loading**: Run `/mcp` to check connection status. May need to restart Claude Code after config changes.
- **Authentication errors**: Check the credentials on the MCP server config and confirm the account has credit. Re-authenticate via `/mcp`.
- **Empty results**: The keyword may have no data for that location or language. Try `us`/`en` before concluding anything.
- **A zero is not a verdict.** See the 80/20 demand rule below. A missing keyword is frequently an index gap, and a new entity is missing precisely because it is new, which is when its term is cheapest to win.
- **Tool name mismatch**: run `/mcp` to list available tools and use the closest match under `mcp__dataforseo__`.

---

## Competition Has THREE Levels in the AI Era (REQUIRED for every keyword deep-dive)

Pre-AI, competition analysis was two levels: domain link profile and page link profile. That is
no longer sufficient. There is a third axis, and it is the one that decides AI visibility.

| Level | What to check | What influences it |
|-------|---------------|--------------------|
| **Domain** | Referring domains to the competitor's root | Backlinks, site authority |
| **Page** | Referring domains to the ranking URL + content quality/depth | Backlinks, subject-matter expertise |
| **Brand** | Off-site mention volume, reviews, third-party consensus | Reviews, directories, forums, other people's content |

**The brand level is not controllable from your own website.** Traditional rankings respond to
things you publish and links you earn. AI recommendation responds to what the rest of the internet
says about you. A brand can rank poorly and still be the AI's repeated recommendation, and the
reverse happens constantly.

**This is observed repeatedly in live accounts, not theory.** The three states you will actually
encounter:
- A page ranking **#1 organic** for its head term while an AI assistant cites it **zero** times.
- A page ranking top-3 with **zero** AI Overview citations for any variant of the query.
- A page ranking **#1 AND holding the top AIO citation** — the win state, and the rarest.
- Ahrefs published an experiment finding that for an established brand, **94%** of new AI mentions
  came from third-party content and only 6% from owned pages.

**Operational consequences:**
1. A keyword that is easy on links can be unwinnable on brand consensus. Score both.
2. When a page ranks well but earns no AI citation, the fix is **off-site surface**
   (directories, forum answers, third-party mentions), NOT another rewrite of the page.
3. Never report a keyword as "low competition" from KD/referring domains alone. Pull the
   live SERP AND at least one AI surface before calling difficulty.

## Demand: the 80/20 Rule (replaces "volume decides")

Search volume is ONE demand signal, not the decision. Proven demand comes from any of:
Google Ads volume · GSC impressions · user signals (Reddit/Quora engagement) · **first-party data**
(sales calls, client questions, coaching Q&A, support tickets).

**Enforce the ratio: 80% of targets must have demonstrated demand from at least one source
above. Reserve 20% for experimental zero-volume bets.**

**A zero is an index gap, not a verdict.** Keyword tools run on lagging data -- a new entity is
missing from the index *because* it is new, which is exactly when its term is cheapest to win.
Independently confirmed twice: `zernio` went 590 to 2,900/mo in four months, RobinReach was
+600% quarterly at KD 1 while reading 20-40/mo. Local long-tail almost never surfaces in tools
at all. Pair every volume pull with a live SERP + AI-surface check before characterizing a
keyword's value.

**A keyword the user supplies is researched input, not a hypothesis to disprove.** A tool zero on
a supplied term is a prompt to go find what they saw, not grounds to recommend dropping it.

## CPC Reads as Commercial-Intent Proof (and zero is a WARNING)

Read CPC as evidence advertisers are spending real money on the topic, which proves commercial
intent independent of volume.

**Invert it carefully: a topic with no advertisers is usually NOT blue ocean.** The likelier
reading is that the query is informational, or that advertisers tested it and found it does not
convert. Treat a zero-CPC, zero-competition keyword with suspicion rather than excitement,
unless another demand signal (first-party data, real user engagement) backs it.

## Page Architecture Diagnostics

### One core topic per page
Every page gets exactly ONE primary keyword, placed in five slots: **URL, title tag, meta
description, H1, first sentence.** Variants live in the body. The reason is not on-page dogma --
one primary keyword per page is what makes performance **trackable**. Without it you cannot tell
what moved.

Classify every keyword in the set as one of three things:
- **Primary** -- the page's core topic. One per page, no exceptions.
- **Variant** -- a near-identical phrasing (`blue shoes` / `blue shoe`). Same page. No action needed.
- **Secondary** -- a distinct topic that needs its own page. See the splintering signal below.

### The splintering signal (poor performance is the diagnostic)
**When a broad page ranks POORLY for a very specific long-tail query, that is the signal the URL
is too broad to serve it.** Mark the query as a secondary keyword and build a dedicated page.

Example: a `/blue-shoes/` page ranking position 67 for `yellow and blue shoes with dots` is not
an optimization problem -- it is an architecture problem. The fix is a new, more specific page.

Position-based opportunity classification:
| Current position | Classification | Action |
|---|---|---|
| 2-15 | Low-hanging fruit | Optimize/expand existing page. **Highest priority.** |
| 16-49 | Improvable | Refresh, add depth, earn links |
| 50+ | Clustering opportunity | Likely needs a dedicated page |
| Unranked | Untapped | New page required |

## SERP Feature Tax (count it, do not estimate it)

Pull the live SERP and **count** the features competing for the click: ad block, AI Overview,
People Also Ask, local pack, shopping carousel, video carousel, featured snippet. Each one is
a measurable subtraction from organic CTR.

Six features on a page-one SERP means the blue links are fighting over what is left. Feed the
count into the score (see Scoring above) rather than reporting a qualitative "high AIO risk."
This forces the live SERP pull that the workspace rules require anyway.

## Sprint Discipline: 25-50 Keywords per 30-90 Days

**Never hand over a 500-keyword target list.** Large sets create paralysis and low-quality work.

1. Pick ONE cluster to dominate.
2. Build the full keyword set for it (500-1,000 raw is fine as raw material).
3. Filter hard: raw set → ~100 → **25-50 final unique-intent topics**.
4. Execute that as a 30-90 day sprint, then declare it finished and pick the next cluster.

50 unique-intent topics already means roughly 25 page rewrites plus 25 new assets. That is a
full quarter of work. The value of the sprint frame is a **sense of completion** -- it matters
most for client/retainer work, which otherwise becomes a perpetual "doing SEO every month" loop
where nothing is ever finished and nothing is ever reportable.

## Local Keyword Rules

- **Only add a geo modifier where the answer genuinely VARIES by location.** "How much does an
  SEO consultant cost in St. Louis" is legitimate (pricing varies by market). "What is creatine
  in St. Louis" is algorithm manipulation and nobody searches it. **The test is location
  variability.**
- **Convert national queries into local ones** rather than hunting for local long-tail in tools.
  Take a Reddit thread or a PAA question with national phrasing and localize it where it makes
  sense. Local long-tail rarely exists in any keyword database.
- **GSC is the best local keyword source available**, better than any paid tool, because tools
  systematically lack local-modifier data. Start there on every local campaign.

## Extend Queries with Modifiers (do not accept AI's seed terms)

When AI generates topic ideas, treat yourself as the **editor, not the recipient**. The
characteristic AI failure is a seed term with weak intent that captures no long-tail:

- AI returns: `B2B SEO St. Louis` -- broad, unclear intent, captures nothing extra
- Correct target: `best B2B SEO agencies in St. Louis` -- ranks for the modifiers AND is the
  phrasing that earns the mention in an AI answer

Adding one or two modifiers **expands** long-tail capture rather than narrowing it. Do not avoid
this because it "changes the search volume" -- the volume number is not the goal.

## Five Stages of Customer Awareness (work BOTTOM-UP)

Prioritize in this order, narrowest first. Do not start at the top because the volume looks big.

| Stage | Query shape | Priority |
|---|---|---|
| **Most aware** | `hire [brand]`, `[brand] free trial`, `[brand] discount code` | Build first |
| **Product aware** | `[brand] review`, `[brand] vs [competitor]` | Second |
| **Solution aware** | **`best [solution]` (+ location)** | **The critical tier** |
| **Problem aware** | `why isn't my website ranking` | Fourth |
| **Unaware** | `how do I get more customers online` | Last |

**The `best [solution]` tier is the one to track in BOTH traditional search and AI answers.**
It is the query shape where you can measure whether the brand gets named in the AI response,
which is the single most useful visibility metric available. Starting at "unaware" because the
volume is seductive is the classic beginner error.

*(Awareness-stage methodology adapted from Nathan Gotch's SEO keyword research work. The
staging model is adopted here; his specific numeric scoring weights are not, as he describes
them as his own arbitrary weighting.)*

---

## Real-World Context: Keywords in the AI Search Era (Charles Floate, April 2026)

Traditional keyword research (volume + difficulty + intent) still matters, but it's no longer the full picture. Google AI Mode is ~68% of B2B queries, and LLM-native search (ChatGPT, Gemini, Perplexity) often skips the SERP entirely. When doing keyword research, keep in mind:

- **Citation queries ≠ ranking queries.** A keyword with low search volume in any tool might still drive significant revenue if it's a common prompt people ask ChatGPT. Think in terms of "what prompts would someone type into an LLM" alongside "what would they Google."
- **Conversational, long-tail phrasing wins in LLMs.** Prompt-style queries ("How do I set up X for Y") often outperform short head terms for AI visibility.
- **Intent matching matters more.** LLMs synthesize across queries, so covering the full intent cluster (how, why, best, vs., alternatives) beats obsessing over one exact match.
- **Check what's currently cited.** For high-value target queries, spot-check what ChatGPT and Perplexity cite today. That reveals the real competition, which is often not the top-10 Google results.

The practical consequence: human judgment about search intent and prompt phrasing beats a tool-dumped volume list. Treat the tool as one input, never the decision.
