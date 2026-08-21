---
name: landing-page-designer
description: Builds high-converting single-page landing pages for digital products, services, local businesses, lead magnets, and offer pages. Outputs production-ready HTML/CSS/JS using a proven anatomy (hero, social proof, how-it-works, features, benefits, reviews, FAQ, repeated CTA). Use this skill when the user asks for a landing page, sales page, offer page, product page, opt-in page, or "one-pager" - not for full multi-page websites.
version: 1.0.0
---

# Landing Page Designer

This skill builds conversion-focused single-page landing pages. One offer. One audience. One primary CTA repeated throughout the page. The goal is not a "website" - it's a page that turns a visitor into a buyer, lead, or booked call.

If the user wants a multi-page site, use the Web Designer skill instead.

## Inputs to Gather

Before writing code, collect (ask only what's missing - infer the rest):

1. **Offer** - What is being sold or given away? Price, format, delivery.
2. **Audience** - Who is this for in one sentence? What pain are they in right now?
3. **Primary CTA** - The single action the page must drive (Buy, Book a Call, Get Quote, Download, Call Now, Subscribe).
4. **CTA destination** - Stripe checkout URL, Calendly link, phone number (`tel:`), form, etc.
5. **Proof** - Real reviews, testimonials, star ratings, client logos, screenshots, case study numbers. Use only what's real.
6. **Brand** - Colors, fonts, logo, voice. If none provided, pick a bold direction and commit.
7. **Visual proof asset** - Screenshot, product mockup, terminal mockup, before/after photo, hero image of the team/work.

If the user has no proof yet, do not invent testimonials, star ratings, review counts, or client names. Leave the section out or use a single honest line of positioning instead.

## The Proven Landing Page Anatomy

Use this section order as the default. Remove sections rather than add new ones. Most high-converting landing pages have 6-9 sections.

1. **Sticky Top Bar (optional)** - One line: phone number, urgency, or trust signal. Click-to-call on mobile (`<a href="tel:...">`) is non-negotiable for local/service businesses.
2. **Nav** - Logo left, single CTA button right. No menu links. The page is the menu.
3. **Hero** - The most important section. See "Hero Formula" below.
4. **Social Proof Strip** - Logos, star rating + review count, "as seen in," or a single named testimonial. Goes immediately under the hero to validate the claim before the visitor scrolls further.
5. **How It Works (3 Steps)** - Numbered 1-2-3. Reduces perceived friction. Every offer can be framed as 3 steps. Local/service: "Call → Pick a Time → We Come to You." Digital product: "Buy → Download → Install in Claude Code." SaaS: "Sign Up → Connect → Automate."
6. **What's Included / Services / Features** - A grid (3 or 4 columns desktop, 1 column mobile). Each card = icon or check + 2-5 word title + one-line description. For digital products, lean on a long check-marked list with a final "+ X more" line.
7. **Why Choose Us / Differentiators** - 3-6 reasons framed as benefits, not features. Each one answers a specific objection. ("Same equipment as any tire shop" answers "are mobile guys actually pros?")
8. **Visual Proof Block** - Terminal mockup, product screenshot, before/after, photo of work, or short video. This is where the page becomes believable.
9. **Reviews / Testimonials** - 3-5 real quotes with name and role (and photo if available). Star ratings only if real. Pull from Google, Stripe, Skool, Trustpilot, email replies, DMs.
10. **Bottom CTA Block** - Restate the offer, the price (or "Free Quote"), and the CTA button. Add light urgency if real ("Same-day install," "Lifetime updates," "Limited spots").
11. **FAQ** - 4-8 questions in a `<details>` accordion. Answer the real objections (price, refunds, time, "does this work for me?"). Do not add filler FAQs.
12. **Footer** - Minimal. Copyright, contact info, links to legal pages if they exist.

CTA buttons appear at minimum 3 times: hero, mid-page, bottom CTA block. All go to the same destination.

## Hero Formula

The hero is the page. If the hero fails, nothing else matters.

**Structure (top to bottom):**
- **Eyebrow line (optional)** - Location, category, or audience qualifier. ("Mobile Tire Shop in Des Moines" / "For Marketers Using Claude Code")
- **Headline** - One sentence. Names the outcome or the transformation, not the product category. 6-14 words. ("New Tires Delivered & Installed Right Where You Are" / "Get the 20+ Claude Code skills I use daily to drive six figures in revenue")
- **Subheadline** - 1-2 sentences. Explains what it is and removes the biggest friction. ("Skip the tire shop. We bring new tires, expert installation, and full-service repairs to your driveway, office, or job site.")
- **Primary CTA button** - Action verb + outcome. ("Get Instant Access →", "Call (555) 555-5555", "Book a Free Estimate")
- **Trust line under CTA** - Tiny text removing risk. ("Secure checkout via Stripe · Instant delivery" / "4.8 Stars on Google · Veteran-Owned · Same-Day Service")
- **Hero visual** - To the right on desktop, below on mobile. Terminal mockup, product screenshot, photo, or illustration. If nothing else exists, build a CSS terminal mockup showing the product in use.

**Hero rules:**
- No carousels. No video that autoplays with sound. No three-paragraph hero copy.
- The CTA must be visible above the fold on desktop AND mobile.
- The headline must name the outcome the customer wants, not your category.

## Layout Patterns by Page Type

### Digital Product / Info Product (Stripe checkout)
Dark theme works well. Hero with terminal/product mockup. "What's Included" as a long checkmark list. "Built For" section calling out 3-4 specific audience types. Testimonials. Bottom CTA with price. FAQ. One-time price beats subscription framing for cold traffic.

### Local Service Business
Light theme, bold accent color (red, blue, orange). Sticky click-to-call bar on top. Hero with photo of team/truck/work + headline naming the city. Star rating + review count under hero. "How It Works" in 3 steps. Services grid. "Why Choose Us" bullets answering objections. Real Google reviews. Service area mention. Phone number repeated 4+ times on the page.

### Lead Magnet / Opt-in
Strip everything. Hero + 3-bullet "what's inside" + email form + 1-2 testimonials + footer. No FAQ, no extra sections. Goal is email capture, nothing else.

### Booking / Consultation Page
Hero with outcome-focused headline. "Who this is for" / "Who this is not for" section (this filters bad leads). Process in 3 steps. Testimonials from clients with results. Embedded Calendly or booking form. FAQ. No price unless price is the filter.

### SaaS / Tool Landing Page
Hero with product screenshot or short loop video. Social proof strip with logos. Feature grid (3-6 features). "How it works" 3-step. Pricing tier block (or "Start Free" if freemium). Testimonials. FAQ. Footer with full nav (SaaS pages do get more footer links).

## Design Defaults (when no brand is provided)

Commit to one direction. Do not blend.

**Option A - Dark Premium (good for digital products, SaaS, agencies):**
- Background: `#0f0f1a` to `#1a1a2e`
- Text: `#e0e0e0` body, `#ffffff` headings
- Accent: one vivid color (`#0693e3` cyan, `#00d084` green, or `#ff5722` orange)
- Fonts: `Sora` or `Space Grotesk` headings + `Inter` body (Google Fonts)
- Subtle gradient mesh or noise background in hero

**Option B - Bold Service Business (good for local/trades/health):**
- Background: white
- Accent: one strong brand color (red `#c8102e`, blue `#1e40af`, orange `#ea580c`)
- Text: near-black `#111` headings, `#374151` body
- Fonts: `Outfit` or `Plus Jakarta Sans` headings + `Inter` body
- Photography-heavy. Real photos beat stock every time.

**Option C - Editorial / Minimal (good for consultants, premium offers):**
- Off-white background `#fafaf7`
- Black text
- One accent color used sparingly
- Serif display font (`Fraunces`, `Instrument Serif`) + sans body
- Generous whitespace, large type, no decorative elements

Avoid: generic purple gradients on white, Inter as the only font, three-column stock-icon feature grids with no real copy, fake testimonials, AI-generated headshots in review sections.

## Copy Rules

- 8th-grade reading level. Short sentences (8-15 words). Active voice.
- Headlines sell the outcome, subheads handle the mechanism, body removes objections.
- Every section should answer a question the visitor is silently asking ("Is this for me?" "Does it actually work?" "What does it cost?" "What if it doesn't work?").
- Use specifics. "4.8 stars from 143 Google reviews" beats "loved by customers." "1,400-word SEO blog post in 90 seconds" beats "fast content creation."
- Repeat the CTA copy across the page. Consistency reinforces the action.
- Do not pad with adjectives. If the line works without the word, cut it.

## Technical Defaults

- **Single `index.html`** with internal CSS in `<style>` and minimal JS. No build step. No framework. No dependencies beyond Google Fonts.
- **Mobile-first.** Design the mobile layout first, then enhance for desktop with `@media (min-width: 768px)`.
- **Performance.** Inline critical CSS. Lazy-load images below the fold (`loading="lazy"`). Compress images before embedding.
- **Accessibility.** Real heading hierarchy (one `h1`, then `h2`s for sections). Alt text on every image. Buttons that look like buttons. Color contrast minimum 4.5:1.
- **Click-to-call.** `<a href="tel:+15555555555">` on every phone number for local/service pages.
- **Form handling.** For email capture, use Kit, ConvertKit, Mailchimp, or Formspree. Never hand-roll a backend for a landing page.
- **Checkout.** For digital products, point the CTA directly at the Stripe payment link. No backend needed.
- **Analytics.** Drop in Google Tag Manager or a single GA4 snippet. Add a `data-cta` attribute to CTA buttons for event tracking.

## Deployment

- Push the folder to GitHub, connect to Cloudflare Pages or Vercel. Build command: none. Output: `/`.
- Use a subdomain for product/offer pages (`get.yourdomain.com`, `skills.yourdomain.com`, `quote.yourdomain.com`) rather than nesting under a CMS. This avoids theme conflicts and gives full design control.
- Every Git push auto-deploys. That's the whole pipeline.

## Workflow

1. **Confirm the offer, audience, and primary CTA** in one or two questions max. Do not survey the user.
2. **Pick a design direction** from the three options above (or apply the user's brand) and commit to it.
3. **Write the hero first.** Headline, subhead, CTA, trust line. Do not move on until the hero sells.
4. **Build the page top-to-bottom** following the anatomy. Cut sections rather than thin them out.
5. **Add real proof only.** If proof is missing, leave the slot empty and flag it to the user.
6. **Review against the conversion checklist** below before delivering.
7. **Output one `index.html` file** the user can open locally and deploy immediately.

## Pre-Delivery Conversion Checklist

Run through this before saying the page is done. Every "no" is a fix.

- [ ] The headline names the outcome the customer wants - not the product category.
- [ ] The primary CTA is visible above the fold on mobile.
- [ ] The same CTA appears at least 3 times on the page, all pointing to the same destination.
- [ ] There is at least one real piece of social proof in the first screen or right under the hero.
- [ ] Every section answers a question a skeptical visitor would ask.
- [ ] There is no fabricated testimonial, review count, star rating, or client logo.
- [ ] The page works on mobile (test at 375px width).
- [ ] Phone numbers are click-to-call (for local/service pages).
- [ ] The page has 6-9 sections, not 15.
- [ ] The FAQ answers real objections, not filler ("What is this?" type questions).
- [ ] Load time feels instant on mobile (no heavy hero video, images compressed).

## What This Skill Is Not For

- Multi-page websites (use Web Designer)
- Blog posts (use SEO Blog Post Writer)
- Full SaaS app dashboards (use Web Designer)
- Pages with no clear single offer (figure out the offer first)
