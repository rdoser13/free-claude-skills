---
name: web-designer
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
version: 1.1.0
---

# Web Designer

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics. Implement real working code with exceptional attention to aesthetic details and creative choices.

The user provides frontend requirements: a component, page, application, or interface to build. They may include context about the purpose, audience, or technical constraints.

## Design Thinking

Before coding, understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work -- the key is intentionality, not intensity.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail

## Working With a Brand Guide

If the user has a brand guide, style guide, or existing site, read it first and apply it automatically. If they specify different branding mid-task, follow their instructions instead.

When no brand guide exists, ask for these before committing to a direction:

- **Primary and accent colors** (or a reference site whose palette they like)
- **Typography preference** (or free rein)
- **Light or dark theme**
- **Tone** (see the aesthetic directions above)

Then propose a direction in one short paragraph and build once they confirm. Do not silently invent a brand identity for a real business.

### Landing page defaults that hold up

These are hard-won defaults, not rules. Override them when the brief calls for it.

- **Less content wins.** Start lean. Three to five sections is usually the right length for an offer page. Clients almost always ask for removals, rarely additions.
- **No fake social proof.** Never add testimonials, star ratings, logo bars, or subscriber counts unless the user supplies real ones. Invented proof is the fastest way to destroy trust, and for a real business it is a legal problem.
- **Mockups beat stock screenshots.** A styled CSS mockup of the product in use (a terminal, an app frame, a dashboard) reads as more credible than a stock photo and costs nothing to change.
- **One destination.** Every CTA on a single-offer page should point to the same URL. Competing CTAs split intent and reduce conversion.

**Terminal mockup pattern** (useful for developer tools and CLI products):

```css
.terminal { background: #0a0a16; border-radius: 12px; border: 1px solid rgba(255,255,255,0.12); }
.terminal-header { padding: 12px 16px; border-bottom: 1px solid rgba(255,255,255,0.05); }
.terminal-dot { width: 12px; height: 12px; border-radius: 50%; }
```

Use colored dots (red/yellow/green) in the header and show a realistic interaction with the actual product, including prompts and plausible output.

**Animations:**
- `fadeUp` keyframe on sections with staggered `animation-delay`
- Subtle `pulse` on the primary CTA
- Keep it minimal. One entrance animation per section is enough.

## Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font.
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.

NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds), predictable layouts and component patterns, and cookie-cutter design that lacks context-specific character.

Interpret creatively and make unexpected choices that feel genuinely designed for the context. No design should be the same. Vary between light and dark themes, different fonts, different aesthetics. NEVER converge on common choices (Space Grotesk, for example) across generations.

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations and effects. Minimalist or refined designs need restraint, precision, and careful attention to spacing, typography, and subtle details. Elegance comes from executing the vision well.

Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision.

## Practical Web Design Workflow

These tips come from real production experience building sites with AI:

### Framework
- **Plain HTML/CSS/JS for single landing pages.** No framework, no build step, no dependencies. Just an `index.html` file. This is the fastest path for disposable landing pages and product pages. Deploy directly to Cloudflare Pages.
- **Astro** for multi-page static sites. It's basically HTML -- Claude Code handles it natively. Just say "build me an Astro site" and it will install and scaffold everything.
- **ShadCN/UI** is worth using as a base design system. Just tell Claude "use ShadCN" and it will figure out the CLI install and component usage. The UI primitives save time on mobile responsiveness and accessibility.
- For React apps, use the component library primitives (Radix UI, etc.) but skip importing pre-built blocks. Let Claude one-shot the layout.

### The "99 Designs" Approach
Instead of asking for one design, ask for **multiple completely unique takes** on the same page. Generate 4-10 one-shots with distinct aesthetics, then pick the best one (or combine elements from multiple). This costs tokens but produces significantly better results than iterating on a single direction.

Example prompt pattern:
> "Take 4 completely unique takes on [brand/page]. Make them very distinct from each other. Different color schemes, layouts, typography, and overall aesthetic direction."

Then pick the winner and say: "Build me a design system based on take #2. Use that system for all future pages."

### Disposable Landing Pages
Think of landing pages as **disposable** -- they can be created in 15 minutes now. This changes how you approach marketing:
- Custom landing pages for email campaigns with strong CTAs
- Special promo pages for specific offers
- Event-specific pages that get thrown away after
- A/B test variants as entirely separate pages

### Design Refinement Process
1. **One-shot first** -- Let Claude generate the full page without intervention
2. **Review and refine** -- Run a second pass in plan mode to review the first draft and improve
3. **Design system extraction** -- Once you like a design, extract the system (colors, fonts, spacing, components) and apply it to future pages
4. **Don't fix old sites** -- If the code is messy from earlier models, start from scratch. It takes the same amount of time now.

### Deployment
- **Plain HTML sites:** No build step needed. Just push the folder to GitHub and connect to Cloudflare Pages. Set build output to `/` (root) with no build command.
- **Astro sites:** Build and preview locally with `npm run dev`. Push to GitHub with build command `npm run build` and output directory `dist`.
- Push to GitHub (make sure no API keys are committed). Init git in the project folder, create a GitHub repo, push.
- Connect to Cloudflare Pages (Workers & Pages > Create Application > Connect GitHub)
- **Subdomain strategy:** Serve product/offer pages from a subdomain (e.g. `offer.yourdomain.com`) rather than a path on the main site. This sidesteps theme and CMS conflicts and gives you full design control.
- Attach the subdomain through Cloudflare's domain interface (CNAME record pointing to the Pages project)
- Every GitHub push auto-deploys. That's it.
- Static sites (HTML or Astro) have zero risk of leaking secrets -- perfect for this workflow.

### Alternative Design Tools
- **Google Stitch** (free, powered by Gemini Flash): Give it URLs and images, get mock-ups back. Export as HTML zip, then pass to Claude Code to build the real Astro site. Good for visual exploration before committing to code.
- Use Stitch or similar when you want to explore visual directions without burning tokens on code generation.
