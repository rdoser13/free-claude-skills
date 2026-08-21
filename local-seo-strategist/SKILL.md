---
name: local-seo-strategist
description: Improve a local business's visibility in Google organic search, the Google Map Pack (local 3-pack), and AI search results (ChatGPT, Perplexity, Google AI Overviews, Gemini). Use when the user says "local SEO", "rank in Google Maps", "Map Pack", "local 3-pack", "Google Business Profile", "GBP optimization", "rank my local business", "service area pages", "city landing pages", "local citations", "NAP consistency", "get more local leads", "AI search optimization", "get cited by ChatGPT", "GEO", or wants to improve where a service-area or storefront business shows up for "near me" and "[service] in [city]" searches. Works for any local business in any trade or city. Do NOT use for new website builds from scratch (use the Local Website Designer skill), national/non-local SEO, ecommerce, or general blog content.
version: 1.0.0
metadata:
# No external APIs required - procedural strategy skill
---

# Local SEO Strategist

An evergreen playbook for improving a local business's visibility across the three surfaces that drive local leads today:

1. **Google organic** (the blue links below the Map Pack)
2. **The Google Map Pack** (the local 3-pack + Google Maps)
3. **AI search** (ChatGPT, Perplexity, Google AI Overviews, Gemini, Copilot)

Most local SEO advice optimizes only the first two. This skill treats AI search as a first-class surface, because "near me" and "best [service] in [city]" queries are exactly where AI answers and Maps are taking share from classic blue links. A business that wins all three is durable. A business that wins only organic is exposed.

Works for any local business in any trade or market: home services (plumbing, HVAC, roofing, electrical, septic, crawl space, pest, landscaping), professional services (legal, dental, accounting, med spa), and storefronts (restaurants, salons, auto shops, retail).

---

## Important: Read This First

- **Reference brief:** If you have a local-SEO playbook you trust, read it before starting and apply its principles. The tactics that consistently matter: the Google Business Profile ranking levers, a review floor plus a steady monthly review velocity, a review-gating flow that routes unhappy customers privately, and automation for GBP posting and auto-reply.
- **The three surfaces need different work.** Don't conflate them. Organic is won with content + on-page + links. The Map Pack is won with a verified Google Business Profile + proximity + reviews + citations. AI search is won with entity clarity + structured data + being cited across the web. Diagnose which surface the business is losing on before prescribing fixes.
- **Diagnose before prescribing.** Always run the Diagnostic (Phase 1) first. Recommending GBP work to a business that has no website pages, or content to a business with a thin GBP, wastes the client's money.
- **No fabricated facts, ever.** Never invent review counts, years in business, customer numbers, neighborhoods, or local regulatory details. Verify every local claim before it goes in copy or a profile. Fabricated specifics are a credibility and liability risk.
- **No em dashes.** Use periods or regular hyphens. Scan output with `python3`, not grep (grep misses U+2014).
- **Every recommendation ships with priority + effort + expected impact.** See "Deliverable Standards" at the bottom. A finding with no priority is noise.

---

## Phase 1: Diagnostic (Always Start Here)

Before any work, find out where the business actually stands on each surface. Ask for or look up:

### Intake (collect what blocks the diagnosis; assume and label the rest)
1. Business name, primary city, and full service-area city list
2. Top 5 revenue services (these become the keyword + page priority)
3. Website URL (and platform: WordPress, Astro, Squarespace, Wix, etc.)
4. Google Business Profile status: claimed? verified? category? review count?
5. Physical storefront the public visits, or service-area business (SAB, no public address)?
6. Known competitors who currently rank (if any)
7. Primary goal: phone calls, form leads, foot traffic, or bookings?

If the business has no address the public visits, it is a **service-area business (SAB)** and that is normal and fully allowed by Google. SABs hide the address on the GBP but still get a verified profile. Do not treat "no storefront" as a blocker.

### Three-Surface Audit (run this for the primary "[service] in [city]" query)

| Surface | What to check | "Losing" signal |
|---|---|---|
| **Map Pack** | Does the GBP appear in the local 3-pack? Review count + rating vs. top 3 competitors? Primary category correct? | Not in top 3, or fewer/lower reviews than the businesses that are |
| **Organic** | Does a relevant page rank on page 1 below the pack? Is there a dedicated page for this service + city? | No dedicated page, thin content, or ranking page 2+ |
| **AI search** | Ask ChatGPT/Perplexity "best [service] in [city]" and "who does [service] in [city]". Is the business named? Cited? | Not mentioned, or competitors named instead |

Output a one-screen scorecard: where they stand on each surface, the single biggest gap, and the 3 highest-leverage fixes. Then route to the relevant phase below.

---

## Phase 2: Google Business Profile (Wins the Map Pack)

The GBP is the single highest-leverage local asset. The Map Pack sits above organic results and is where most "near me" clicks go. It is also a primary source AI assistants pull from for local intent.

### Setup + verification
- Claim or create the profile at business.google.com. Verify it (video verification is now the most common method).
- **Business name = the real legal/DBA name only.** Never keyword-stuff the name ("[Business] [City] Emergency 24/7 Cheap"). It is the #1 cause of suspensions and it no longer helps.
- **SAB profiles:** set service areas (list the cities served), hide the street address. A real address is still required for verification but stays private.

### Optimization checklist
- [ ] **Primary category** = the single most specific match for the trade (e.g., "Emergency dental service" not "Dentist"; "Septic system service" not "Contractor"). This is the biggest Map Pack ranking lever after proximity and reviews.
- [ ] Secondary categories added (up to 9) for every service offered
- [ ] Service areas list every target city
- [ ] Hours current, including holiday hours; mark 24/7 if true
- [ ] Business description (750 char max) uses primary + secondary keywords naturally (template below)
- [ ] Services/Products added, one per service, each linking to its matching website page
- [ ] Attributes selected (licensed, free estimates, online appointments, etc.)
- [ ] Photos: logo, cover, 5+ interior or job-site, 3+ exterior, team, 10+ service/product. Geo-authentic photos beat stock.
- [ ] Google Posts published weekly (offers, jobs completed, tips)
- [ ] Q&A section seeded with 3-5 real questions and answered
- [ ] Messaging enabled if the business can respond fast

**GBP description template (750 chars):**
```
[Business Name] provides [primary service] in [City] and the surrounding
[Region/County] area. We serve [City 1], [City 2], and [City 3] with
[service 2] and [service 3]. [One concrete differentiator: years, license,
guarantee]. [Credibility line: licensed and insured / X years serving Region].
Call [phone] for a free estimate.
```

### Reviews (the Map Pack flywheel)
Reviews drive both ranking and click-through. Velocity and recency matter as much as total count.
- Ask at the moment of peak satisfaction (job done, problem solved).
- Remove friction: QR code, direct review link, in-person tablet for storefronts.
- Follow up by SMS/email within 24 hours of service.
- Treat it as a daily system, not a one-time sprint. A steady trickle beats a one-week spike (which can look manipulative).
- **Respond to every review within 24 hours.** Thank positives by name and mention the service + city (a natural keyword signal). Handle negatives by acknowledging, apologizing, and taking it offline. Never use canned identical responses.

**SMS request template:**
```
Hi [Name], thanks for choosing [Business]! A quick Google review helps
a ton and takes under a minute: [Direct Review Link]
```

---

## Phase 3: On-Page + Content (Wins Organic)

Organic ranking for local intent is won with one dedicated, genuinely useful page per service + city, plus on-page signals. For the page templates, copy voice rules, and full meta/JSON-LD patterns, the **Local Website Designer** skill is the source of truth. This skill covers the SEO strategy layer on top of it.

### Service + City page strategy
- Build a **service x city matrix.** Each cell is one potential page. Prioritize by the business's revenue services and the cities with real demand.
- **Each page must be genuinely unique** (target ~60% unique content). Google treats find-and-replace city pages as doorway pages and ranks none of them. Make each one demonstrate local knowledge: neighborhoods, terrain, local regulations or permit bodies, common local issues. Verify every local fact.
- **Scaling rule:** more than 5 services or 12 cities dilutes link equity across thin pages. Pick the top 5 services for dedicated pages; group extra cities by county/region. Depth beats breadth.

### Local keyword formulas
- **Head:** `[service] in [city]`, `[service] near me`, `best [service] [city]`, `[service] company [city]`
- **Long-tail:** `emergency/24 hour/affordable [service] [city]`, `[service] near [landmark]`, `[service] in [neighborhood]`
- **Question (these feed FAQs AND AI search):** `how much does [service] cost in [city]`, `who is the best [service] in [city]`, `what is the average price for [service] in [city]`

### On-page implementation per page
- Primary keyword in: URL slug, title tag (under 60 chars), meta description (under 160), H1 (one per page), one H2, and the first 100 words
- Stacked `[Service] in [City]` H2s on location pages drive keyword relevance without spam
- Closely related phrases, not just exact repeats (a roofer pairs "roof repair" with "shingle replacement" and "storm damage roofing"; a med spa pairs "Botox" with "wrinkle treatment" and "injectables")
- Descriptive image alt text: `[service] [city] [visual detail]`
- Internal links: every service page links to relevant city pages and vice versa, with varied geo-modified anchor text (not bare "click here" or repeated identical anchors)

### Supporting content engine (Tier 2)
Blog or resource posts that target long-tail and question keywords, then internally link to the money pages. Proven post types:
- **Symptom/diagnostic:** "Signs you need [service]"
- **Comparison:** "[Service A] vs [Service B]: what's the difference"
- **Seasonal/local:** "Best time of year for [service] in [State]"
- **Cost:** "How much does [service] cost in [city]?"
- **Local listicle:** "Best [service] companies in [city]" (see the outreach tactic in Phase 4)

Before writing any post, **cannibalization-check** it against existing pages so two pages don't compete for the same keyword.

---

## Phase 4: Citations + Backlinks (Supports Both Organic and the Map Pack)

### NAP consistency
NAP (Name, Address, Phone) must be **byte-for-byte identical** everywhere: same abbreviations, punctuation, suite format. Inconsistent NAP confuses both Google's entity matching and AI assistants.
1. Establish the one canonical NAP format.
2. Audit existing listings (search `[business name] + directory`).
3. Correct discrepancies, then submit to new directories using the canonical format.
4. For SABs with no public address: keep Name + Phone identical everywhere and use directories that accept service-area businesses without a street address.

### Citation directory tiers
- **Tier 1 (do first):** Google Business Profile, Bing Places, Apple Business Connect, Yelp, Facebook
- **Tier 2 (high authority):** Yellow Pages, BBB, Foursquare, Nextdoor, MapQuest, Superpages, DexKnows
- **Tier 3:** Industry-specific directories for the trade
- **Tier 4:** Local: chamber of commerce, regional business directories, local news listings

**Reality check on citations (hard-won):** the high-domain-authority aggregators (YellowPages, Superpages, DexKnows, etc.) carry real ranking signal. Dozens of low-authority filler directories mostly count toward NAP consistency, not ranking. Build the heavy hitters first and stop chasing diminishing returns on filler. Quality and consistency over raw count.

### Backlinks (ordered by effectiveness)
1. **Local listicle / "best of" inclusion** (often the easiest real link)
2. Guest posts on industry blogs with contextual links to service pages
3. Competitor backlink analysis: find their link sources, replicate the gettable ones (filter aggressively; spammy niches have ~85% junk backlinks, the signal is the other 15%)
4. Local news/media coverage via story pitches and press releases
5. Sponsorships of local events, charities, sports teams (local relevance + link)
6. Chamber of commerce and business association memberships
7. Partnerships with complementary local businesses (cross-links)

**Outreach tactic that compounds:** publishing your own "Best [service] companies in [city]" listicle that honestly features real competitors gives you a warm outreach hook ("you're featured on our [city] guide") for partnerships, links, and referrals later.

---

## Phase 5: AI Search + GEO (Wins ChatGPT, Perplexity, AI Overviews)

This is the surface most competitors ignore and the one gaining share fastest. Generative Engine Optimization (GEO) means making the business easy for an LLM to **understand as an entity** and **cite as an answer.**

### Why local businesses are exposed here
AI assistants answer "best [service] in [city]" directly, often without a click. They synthesize from: the business's own site (especially the homepage and clearly structured pages), the Google Business Profile and Maps data, reviews, and third-party mentions/citations across the web. A business with a thin web presence and few mentions simply won't be named.

### What moves AI visibility
- [ ] **Entity clarity.** One consistent business name, NAP, and description everywhere (this is why Phase 4 NAP consistency feeds AI search). LLMs build an entity from repeated, consistent signals.
- [ ] **Comprehensive, conversational FAQ sections** using the exact question phrasing people use. AI extracts answers from clean Q&A. Pair with **FAQPage schema.**
- [ ] **Clean structured data.** LocalBusiness/Service/FAQPage/Review JSON-LD gives machines unambiguous facts (name, services, area served, phone, hours, ratings). Validate at validator.schema.org.
- [ ] **Strong, fact-dense homepage and About page.** LLMs frequently surface homepages and entity pages. State plainly who you are, what you do, where, and the credentials (E-E-A-T: experience, expertise, authoritativeness, trust).
- [ ] **Third-party corroboration.** Being named in local listicles, directories, and media gives the model independent sources that confirm the business exists and is relevant. The same citations from Phase 4 do double duty here.
- [ ] **Reviews on Google and elsewhere.** AI assistants summarize sentiment and frequently name well-reviewed local options.
- [ ] **Direct, extractable answers in copy.** Lead sections with the answer, then explain. "We offer same-day [service] in [city]. Here's what's included..." extracts cleanly; a meandering intro does not.

### GEO testing loop (do this for real, monthly)
1. Ask ChatGPT, Perplexity, and Google (AI Overview) the top 3-5 local queries the way a customer would phrase them.
2. Record: is the business named? cited with a link? Who is named instead?
3. Diagnose the gap (no FAQ schema? not in the listicles the AI cited? thin homepage? few reviews?).
4. Fix the diagnosed gap.
5. Re-test next month. AI answers shift, so this is ongoing, not one-time.

### Schema starting points
Use the full JSON-LD blocks (LocalBusiness, Service, BreadcrumbList) from the **Local Website Designer** skill. For GEO specifically, also ensure:
- **FAQPage** schema on every FAQ section
- **Review / AggregateRating** where genuine reviews exist (never fabricate)
- **areaServed** populated with every target city on LocalBusiness/Service schema

---

## Execution Roadmap

| Phase | Timeframe | Focus |
|---|---|---|
| Foundation | Weeks 1-2 | Diagnostic scorecard, GBP claim + full optimization, NAP audit, review system launch |
| Content | Weeks 3-6 | Top service + city pages, Tier 1-2 citations, on-page fixes |
| Authority + AI | Weeks 7-12 | Backlink + listicle outreach, FAQ + schema buildout, GEO testing loop, long-form content |
| Scale | Ongoing | New city pages, review velocity, monthly GEO + rank monitoring, Google Posts cadence |

### Monitoring cadence (set expectations honestly)
- **Search Console / Bing impressions:** first movement in 2-3 weeks for a new or newly-optimized page.
- **Organic position:** page 2 by week 6-8, page 1 attempts month 3-4 if content + citations + a few real backlinks land. Local SEO is a months-not-weeks game; say so up front.
- **Map Pack:** moves with reviews + category + proximity; reviews are the fastest lever.
- **AI search:** re-test monthly; expect lag behind organic.

---

## Recursive Audit Loop (for client work)

For paid engagements, run the **generate -> evaluate -> diagnose -> improve -> repeat** loop before delivering:
1. Generate the recommendations or page copy.
2. Evaluate against this skill's checklists with explicit pass/fail (not "looks good").
3. Diagnose what failed and why (verify every local fact, scan for em dashes, confirm NAP consistency, confirm priority labels present).
4. Rewrite to fix.
5. Re-score until everything passes.

---

## Deliverable Standards

Every recommendation in a deliverable includes:
- **Priority:** High / Medium / Low
- **Effort:** Hours / Days / Weeks
- **Expected impact:** 1-10
- **Surface it affects:** Map Pack / Organic / AI search (often more than one)
- **Step-by-step instructions** using the client's real business name, services, and cities
- **Success metric + how it's tracked**

Always offer both a DIY path and a done-for-you path. Flag any tactic that risks a Google guideline violation (keyword-stuffed GBP names, fake reviews, doorway pages, PBN links) and recommend the compliant alternative instead.

---

## Related Skills

- **Local Website Designer** (`/Local Website Designer.md`): builds the site this skill optimizes. Page templates, copy voice, full meta + JSON-LD blocks, and the pre-launch audit live there. Invoke it for net-new builds; invoke this skill to improve an existing site's local visibility. The natural handoff: Designer's launch is this skill's starting line.
