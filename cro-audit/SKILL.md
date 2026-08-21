---
name: cro-audit
description: Evergreen Conversion Rate Optimization audit and build-check skill. Audits any landing page, sales page, lead gen form, homepage, pricing page, or blog post against a 25-point CRO framework plus a library of proven SaaS conversion patterns. Use when user says "CRO audit", "conversion audit", "audit this landing page", "review my sales page", "check this lead form", "improve conversions", "why isn't this converting", or shares a URL/screenshot/HTML and asks for feedback. Also use as a pre-ship gate before delivering any new landing page, sales page, or opt-in form.
version: 1.1.0
---

# CRO Skill

A 25-point Conversion Rate Optimization framework plus a proven-patterns library for auditing existing pages and validating new builds before they ship. Works for landing pages, sales pages, lead gen forms, homepages, pricing pages, blog posts, and checkout flows across any industry.

## Two Modes

This skill operates in two modes. Pick the one that matches the user's request.

### Mode A: Page Audit
The user shares an existing page (URL, screenshot, HTML, or description) and wants feedback.

**Deliver:**
1. **Pass/Fail scorecard** for all 25 items (table format)
2. **Top 5 failures ranked by conversion impact** (highest impact first)
3. **One specific fix per failure** — concrete, copy-pasteable, not vague
4. **Quick-win priority list** — what to fix this week vs. test next

### Mode B: Pre-Ship Build Check
The user is building a new page and wants to validate it before delivering.

**Rule:** Do not ship a page that fails any of items 1-5 (headline, above-fold value prop, CTA psychology, 5-field form max, message match). These are non-negotiable. Items 6-25 should pass at a minimum 80% rate.

Run the full 25-point check, fix every failure, and only then deliver.

## The 25-Point Framework

### Fundamentals (Items 1-5) — NON-NEGOTIABLE on new builds

**1. Headline 4-U Formula**
Headline must be Useful, Unique, Urgent, Ultra-Specific. 80% of visitors won't read past it.
- *Fail signal:* generic ("Welcome to..."), feature-first, no specificity, no benefit.
- *Pass example:* "Get 10 Qualified Leads in 30 Days, Without Cold Calling."

**2. Above-Fold Value Proposition**
Customer problem focus, not company story. Zero scroll required to understand the offer.
- *Fail signal:* "We are a..." / "Founded in..." / scroll required to see what they sell.
- *Check:* Cover everything below the fold. Can a stranger tell what this is and who it's for in 5 seconds?

**3. CTA First-Person Psychology**
"Get MY guide" outperforms "Get YOUR guide" by ~90%. Write CTAs in the visitor's voice.
- *Fail signal:* "Get Your Free Demo", "Download Your Report".
- *Fix:* "Send Me the Guide", "Show Me My Score", "Start My Free Trial".

**4. 5-Field Form Maximum**
Every additional form field kills conversions. Use progressive profiling for the rest.
- *Fail signal:* >5 fields on first opt-in, asking for phone before email is validated.
- *Fix:* Start with email only. Capture name/company/role post-conversion or via enrichment.

**5. Message Match Precision**
Ad copy headline = landing page headline. Broken promises = instant bounce.
- *Fail signal:* Ad says "AI Marketing Templates", LP headline says "Welcome to [Brand]".
- *Fix:* Mirror the exact promise (and keyword) from the inbound source.

### Persuasion & Psychology (Items 6-10)

**6. Social Proof Near CTAs**
Testimonials with faces + names placed at decision points (next to CTAs, near pricing, after objections).
- *Fail signal:* Logos-only, anonymous quotes, social proof buried in a separate section.

**7. Cognitive Bias Stack**
Layer loss aversion (fear of missing out), social proof (others doing it), and anchoring (price comparison).
- *Pass:* "Join 4,600+ marketers" + "Spots fill in 48 hours" + "Normally $497, today $97".

**8. PAS Copy Framework**
Problem, Agitate, Solve. Emotion before logic. Sales copy that opens with features fails.
- *Fail signal:* Body copy opens with "Our platform features...".

**9. Genuine Urgency Only**
Real deadlines, real seat limits. Fake countdown timers destroy trust forever once spotted.
- *Fail signal:* Resetting countdown timer, "Only 3 left" that's been there for a month.

**10. Price Anchoring Display**
Show the expensive option first. Make the real price feel like relief.
- *Pass:* "Agencies charge $5,000/mo. Our system: $97."

### Trust & Clarity (Items 11-15)

**11. Trust Signal Clustering**
Security badges, guarantees, refund policies, certifications visible together, usually near the CTA and at the footer.

**12. Visual Hierarchy F-Pattern**
Eyes scan in an F-shape (top horizontal, second horizontal, left vertical). CTAs and value props belong in that path.
- *Fail signal:* Primary CTA bottom-right, value prop centered low.

**13. Lead Magnet Hierarchy**
Templates > Checklists > Guides > Ebooks > Webinars. Instant gratification beats delayed.
- *Fix:* Reposition "Free 47-page guide" as "Free template you can use in 2 minutes".

**14. Objection Preemption**
Address the top 3 buyer concerns before they're consciously thought. FAQ near the CTA.
- *Top 3 to find:* price, time/effort, "will this work for me?"

**15. Mobile Thumb Zone**
Primary CTAs sit where thumbs naturally rest (bottom 1/3 of screen, center). No stretching, no zooming.
- *Test:* Open on a phone with one hand. Can you tap the CTA without shifting grip?

### Copy & Structure (Items 16-20)

**16. One-Variable Testing**
Change ONE thing per test (headline OR CTA OR image, never all three). Measure, then compound.
- *Fail signal:* "We redesigned the whole page and conversions went up/down 10%."

**17. Post-Conversion Momentum**
The thank-you page is prime real estate. Sell the next step while excitement peaks (tripwire, upsell, share-to-unlock, book-a-call).
- *Fail signal:* Blank "Thanks!" page with no next action.

**18. Cart/Lead Recovery Sequence**
Email at 1 hour, retarget ad at 4 hours, incentive (discount/bonus) at 24 hours.
- *Fail signal:* No abandonment sequence at all, or 1 email 3 days later.

**19. Reading Level Grade 6**
Smart people prefer simple. 11-word sentences. Short paragraphs (1-3 lines). Cut adjectives.
- *Test:* Paste into Hemingway. Aim for Grade 5-6.

**20. ToFu / MoFu / BoFu Logic**
Awareness content is not decision content. Match the offer to intent.
- *ToFu:* free content, blog, lead magnet. *MoFu:* case studies, webinars, comparisons. *BoFu:* demo, trial, pricing, checkout.

### Design & Conversion Mechanics (Items 21-25)

**21. White Space = Focus**
Empty space makes CTAs impossible to miss. Crowded = confused = bounce.
- *Fail signal:* Three CTAs visible, four colors, two competing offers in one section.

**22. Benefit-First Language**
Features tell. Benefits sell. Transformations compel.
- *Fail:* "AI-powered scheduling engine." *Pass:* "Get your week back by Friday."

**23. Micro-Commitment Ladder**
Small yes leads to big yes. Start with email only. Then survey. Then book a call. Then buy.
- *Fail signal:* First CTA on a cold page is "Buy Now $497".

**24. Performance Tracking Stack**
Heatmaps (Hotjar/Microsoft Clarity) show *where* problems are. Session recordings show *why*. Event tracking (GA4/PostHog) shows *what* converts.
- *Audit question:* Can the user even see what's failing? If no tracking, that's failure #1.

**25. Weekly Optimization Ritual**
Review metrics Monday, test Tuesday, iterate or scale. CRO compounds; one-off audits don't.

## Proven Patterns from High-Converting SaaS Pages

These are evergreen, observed-in-the-wild patterns from SaaS sites that convert well on cold paid traffic. Use them as a reference library when auditing or building.

### Headline & Hero Patterns

- **Outcome + timeframe + zero-effort headline.** Format: `[High-value outcome]. In [shockingly short time].` Subhead breaks the mechanism into a 3-step verb sequence (e.g., "Drop a topic. Pick a template. Walk away with finished posts."). Sells the result first, then the simplicity.
- **Repeat the primary CTA twice above the fold** — once in the sticky nav, once in the hero. Use the exact same button text both places.
- **Lead with a secondary CTA for skeptics.** Pair the primary CTA with a low-commitment option like "See how it works" that scrolls to features. This catches visitors who aren't ready to convert yet but would otherwise bounce.

### CTA Copy Patterns That Outperform

- **Trial-framed CTAs beat purchase-framed CTAs on cold traffic.** "Start free week →" outperforms "Sign up" or "Buy now". The trial frame removes commitment objection.
- **Use a directional arrow (→) on every primary CTA.** It adds visual momentum and lifts CTRs measurably.
- **Keep CTA text identical across every plan/tier** on pricing pages. Variation in button copy confuses visitors and shifts the decision from "which plan" to "which button" — kills conversion.

### Social Proof Patterns

- **Quantified user count in eyebrow text above the hero or under the fold:** `TRUSTED BY [N]+ [SPECIFIC ROLE]`. Specific role ("business owners", "founders", "operators") outperforms generic ("users", "customers").
- **Testimonials need 3 attribution layers: photo + name + role/location.** Anonymous quotes register as fake. Add city/country for B2B SaaS — it implies real distribution and adds credibility.
- **Founder credibility badges** (press logos, follower counts, results metrics) belong near the hero, not buried in the about page. Operator-built signals trust on creator/SMB pages.
- **Stack 20+ testimonials vertically** rather than 3 in a carousel. Volume itself is a proof signal. Carousels hide proof; vertical stacks let visitors scan and self-select the one that matches them.

### Pricing Page Patterns

- **Three tiers with the middle one badged "MOST POPULAR".** Decoy pricing — anchors visitors away from the cheapest and toward the middle. The middle tier should be ~3-4x the entry tier in price.
- **State annual discount in plain language, not as a toggle by default.** A toggle adds a decision step; a single line ("annual plans save ~17%") in the FAQ converts better when paired with bonus credits or perks.
- **Add a sticky footer bar on pricing pages** with three pieces of info comma-separated: `[STARTING PRICE] · FREE [N]-DAY TRIAL · CANCEL ANYTIME`. Visible during scroll, persistent reassurance.
- **Soft guarantee outperforms aggressive money-back.** "If something doesn't work, email us within 14 days and we'll make it right" reads more human and trustworthy than "100% Money Back Guarantee" badges that look like 2012 affiliate sites.

### Objection Handling Patterns

- **Include a "Who this is NOT for" section.** Counter-intuitive but converts. Honesty about fit increases trust from the right audience and disqualifies bad-fit leads who'd churn anyway.
- **FAQ goes late on a sales page, early on a pricing page.** Sales page = emotion before logic (item 8, PAS). Pricing page = visitor is already considering, needs rational defense fast.
- **Address the effectiveness objection directly.** For any tool that automates a marketing channel, include an FAQ that names the visitor's fear (e.g., "Will scheduling posts hurt my reach?"). Saying it out loud disarms it.

### Blog Post CRO Patterns (the highest-leverage, least-used)

Blog posts are the #1 missed CRO surface. Apply these on every post:

- **In-line callout box after the intro** (within first 25-30%, matches item #5 on CTA placement). Format: small boxed unit with trial terms + CTA button. Example: `Free [N]-day trial · Cancel anytime [Start free week →]`.
- **Second in-line CTA after the section that establishes "who this is for"** — once the reader has self-identified, the CTA converts at peak intent.
- **End-of-post CTA modal box** with the hero headline of the site condensed to one line, followed by the same primary CTA button. Reuse hero copy; don't invent new copy here.
- **Comparison tables with no CTA inside them.** Let the table do the persuasion work. Adding a CTA inside the table reads as sales-y and undermines the "objective comparison" frame. Put the CTA in a callout box immediately after the table.
- **Skip newsletter popups on comparison/BoFu posts.** These visitors are decision-stage; newsletter signup is the wrong micro-commitment. Send them to trial.
- **Internal links weave the product narrative.** Link to `/pricing` 3+ times within a long-form post, plus 2-3 sister comparison posts. Anchor text should be specific ("[product] pricing page", "[competitor] alternatives") not generic ("click here").
- **Author bio carries authority, not CTA.** Don't stuff a CTA into the author bio. Use the bio to credentialize (credentials, follower count, results). The trust transfers to the body CTAs.

### Visual & UX Patterns

- **Numbered feature cards (01-08)** outperform unnumbered grids. Numbering implies completeness and creates a "must-see-all" effect.
- **Sticky nav with one CTA, never two.** Two sticky CTAs create decision paralysis on every scroll.
- **No exit popups on product/pricing pages.** Exit popups belong on blog posts or lead magnet pages where the visitor wasn't going to buy anyway. On a pricing page they read as desperate and reduce trust.
- **Carousel of real product screenshots** beats marketing illustrations every time. Show the actual UI the user will land in post-signup.

## How to Run an Audit (Mode A)

### Step 1: Gather Inputs
Ask only if blocking:
- URL or screenshot of the page
- What's the goal of this page? (email opt-in, demo book, sale, etc.)
- What traffic source? (cold ads, SEO, email list, referral) — needed for items 5, 20
- Current conversion rate if known

If the user pastes a URL, fetch it. If they paste HTML/screenshots, work from those.

### Step 2: Score All 25 Items
Output a markdown table:

| # | Item | Status | Note |
|---|------|--------|------|
| 1 | Headline 4-U | ❌ FAIL | Headline is feature-first, no urgency or specificity |
| 2 | Above-fold value prop | ✅ PASS | Clear in 3 seconds |
| ... | | | |

### Step 3: Rank Top 5 Failures by Impact
Impact ranking heuristic (highest to lowest):
1. Items 1-5 (fundamentals) always rank highest if failing
2. Items affecting the primary CTA path (3, 6, 12, 15, 21)
3. Items affecting trust at decision points (11, 14)
4. Copy/structure items (8, 19, 22)
5. Everything else

### Step 4: Specific Fix Per Failure
Each fix must be **copy-pasteable or a concrete design instruction.** Not "improve your headline" — write the actual replacement headline. Reference the Proven Patterns library above when the fix matches a known winning pattern.

### Step 5: Quick-Win Priority
Close with:
- **Fix this week (high impact, low effort):** [list 2-3]
- **Test next (high impact, needs A/B):** [list 2-3]
- **Long-term (structural):** [list 1-2]

## How to Run a Pre-Ship Check (Mode B)

Before delivering any net-new landing page, sales page, or lead form:

1. Run the 25-point check internally
2. If ANY of items 1-5 fail → fix before delivery (do not ship)
3. If <80% of items 6-25 pass → flag the gaps in delivery notes with proposed fixes
4. Cross-reference Proven Patterns library — apply at least 5 patterns relevant to the page type
5. Include a one-line summary in delivery: "CRO check: 23/25 passed. Flagged #14, #18 — see notes."

## Output Style Rules

- No em dashes. Use regular hyphens, periods, or commas.
- Grade 6 reading level in all written recommendations.
- Be specific — write the replacement copy, don't describe it.
- No fluffy openings ("Great question!"). Get to the audit.
- Skip FAQs and CTAs in audit deliverables unless explicitly requested.

## When NOT to Use This Skill

- Pure copywriting requests with no conversion goal (use a copy skill instead)
- Brand strategy or positioning work (this is page-level optimization)
- Technical SEO audits (use the SEO Audit Skill)
- Email body optimization (use the relevant email skill, though items 3, 8, 19, 22 still apply)
